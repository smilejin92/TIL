SPA

모든 것을 뷰로 취급한다.

```jsx
import React, {Componenet} from 'react';
import './App.css';

class App extends Component {
    render() {
        <div className="App">
        	<div className="App-header">
            	<h2>Welcome to React</h2>
            </div>
            <p className="App-intro">
            	To get started, edit <code>src/App.js</code> and save to reload.
            </p>
        </div>
    }
}
```

바벨에 의해 JSX 코드는 자바스크립트 엔진이 알아들을 수 있게 컴파일된다.

React에서 모든 요소는 불변하다.

`import App from ./App` (.js 확장자는 생략 가능)

`<div id="root">` 안에 render



소스 코드를 업데이트하면 브라우저가 리로드 되지 않고도 업데이트가 반영된다.

```jsx
if (module.hot) {
  module.hot.accept();
}
```

JSX 내에서 자바스크립트에서 값으로 평가되는 표현식을 사용하려면 중괄호로 감싸고, 그 안에서 또 JSX 문법이 나오면 중첩해서 중괄호를 사용한다.

`<div key={item.objectID}`

리액트에서 상태 변화를 감지하는 방법은 key값의 변화를 감지하는 방법이다.

key 값으로 배열의 인덱스를 넣으면 절대 안된다. 알아볼 수 있는 절대적인 값이 필요하다. (정렬 때문) 최상위 노드의 key 값을 설정해야한다.

순회하면서 return할때 필요하다 key값이 (**pg. 21**)

map

state <-> setState

프로퍼티 다음 쉼표를 남겨놓는건 이후에 더 추가 될수도 있다는 것을 명시적으로 알리기 위함이다.

fetch는 크로스브라우징, status.ok확인, 쿠기를 전달 불가