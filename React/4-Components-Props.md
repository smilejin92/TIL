# 4. Components & Props

> 컴포넌트는 UI를 독립적이며 재사용 가능한 조각으로 나눈 것이다.

이론적으로, React 컴포넌트는 자바스크립트의 함수와 같다. React 컴포넌트는 임의의 값(props)을 전달 받아 React Elements를 반환한다.



### 4.1 함수/클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 자바스크립트 함수를 작성하는 것이다.

```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
```

위의 함수는 생성할 React Element의 데이터(어트리뷰트, 하위 요소)를 포함하는 props 객체를 인수로 전달 받아 React Element를 생성 후 반환하므로 유효한 컴포넌트이다. 위와 같은 컴포넌트를 **함수 컴포넌트**라고 부른다.

ES6 클래스 문법을 사용하여 컴포넌트를 정의할 수 있다.

```jsx
class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>;
    }
}
```

React의 관점에서 위의 두 코드 예제는 동일하다.

클래스 컴포넌트는 함수 컴포넌트에 비해 더 많은 기능을 제공한다 (다음 장에서 소개).

| 자바스크립트 생성자 함수      | React 컴포넌트                   |
| ----------------------------- | -------------------------------- |
| 새로운 instance를 반환한다    | 새로운 React Element를 반환한다. |
| `new Person({ name: 'Jin' })` | `<Person name="Jin" />`          |



### 4.2 컴포넌트 렌더링

이전 장에서는 DOM 태그를 의미하는 React Element만 살펴보았다.

```jsx
const element = <div />;
```



React Element는 사용자가 직접 정의한 컴포넌트의 반환 값이될 수도 있다 (ex. 생성자 함수의 인스턴스).

```jsx
// Welcome 컴포넌트가 반환하는 React Element가 변수 element에 할당된다.
const element = <Welcome name="Jin" />;
```



React는 런타임시 변수 할당문의 우항이 컴포넌트 호출문일 경우, JSX 어트리뷰트를 하나의 객체에 담아 컴포넌트에 전달, 호출한다. 이때 전달되는 객체를 `props`라 한다. 

```jsx
// React Element를 생성/반환하는 함수 컴포넌트
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

// Welcome 함수 컴포넌트를 호출하여 React Element 생성, element 변수에 할당
const element = <Welcom name="Sara" />;

// root DOM 노드에 렌더
ReactDOM.render(element, document.getElementById('root'));
```

위의 예제의 실행 순서를 살펴보자.

1. `Welcome` 함수 컴포넌트 정의
2. `element` 변수 선언, `Welcome` 컴포넌트의 반환 값을 `element` 변수에 할당
3. `ReactDOM.render` 메소드에 변수 `element`와 root DOM 노드를 전달/호출.

> **컴포넌트의 이름은 항상 대문자로 작성한다.**
>
> React는 소문자로 시작하는 컴포넌트를 일반 DOM 태그로 취급한다. 예를 들어, `<div />`는 HTML의 div 태그로 취급되지만, `<Welcome />`은 컴포넌트로 취급되며 컴포넌트는 스코프내에 존재해야한다.



### 4.3 컴포넌트 구성

컴포넌트의 반환 값에 다른 컴포넌트의 반환 값을 사용할 수 있다 (ex. 함수의 반환 값에 다른 함수의 반환 값을 사용할 수 있다). 아래 코드 예제를 살펴보자.

```jsx
// Welcome 함수 컴포넌트
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

// App 함수 컴포넌트
function App() {
    return (
        // App 함수 컴포넌트의 반환 값에 Welcome 함수 컴포넌트를 호출할 수 있다.
    	<div>
        	<Welcome name="Sara" />
            <Welcome name="Cahal" />
            <Welcome name="Edite" />
        </div>
    );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

일반적으로 새롭게 생성한 React 앱은 최상단에 하나의 `App` 컴포넌트를 가진다.  However, if you integrate React into an existing app, you might start bottom-up with a small component like `Button` and gradually work your way to the top of the view hierarchy. 



### 4.4 컴포넌트 분리

아래 `Comment` 컴포넌트 예제를 살펴보자.

```jsx
function Comment(props) {
    return (
    	<div className="Comment">
        	<div className="UserInfo">
            	<img className="Avatar"
                    src={props.author.avatarUrl}
                    alt={props.author.name}
                />
                <div className="UserInfo-name">
                	{props.author.name}
                </div>
            </div>
            <div className="Comment-text">
            	{props.text}
            </div>
            <div className="Comment-date">
            	{formatDate(props.date)}
            </div>
        </div>
    );
}
```

`Comment` 컴포넌트는 `props` 객체를 전달 받고, `props` 객체는 프로퍼티로 `user`(객체), `text`(문자열), `date`(날짜)를 갖는다.

`Comment` 컴포넌트가 반환하는 React Elements는 중첩되어있고, 각 element를 재사용하기 어렵다. 아래 예제를 통해 `Comment` 컴포넌트를 분리시켜보자.

```jsx
function Avatar(props) {
    return (
    	<img className="Avatar"
            src={props.user.avatarUrl}
            alt={props.user.name}
        />
    );
}

function UserInfo(props) {
    return (
    	<div className="UserInfo">
            <Avatar user={props.user} />
            <div className="UserInfo-name">
                {props.user.name}
            </div>
        </div>
    );
}

function Comment(props) {
    return (
    	<div className="Comment">
        	<UserInfo user={props.author} />
            <div className="Comment-text">
            	{props.text}
            </div>
            <div className="Comment-date">
            	{formatDate(props.date)}
            </div>
        </div>
    );
}
```

`props`의 프로퍼티 이름을 지을 때 컴포넌트의 입장으로 짓는 것을 권장한다.

여러 번 사용되는 UI 부분을 컴포넌트화하여 관리하는 것을 권장한다.



### 4.5 Props 객체는 참조만 가능하다 (Read-Only).

함수 혹은 클래스로 컴포넌트를 정의할 때, 컴포넌트 내부에서 `props` 절대로 변경/재할당하면 안된다. 아래 예제를 살펴보자.

```jsx
function sum(a, b) {
    return a + b;
}
```

위와 같은 함수(컴포넌트)를 순수(pure) 함수(컴포넌트)라 표현한다. 컴포넌트로 전달된 인자의 값을 변경하지 않고, 전달된 특정 인수를 사용해 반환하는 값이 항상 동일하기 때문이다.

반면 아래 컴포넌트는 비순수하다. 인자 값을 직접 변경하기 때문이다.

```jsx
function withdraw(account, amount) {
    account.total -= amount;
}
```

React는 비교적 유연하지만 하나의 엄격한 규칙이 있다.

**React의 모든 컴포넌트는 전달 받은 props 객체를 변경하지 않는 순수 함수여야한다.** 이 규칙을 어기지 않고 UI를 동적으로 변경할 수 있는 state(상태) 관리에 대해 다음 장에서 알아보자.