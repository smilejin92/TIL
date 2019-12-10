# 이벤트 핸들링

> React에서의 이벤트 핸들링은 DOM 요소의 이벤트 핸들링과 매우 유사하다. 단, 몇가지 문법적인 차이가 있다.

* React 이벤트는 camelCase로 표기한다.
* JSX 사용시 함수 식별자를 이벤트 핸들러로서 전달한다.

예를 들면, HTML에서는 DOM의 이벤트에 함수를 아래와 같이 바인딩한다.

```html
<button onclick="activateLasers()">
    Activate Lasers
</button>
```

React에서는 이벤트에 함수 정의를 전달하여 핸들러를 바인딩한다.

```jsx
<button onClick={activateLasers}>
    Activate Lasers
</button>
```

또한 React에서는 default behavior를 막기 위해 `false`를 반환할 수 없다. default behavior를 막기 위해서는 `preventDefault`를 명시적으로 작성해야한다. 예를 들어, 일반 HTML에서는 앵커 태그 사용시 새창이 열리는 default behavior를 방지하기 위해 아래와 같이 `false`를 반환하였다.

```html
<a href="#" onclick="console.log('The link was clicked.'); return false">Click me</a>
```

React에서는 위의 코드가 아래와 같이 대체될 수 있다.

```jsx
function ActionLink() {
    function handleclick(e) {
        e.preventDefault();
        console.log('The link was clicked.');
    }
    return (
    	<a href="#" onClick={handleClick}>
        	Click me
        </a>
    );
}
```

위 예제에서의 `e` 이벤트 객체는 synthetic event이다. synthetic event는 React에서 W3C 규격에 맞게 정의되었다 (각 이벤트가 모든 브라우저에서 동일하게 동작하기 위해 wrapper로 싸놓음). 따라서 크로스 브라우징 이슈를 따로 생각하지 않아도 된다.

React를 사용할 때는 DOM 요소가 생성된 이후에  `addEventListener` 메소드로 리스너를 바인드할 필요가 없다. DOM 요소가 렌더될 때 리스너를 바인드해주면 된다 (인라인 이벤트 핸들러).

ES6 클래스 문법으로 컴포넌트를 정의할 때, 이벤트 핸들러를 사용하는 가장 일반적인 방법은 클래스 몸체에 메소드로 정의하는 방법이다. 예를 들어, 아래의 `Toggle` 컴포넌트는 사용자가 상태를 "ON"과 "OFF"로 변경할 수 있는 버튼을 렌더한다.

```jsx
class Toggle extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            isToggleOn: true;
        }
        // this 바인딩을 통해 handleClick 메소드 내부의 this가
    	// Toggle 인스턴스를 가리키도록 한다.
        this.handleClick = this.handleClick.bind(this);
    }
    
    handleClick() {
        this.setState(state => ({ isToggleOn: !state.isToggleOn }));
    }
    
    render() {
        return (
        	<button onClick={this.handleClick}>
            	{this.state.isToggleOn ? 'ON' : 'OFF'}
            </button>
        );
    }
}

ReactDOM.render(<Toggle />, document.getElementById('root'));
```



JSX 콜백에서 `this`가 무엇을 의미하는지에 대해 주의해야한다. 자바스크립트에서 메소드는 자신을 호출한 객체를 `this`로 가리킨다.

```javascript
const person = {
  name: 'Jin',
  whatIsThis() {
      console.log(this);
  }
};

person.whatIsThis(); // person {}
```



하지만 메소드가 일반 함수로 호출될 경우, 메소드 내부의 `this`는 항상 전역 객체를 가리키며, 엄격 모드에서는 `undefined`를 가리킨다.

```javascript
const person = {
  name: 'Jin',
  whatIsThis() {
      console.log(this);
  }
};

person.whatIsThis(); // person {}

const whatIsThis = person.whatIsThis;
whatIsThis(); // window, global, undefined
```

위 `Toggle` 컴포넌트 예제에서

1. `handleClick` 메소드를 `this`와 바인드하지 않고,
2. `render` 메소드 내부의 `<button>` 요소에 인라인 이벤트 핸들러 방식으로 함수 정의를 바인드하면
3. 이벤트 발생시 핸들러는 **일반 함수로 호출되므로** `handleClick` 메소드 내부의 `this`는 전역 객체를 가리키며,
4. 바벨 컴파일 이후 엄격 모드가 적용되어 `handleClick` 메소드 내부의 `this`는 `undefined`를 가리킨다.

따라서, `onClick={this.handleClick}`과 같이 함수 정의를 할당하는 경우, this 바인딩을 해주어야한다.

`bind` 함수를 사용하는 것이 번거롭다면 아래 두 가지 방법으로 우회할 수 있다.

#### 1. 클래스 필드 정의 제안

```jsx
class LoggingButton extends React.Componenet {
    // 아래 문법은 handleClick 내부의 this가 LoggingButton의
    // 인스턴스를 가르키도록 바인드한다.
    // 주의: '아직' 표준 사양이 아니다
    handelClick = () => {
        console.log('this is ', this);
    }
    
    render() {
        return (
            <button onClick={this.handleClick}>
            	Click Me
            </button>
        );
    }
}
```

클래스 필드 문법은 `Create React App`에 기본으로 활성화돼있다.

#### 2. 화살표 함수

```jsx
class LoggingButton extends React.Component {
    handleClick() {
        console.log('this is:', this);
    }
    
    render() {
        // 아래 문법은 handleClick 내부의 this가 LoggingButton의
        // 상위 컨텍스트의 this를 가리키도록 한다.
        return (
        	<button onClick={e => this.handleClick(e)}>
            	Click me
            </button>
        );
    }
}
```

화살표 함수는 함수 자체의 this 바인딩이 없다. 화살표 함수 내부에서 this를 참조하면 상위 컨텍스트의 this를 그대로 참조한다. 이를 Lexical this라 한다. 이는 마치 렉시컬 스코프와 같이 **화살표 함수의 this가 함수가 정의된 위치에 의해 결정된다는 것을 의미한다.**

화살표 함수 사용의 문제점은 `LoggingButton` 컴포넌트가 렌더될 때마다 새로운 콜백이 생성된다는 것이다. 만약 콜백(이벤트 핸들러)가 하위 컴포넌트의 props로 전달되면, 하위 컴포넌트에서 추가적인 re-렌더링이 발생할 수 있다. 컨스트럭터 내부에서 this 바인딩을 해주거나 클래스 필드 정의 제안을 사용하는 것을 권장한다.



### 6.1 이벤트 핸들러에 인수 전달

아래 예제는 이벤트 핸들러에 이벤트 객체 `e` 외의 추가적인 인수를 전달하는 경우이다.

```jsx
<button onClick={e => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

위 예제의 두 버튼 요소는 동일하다. 각각 화살표 함수와 `bind` 함수를 사용한 예제이다.

두 예제 모두 React 이벤트를 의미하는 인수 `e`가 `id` 이후 두 번째 인수로 전달된다. 화살표 함수 사용시, 명시적으로 `e` 객체를 전달해야하지만, `bind` 함수 사용시 추가적인 인수 `e`는 `arguments` 객체의 요소로 추가되어 자동으로 전달된다.

