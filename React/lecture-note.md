# JSX

```javascript
/** @jsx virtualDOM */ 
```

![](C:\Users\Jinhyun Kim\Desktop\jsx-transfile.png)

 /** @jsx virtualDOM**/  -jsx를 사용하겠다는 선언문,  react를 import를 하지 않고, 내부적으로 virtualDOM을 사용하겠다는 선언. (import React from 'react'; 대신 사용)

바벨이 해석한다.

# Virtual DOM

리액트는 DOM을 조작하지 않는다.



1. index.html 로드
2. index.js 로드
   1. index.js에서 import한 리액트 코드를 실행?
   2. 



* `create.element`
* `render()`

package.json scripts 부분에 npm start 하면 index.html에 index.js를 주입





function virtualDOM(type, props, ...child)

type - 태그 종류

props - 태그 어트리뷰트

child - 하위 요소 (including text)



디버깅 - add to watch



App.js의 App() 내부에서 return 하는 html 요소에서의 class는 className으로 대체한다.

img 태그의 alt 어트리뷰트를 무조건 넣어야한다.

html 태그의 어트리뷰트 값은 {}안에 자바스크립트에서 값으로 취급되는 모든 코드를 넣을 수 있다.

이벤트 이름 등 두 단어 이상의 속성은 모두 camel case로 대체한다. (ex. onclick = onClick)

각 html 태그를 모두 컴포넌트로 취급한다.

양방향 바인딩을 통해 상태를 관리한다.

상태 (state)는 첫 자를 대문자로 표기한다.

기존의 App.js

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

```

상태 관리 App.js

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

// Stateless component
const Header = props => <header>{props.children}</header>;

function App() {
  return (
    <div className="App">
      <Header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </Header>
    </div>
  );
}

export default App;

```

props 객체에 className 프로퍼티와 children 프로퍼티가 있다.



오리지널 버전

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

```

react에서 상태는 모두 setState 함수로 변경한다. 직접 변경하면 안된다. 왜? 그냥 그렇게 설계돼있어서?

setState는 비동기 함수다

인라인 핸들러 바인딩시 파라미터를 넘길 경우 화살표 함수로 정의, 아닌 경우 함수 정의만 표기