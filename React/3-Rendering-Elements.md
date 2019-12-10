# 3. Rendering Elements

요소(element)는 사용자가 화면을 통해 보는 컨텐츠를 표현한다.

```jsx
const element = <h1>Hello, world</h1>;
```

브라우저 DOM 요소와는 달리, React 요소는 일반 객체이며 생성시 필요한 비용이 비교적 적다. React DOM은 DOM을 React Element와 일치할 수 있도록 최신 상태로 업데이트한다.

> **Elements vs. Components**
>
> 요소(Elements)는 컴포넌트를 이루는 최소 단위이다.



### 3.1 DOM 내부에 요소 삽입/렌더

HTML 파일에 `<div>` 태그가 있다고 가정해보자.

```html
<div id="root"></div>
```

위 `<div>` 태그의 하위로 들어가는 모든 요소는 React DOM에 의해 관리되므로 위의 `<div>` 태그를 "root"라고 부른다.

React로 개발된 어플리케이션은 보통 한 개의 root DOM 노드를 가진다. 만약 이전에 개발된 앱에 React를 추가한다면, 필요한 만큼의 isolated(독립적인) root DOM 노드를 생성해도된다.

React Element를 root DOM 노드에 렌더하고 싶다면 `ReactDOM.render` 메소드에 React Element와 root DOM 노드를 인수로 전달하여 호출한다.

```jsx
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```



### 3.2 렌더된 요소 업데이트

React Elements는 변경할 수 없다(immutable). React Element를 한번 생성하면, 해당 요소의 속성과 하위 요소를 변경할 수 없다. 지금까지 배운 내용만으로 UI를 업데이트 하는 유일한 방법은 새로운 React Element를 생성하여 `ReactDOM.render`에 인수로 전달 후 호출하는 방법 뿐이다.

아래 시계 예제를 살펴보자.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

function tick() {
    const element = (
    	<div>
        	<h1>Hello, world!</h1>
            <h2>It is {new Date().toLocaleTimeString()}.</h2>
        </div>
    );
    ReactDOM.render(element, document.getElementById('root'));
}
setInterval(tick, 1000);
```

`setInterval` 함수로 매초 `ReactDOM.render` 메소드를 호출한다.



### 3.3 React는 필요한 부분만 업데이트한다.

React DOM은 React Element와 React Element의 하위 요소를 이전 상태와 비교하여 변경된 부분만을 DOM에 반영한다. 

<img src="./img/dom-update.png" style="zoom:60%;" />

3.2 시계 예제에서는 매초 모든 UI를 새롭게 그리지만, `<h2>` 태그의 텍스트만을 업데이트한다.