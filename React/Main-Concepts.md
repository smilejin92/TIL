# Main Concepts

## 1. Hello World

![](./img/hello-world.png)



React 공식 문서를 통해 React 앱의 elements와 components가 무엇인지 살펴보자.



## 2. Introduing JSX

아래 변수 선언문을 살펴보자.

```jsx
const element = <h1>Hello, world!</h1>;
```

위의 태그 문법은 문자열도 아니며 HTML도 아니다. 이것은 자바스크립트의 확장형 문법인 JSX라 불린다. UI가 어떻게 구성되어야 하는지 정확히 표현하기 위해 JSX와 React를 함께 사용하는 것을 권장한다. JSX가 템플릿 언어처럼 보일 수 있지만, 자바스크립트의 모든 기능을 포함하고 있다. JSX를 사용하려면 react 모듈을 import 해야한다.

JSX는 React Elements를 생성한다. React Elements를 DOM에 렌더하는 것은 다음 장에서 살펴볼 것이다. 아래는 JSX의 기본적인 개념에 대한 내용이다.



### 2.1 왜 JSX를 사용하는가?

React는 렌더링 로직이 이벤트 처리, 혹은 상태(state) 변화와 같은 UI 로직과 본질적으로 연결돼있는 점을 수용한다. React는 마크업(HTML)과 로직(JS)을 분리하여 저장하지 않는 대신, 마크업과 로직을 모두 포함하는 컴포넌트(components)를 통해 관심사를 분리한다 (Separate of Concerns).

React에서 JSX의 사용이 필수적이지는 않지만, 대부분의 사람들이 가독성 측면에서 JSX 사용을 선호하는 편이다. 또한 JSX는 보다 유용한 에러와 경고 메시지를 제공한다.



### 2.2 JSX 내부의 표현식

아래 예제는 `name` 변수를 선언하여 `{}` 중괄호로 감싼 뒤 JSX 내부에서 사용한다.

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

자바스크립트에서 표현식(값)으로 평가되는 모든 문법을  `{}` 중괄호로 감싼 뒤 JSX 내부에서 사용할 수 있다. 예를 들면, `2 + 2`, `user.firstName`, `formatName(user)` 모두 유효한 자바스크립트 표현식이다.



아래 예제는 자바스크립트 함수의 반환 값 `formatName(user)`을 `<h1>` 요소 안에 삽입하는 과정이다.

```jsx
function formatName(user) {
    return user.firstname + ' ' + user.lastName;
}

const user = {
    firstName: 'Harper',
    lastName: 'Perez'
};

// JSX
const element = (
	<h1>
    	Hello, {formatName(user)}!
    </h1>
);

ReactDOM.render(
	element,
    document.getElementById('root')
);
```

JSX 사용시 가독성을 위해 개행을 해주었다. 또한 JSX 사용시 세미콜론 자동 삽입 기능을 방지하기 위해 `()` 소괄호로 감싸주는 것을 권장한다.



### 2.3 JSX 또한 표현식이다

바벨 컴파일 이후, **JSX 표현식은 일반 자바스크립트 함수 호출문으로 해석되어 자바스크립트 객체를 생성한다.** 즉, JSX 문법을 `if...else`, `for`, 할당문, 함수의 인수, 함수의 반환 값 등 다양하게 사용할 수 있다.

```jsx
function getGreeting(user) {
    if (user) {
        return <h1>Hello, {formatName(user)}!</h1>;
    }
    return <h1>Hello, Stranger.</h1>;
}
```

위의 코드는 Babel에 의해 아래 코드로 치환된다.

```jsx
"use strict";

function getGreeting(user) {
  if (user) {
    return React.createElement("h1", null, "Hello, ", formatName(user), "!");
  }
  return React.createElement("h1", null, "Hello, Stranger.");
}
```



### 2.4 JSX로 어트리뷰트 명시

요소(React Element)의 어트리뷰트 값으로 문자열 리터럴을 할당할 때 큰 따옴표를 사용할 수 있다.

```jsx
const element = <div tabIndex="0"></div>;
```



요소의 어트리뷰트 값으로 자바스크립트 표현식을 할당할때 `{}`중괄호로 감싸준다.

```jsx
const element = <img src={user.avatarUrl}></img>;
```



단, 자바스크립트 표현식을 감싼 중괄호를 큰 따옴표로 감싸면 안된다.

```jsx
const element = <img src="{user.avatarUrl}"></img>; // NOPE
```



> **경고**
>
> JSX는 HTML 보다 JavaScript에 더 가까운 문법이기 때문에, React DOM은 요소의 어트리뷰트를 `camelCase`로 표현한다.
>
> 예를 들어, HTML 태그의 어트리뷰트 `class`는 React DOM에서 `className`로 표현하며, `tabIndex` 어트리뷰트도 `tabIndex`로 표현한다.



### 2.5 JSX로 하위 요소 명시

만약 태그가 비었다면 (하위 태그, 혹은 텍스트가 없다면)  `/>`로 즉시 닫아준다.

```jsx
const element = <img src={user.avatarUrl} />;
```



JSX 태그는 자식을 포함할 수 있다.

```jsx
const element = (
	<div>
    	<h1>Hello!</h1>
        <h2>Good to see you here.</h2>
    </div>
);
```



### 2.6 JSX는 XSS를 방지한다.

user input을 JSX 내부에서 안전하게 사용할 수 있다.

```jsx
const title = response.potentiallyMaliciousInput;
// 아래 코드는 안전하다.
const element = <h1>{title}</h1>;
```

By default, React DOM escapes any values embedded in JSX before rendering them.  Thus it ensures that you can never inject anything that's not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent XSS (cross-site-scripting) attacks.



### 2.7 JSX는 객체로 변환된다

Babel을 통해 JSX 문법은 `React.createElement()`로 컴파일된다. (2.3 참고)

아래 두 예제는 동일하다.

```jsx
const element = (
	<h1 className="greeting">
    	Hello, world!
    </h1>
);
```

```jsx
const element = React.createElement(
	'h1',
    {className: 'greeting'},
    'Hello, world!'
);
```

`React.createElement()`는 몇 가지 검사를 실행한 뒤 아래와 같은 **객체를 생성**한다.

```java
const element = {
    type: 'h1',
    props: {
        className: 'greeting',
        children: 'Hello, world!'
    }
};
```

**이러한 객체를 React element(요소)라 부른다.** React는 React Element를 해석하여 DOM을 생성하고 DOM의 상태를 최신으로 유지한다.

