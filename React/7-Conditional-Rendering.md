# Conditional Rendering

> 앱의 상태에 따라 필요한 컴포넌트들만을 렌더할 수 있다.

React에서의 조건부 렌더링 (Conditional Rendering)은 자바스크립트의 조건문과 동일하고 동작한다. 자바스크립트의 `if` 연산자 혹은 비교 연산자를 통해 현재 상태를 나타내는 컴포넌트를 렌더할 수 있다.

아래 두 컴포넌트를 살펴보자.

```jsx
function UserGreeting(props) {
    return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
    return <h1>Please sign up.</h1>
}
```

사용자의 로그인 상태를 확인하여 위의 두 컴포넌트 중 하나를 렌더하는 `Greeting` 컴포넌트를 정의해보자.

```jsx
function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;
    return isLoggedIn ? <UserGreeting /> : <GuestGreeting />;
}

ReactDOM.render(
    // isLoggedIn={true}로 어떻게 변경하는가?
    <Greeting isLoggedIn={false} />,
    document.getElementById('root')
);
```

위 예제는 `isLoggedIn` prop의 값에 따라 다른 컴포넌트를 렌더한다.



### 7.1 Element Variables

변수를 사용하여 React Element를 담아둘 수 있다. 상태에 따라 UI의 일부가 변경되어야할 때 유용하다.

아래 예제의 두 컴포넌트 `Logout`과 `Login` 컴포넌트를 살펴보자.

```jsx
function LoginButton(props) {
    return (
    	<button onClick={props.onClick}>
        	Login
        </button>
    );
}

function LogoutButton(props) {
    return (
    	<button onClick={props.onClick}>
        	Logout
        </button>
    )
}
```

위의 두 컴포넌트를 상태에 따라 알맞게 사용하는 stateful 컴포넌트 `LoginControl`를 작성해보자.

```jsx
class Login Control extends React.Component {
    constructor(props) {
        super(props);
        this.handleLoginClick = this.handleLoginClick.bind(this);
        this.handleLogoutClick = this.handleLogoutClick.bind(this);
        this.state = { isLoggedIn: false };
    }
    
    handleLoginClick() {
        this.setState({ isLoggedIn: true });
    }
    
    handleLogoutClick() {
        this.setState({ isLoggedIn: false });
    }
    
    render() {
        const isLoggedIn = this.state.isLoggedIn;
        let button;
        
        button = isLoggedIn ? <LogoutButton onClick={this.handleLogoutClick} /> : <LoginButton onClick={this.handleLoginClick} />;
        
        return (
        	<div>
            	<Greeting isLoggedIn={isLoggedIn} />
                {button}
            </div>
        );
    }
}

ReactDOM.render(
	<LoginControl />,
    document.getElementById('root')
);
```



### 7.2 비교 연산자와 인라인 If-Else

