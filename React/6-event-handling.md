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

위 예제에서의 `e`는 synthetic event이다. synthetic event는 React에서 W3C 규격에 맞게 정의되었다 (각 이벤트가 모든 브라우저에서 동일하게 동작하기 위해 wrapper로 싸놓음). 따라서 크로스 브라우징 이슈를 따로 생각하지 않아도 된다.

React를 사용할 때는 DOM 요소가 생성된 이후에  `addEventListener` 메소드로 리스너를 바인드할 필요가 없다. DOM 요소가 렌더될 때 리스너를 바인드해주면 된다.

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

