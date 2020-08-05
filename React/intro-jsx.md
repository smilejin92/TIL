# Introducing JSX

JSX는 React에서 제공하는 특별한 문법(syntax extension to JavaScript)이다. JSX를 사용하여 React element를 간편하게 생성할 수 있다.

```react
// with JSX
const element = <h1 class="greeting">Hello, world!</h1>;

// without JSX
const element = React.createElement(
	"h1", // type
  { className: "greeting" }, // props
  "Hello, world!" // children
);
```

* JSX로 작성한 코드는 babel에 의해 자바스크립트 코드로 transplie된다.
* JSX는 "React elements"를 생성한다.

&nbsp;  

## Why JSX?

* JSX를 필수적으로 사용해야하는 것은 아니다.
* JSX를 사용하면 가독성을 높일 수 있다.
* JSX를 사용하면 React에서 보다 useful한 에러와 경고 메시지를 제공한다.

&nbsp;  

## 표현식 삽입 in JSX

* JSX 안에 값을 embed 하기 위해서는 curly braces(`{}`)를 사용한다.
* curly braces 안에는 "유효한"(valid) 자바스크립트 표현식이 들어올 수 있다.

```react
const name = <span>{user.name}</span>;
const age = <span>{10 + 19}</span>;
```

* 여러 줄에 걸쳐 JSX를 작성할 경우, 소괄호로 감싸는 것이 좋다. 세미콜론 자동 삽입 기능을 방지하기 위함이다.

```react
const Header = (
	<header>
  	<h1>Hello World!</h1>
    <p>This is a greeting paragraph.</p>
  </header>
);
```

&nbsp;  

## JSX 또한 표현식이다.

* JSX는 자바스크립트 표현식이다. Babel에 의해 JSX가 transplie되면 일반 자바스크립트 함수 호출문으로 실행되며, 해당 함수 호출문(`React.createElement()`)은 자바스크립트 객체로 평가된다.
* JSX가 표현식이라는 말은, `if`문과 `for`문, 변수 할당문, 함수 호출시 전달되는 arguments, 함수의 return 값 등으로 사용될 수 있다는 뜻이다.

```react
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}</h1>
  }
  return <h1>Hello, Stranger.</h1>
}
```

&nbsp;  

## 어트리뷰트 정의 with JSX

* 어트리뷰트 값의 타입이 string일 경우, 문자열 리터럴을 따옴표로 감쌀 수 있다.

```react
const element = <div tabIndex="0"></div>;
```

* 어트리뷰트 값으로 자바스크립트 표현식을 할당할 경우 중괄호로 감쌀 수 있다.

```react
const element = <img src={user.avatarUrl}></img>;
```

* 어트리뷰트 값으로 자바스크립트 표현식을 할당할 때 중괄호를 따옴표로 감싸면 안된다. 따옴표(문자열 리터럴) 혹은 중괄호(표현식) 둘 중 하나만 사용한다.

```react
const element = <img src="{user.avatarUrl}"></img>; // NOPE
```

&nbsp;  

> **주의**
>
> JSX는 HTML 보다 자바스크립트에 더 가까운 문법이므로, JSX로 생성한 React element의 프로퍼티(어트리뷰트) 네이밍은 카멜 케이스를 따른다.
>
> 예를 들어, HTML 요소의 `class`, `tabindex` 어트리뷰트는 React element의 `className`, `tabIndex` 프로퍼티로 작성한다.

&nbsp;  

## 자식 요소 작성 with JSX

* 만약 JSX 태그가 비어있다면, XML처럼 닫는 태그(`/>`) 바로 사용할 수 있다.

```react
const element = <img src="{user.avatarUrl}" />;
```

* JSX 태그는 자식 요소(React elements)를 포함할 수 있다.

```react
const element = (
	<div>
    {/* children */}
  	<h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

&nbsp;  

## JSX는 XSS 공격을 방지한다.

* JSX를 사용하면 사용자 입력을 JSX에 embed 하여도 안전하다.

```react
const title = response.petentiallyDangerousInput;
// 안전하다.
const element = <h1>{title}</h1>;
```

* 기본적으로 React DOM은 JSX에 embed된 모든 값을 escape 처리하여 렌더링한다.
* 따라서 애플리케이션에 명시적으로 작성된 것이 아니면, 그 어떠한 것도 inject 할 수 없다.
* 모든 요소는 문자열로 convert되어 렌더링된다. 따라서 XSS 공격을 방지한다.

&nbsp;  

## JSX는 객체를 나타낸다.

* 앞서 살펴보았듯 JSX는 Babel에 의해 transplie되어 `React.createElement()` 호출문으로 실행된다. 아래 두 예제는 identical하다.

```react
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```react
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

* `React.createElement()`는 bug-free한 코드를 작성할 수 있도록 도와준다(validation test). **또한 아래와 같은 객체를 생성한다.**

```react
// 아래 객체의 모습은 simplified 된 것이다.
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

* 이러한 객체를 "React Elements"라 부른다. React element는 UI에 대한 정보를 포함하고 있다.
* React는 React element를 읽어들여 DOM을 생성하고 최신화한다.

&nbsp;  

