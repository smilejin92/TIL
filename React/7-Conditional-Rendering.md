# Conditional Rendering

> 앱의 상태에 따라 필요한 컴포넌트들만을 렌더할 수 있다.

React에서의 조건부 렌더링 (Conditional Rendering)은 자바스크립트의 조건문과 동일하게 동작한다. 자바스크립트의 `if` 연산자 혹은 비교 연산자를 통해 현재 상태에 따라 컴포넌트를 선택적으로 렌더할 수 있다.

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
class LoginControl extends React.Component {
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
        
        if (isLoggedIn) {
            button = <LogoutButton onClick={this.handleLogoutClick} />;
        } else {
            button = <LoginButton onClick={this.handleLoginClick} />
        }
        
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

변수를 선언하여 if문을 사용하는 방법 외에도 JSX 내부에서 인라인으로 조건문을 사용할 수 있다. 아래에 자세히 설명하겠다.



### 7.2 단축 평가 - 논리곱 연산자 &&

논리곱 연산자 `&&`는 논리 평가를 결정한 피연산자를 그대로 반환한다.

| 단축 평가 표현식  | 평가 결과 |
| ----------------- | --------- |
| true && anything  | anything  |
| false && anything | false     |

단축 평가식을 JSX 내부에서 중괄호 `{}`로 감싸 사용할 수 있다. 조건부 렌더링에서 단축 평가는 매우 유용하게 사용될 수 있다.

```jsx
function Mailbox(props) {
    const unreadMessages = props.unreadMessages;
    return (
    	<div>
        	<h1>Hello!</h1>
            {unreadMessages.length > 0 && 
            	<h2>
                    You Have {unreadMessages.length} unread messages.
                </h2>
            }
        </div>
    )
}

const messages = ['React', 'Re: React', 'Re: Re: React'];
ReactDOM.render(
	<Mailbox unreadMessages={messages} />,
    document.getElementById('root')
);
```

단축 평가식이 `true`로 평가되면, 피연산자(`&&` 뒤의 값)를 그대로 반환한다. 만약 단축 평가식이 `false`로 평가되면, `false`를 반환한다.



### 7.3 삼항 연산자

`condition ? true : false`

조건이 true로 평가되면, `:` 앞의 피연산자가 그대로 반환되며, false인 경우 `:` 뒤의 피연산자가 그대로 반환된다.

```jsx
render() {
    const isLoggedIn = this.state.isLoggedIn;
    return (
    	<div>
        	The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
        </div>
    );
}
```



### 7.4 컴포넌트 렌더 방지

아주 특별한 경우 컴포넌트가 렌더되었지만, 숨김 처리 해야하는 상황이 생길 수 있다. 이러한 경우,  렌더하려는 요소 대신 `null`을 반환하면된다.

```jsx
function WarningBanner(props) {
    if (!props.warn) return null;
    
    return (
    	<div className="warning">
        	Warning!
        </div>
    );
}

class Page extends React.Component {
    constructor {
        ...
        this.state = { showWarning: true };
        ...
    }
        
    ...
    
    render() {
        return (
            ...
        	<div>
            	<WarningBanner warn={this.state.showWarning} />
            </div>
            ...
        );
    }
}
ReactDOM.render(
	<Page />,
    document.getElementById('root')
);
```

컴포넌트의 `render` 메소드 내부에서 `null`을 반환하는 것은 해당 컴포넌트의 생명 주기 메소드에 영향을 주지 않는다. 예를 들어, `null`이 반환되어도 `componentDidUpdate` 메소드는 그대로 호출된다.