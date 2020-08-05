# Components and Props

* 컴포넌트는 UI를 독립적이며, 재사용 가능한 조각으로 나눌 수 있게 해준다.
* 이론상으로, 컴포넌트는 자바스크립트의 함수와 비슷하다. 임의의 입력(props)를 전달받아 React element를 반환한다.

&nbsp;  

## 함수 컴포넌트와 클래스 컴포넌트

컴포넌트를 정의하는 가장 쉬운 방법은 자바스크립트 함수를 작성하는 것이다.

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

위 함수는 단일 "props"(properties의 준말)를 전달받아 리액트 요소를 반환하기 때문에 유효한 리액트 컴포넌트이다. 이러한 컴포넌트를 함수 컴포넌트(function component)라 부른다.

ES6 클래스 문법을 사용하여 컴포넌트를 정의할 수도 있다.

```react
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

리액트의 관점에서 위 두 개의 컴포넌트는 동치(equivalent)이다.

함수와 클래스 컴포넌트 모두 추가적인 기능을 가지며, 이에 대해서는 다음 장에서 살펴 볼 것이다.

&nbsp;  

## 컴포넌트 렌더링

지금까지는 DOM 태그를 나타내는 리액트 요소만 다루었다.

```react
const element = <div />;
```

리액트 요소는 사용자 정의 컴포넌트도 나타낼 수 있다.

```react
const element = <Welcome name="Sara" />;
```

리액트는 사용자 정의 컴포넌트를 나타내는 요소를 만나면 JSX 어트리뷰트와 자식 요소(children)를 **하나의 객체에 묶어** 전달한다. 이러한 객체를 "props"라 부른다.

예를 들어, 아래 코드는 "Hello, Sara"를 페이지에 렌더한다.

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

위 예제의 실행 순서는 아래와 같다.

1. `ReactDOM.render` 메소드에 `<Welcome name="Sara" />` 요소를 전달하여 호출한다.
2. React는 `Welcome` 컴포넌트를 `{ name: 'Sara' }` 객체를 "props"로 전달하여 호출한다.
3. `Welcome` 컴포넌트는 `<h1>Hello, Sara</h1>` 요소를 반환한다.
4. React DOM은 브라우저 DOM을 ``<h1>Hello, Sara</h1>`와 match되도록 업데이트 한다.

&nbsp; 

> **Note: 컴포넌트 이름은 항상 대문자로 시작한다.**
>
> React는 이름이 소문자로 시작하는 컴포넌트를 DOM 태그로 간주한다.

&nbsp;  

## 컴포넌트 구성하기

* 컴포넌트는 자신의 return 결과에 다른 컴포넌트를 포함할 수 있다.
* 동일한 컴포넌트에 다른 props를 넘겨 재사용할 수 있다.

예를 들어, `App` 컴포넌트의 렌더 아웃풋에 `Welcome` 컴포넌트를 원하는 만큼 작성할 수 있다.

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

&nbsp;  

## 컴포넌트 분리하기

컴포넌트를 더 작은 컴포넌트로 분리하여 작성할 수 있다.

아래 `Comment` 컴포넌트를 살펴보자.

```react
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

위와 같이 여러가지 요소가 중첩되어 있는 컴포넌트는 유지보수하기 까다로울 수 있다. 또한 컴포넌트의 각 부분을 재사용하기 어렵다. 위 예제에서 몇가지 컴포넌트를 추출해보자.

&nbsp;  

### 1. `Avatar` 컴포넌트 분리

```react
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

`Avatar` 컴포넌트는 자신이 `Comment` 컴포넌트 안에서 렌더된다는 것을 알 필요가 없다. 때문에 `author`라는 prop 이름 보다 generic한 이름 `user`로 prop 이름을 변경하였다.

props의 네이밍은 컴포넌트를 사용하는 관점에서 결정하는 것 보다, 컴포넌트 자신의 관점에서 결정하는 것이 좋다.

&nbsp;  

### 2. `UserInfo` 컴포넌트 분리

1에서 분리한 `Avatar` 사용하여 아래와 같이 `UserInfo` 컴포넌트를 분리할 수 있다.

```react
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
```

&nbsp;  

1, 2에서 분리한 컴포넌트를 사용하여 이전의 `Comment` 컴포넌트를 아래와 같이 작성할 수 있다.

```react
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

아래와 같은 경우에 컴포넌트를 분리시키는 것이 좋다.

1. UI의 일부분이 중복되는 경우
2. 컴포넌트 자체가 복잡한 경우

&nbsp;  

## Props는 Read-only이다.

* 모든 리액트 컴포넌트는 순수 함수처럼 동작해야한다.
* 즉, 같은 props을 전달하여 렌더하면 같은 UI가 렌더되어야 한다.

&nbsp;  

