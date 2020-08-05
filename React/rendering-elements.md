# Rendering Elements

* React Elements(이하 요소)는 React app을 만드는 가장 작은 단위이다.
* 요소는 화면에 표시되어야 할 정보를 나타낸다.

```react
const element = <h1>Hello, world</h1>;
```

* 브라우저 DOM 요소와는 달리, React 요소는 일반 객체이며 생성하는 데 소모되는 비용이 적다.
* React DOM은 브라우저 DOM을 React 요소와 match 되도록 업데이트 시킨다.

&nbsp;  

## 요소 렌더링 into the DOM

HTML 파일 어딘가에 아래와 같은 `<div>` 요소가 있다고 해보자.

```html
<div id="root"></div>
```

위 요소를 "root" DOM 노드라고 부른다. 해당 root 노드 하위의 모든 것은 React DOM에 의해 관리될 것이기 때문이다.

* React로만 만들어진 어플리케이션은 대체로 단일 root DOM 노드를 가진다.
* 만약 이미 만들어진 애플리케이션에 React를 intergrate 할 것이라면, 필요한 만큼의 독립된(isolated) root DOM 노드를 작성할 수 있다.
* 리액트 요소를 root DOM 노드 안에 렌더하기 위해서는 `ReactDOM.render` 메소드에 리액트 요소와 root DOM 노드를 전달하여 호출한다.

```react
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

&nbsp;  

## 렌더된 요소 업데이트하기

* 리액트 요소는 immutable하다. 즉, 한번 요소를 생성하면, 요소의 어트리뷰트나 자식 요소(children)을 변경할 수 없다.
* 지금까지 살펴본 내용만으로 UI를 업데이트 할 수 있는 방법은 새로운 요소를 생성한 후 `ReactDOM.render` 메소드를 다시 호출하는 것 뿐이다.

아래 시계 예제를 살펴보자.

```react
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

`setInterval`의 콜백이 매초 `ReactDOM.render` 메소드를 호출한다.

&nbsp;  

## React는 필요한 것만 업데이트 한다.

* React DOM은 요소와 자식 요소를 이전에 렌더된 요소와 비교하여 변경된 부분만을 DOM에 적용한다.
* 위의 시계 예제에서 `<div>` 요소를 포함한 모든 하위 요소를 매초 새롭게 생성하지만, 실질적으로 변경된 부분(`<h2>`의 텍스트 노드)만이 React DOM에 의해 업데이트 된다.

&nbsp;  

















