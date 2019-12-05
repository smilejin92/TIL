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
// Welcome 컴포넌트가 반환하는 React Element가 할당된다 변수 element에 할당된다.
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

컴포넌트의 반환 값에 다른 컴포넌트