# 함수와 일급 객체

## 1. 일급 객체

함수는 값이다. 함수형 프로그래밍을 위해 함수는 값으로 설계되었다.

무명 함수 리터럴은 반드시 할당해야한다. 유명 함수 리터럴은 함수 선언문으로 해석될 수 있다.

함수면 [[Call]] 내부 슬롯이 무조건 있지만, 모든 함수가 [[Construct]] 내부 슬롯을 가지진 않는다.

## 2. 함수 객체의 프로퍼티

함수는 객체이다. 따라서 함수도 프로퍼티를 가질 수 있다. 브라우저 콘솔에서 `console.dir` 메소드를 사용하여 함수 객체의 내부를 들여다 보면 아래와 같이 출력된다.

<img src="https://user-images.githubusercontent.com/32444914/81144671-86b0bd80-8faf-11ea-8afa-ff613db1ae9b.png" width="80%" />

일반 객체에는 없는 `arguments`, `caller`, `length`, `name`, `prototype`, `__proto__` 프로퍼티가 함수 객체에는 존재한다. square 함수의 모든 프로퍼티의 프로퍼티 어트리뷰트를 `Object.getOwnPropertyDescriptors` 메소드로 확인해 보면 아래와 같다.

```javascript
console.log(Object.getOwnPropertyDescriptors(square));
/*
{
  length: {value: 1, writable: false, enumerable: false, configurable: true},
  name: {value: "square", writable: false, enumerable: false, configurable: true},
  arguments: {value: null, writable: false, enumerable: false, configurable: false},
  caller: {value: null, writable: false, enumerable: false, configurable: false},
  prototype: {value: {...}, writable: true, enumerable: false, configurable: false}
}
*/

// __proto__는 square 함수의 프로퍼티가 아니다.
console.log(Object.getOwnPropertyDescriptor(square, '__proto__'));
// undefined

// __proto__는 Object.prototype 객체의 접근자 프로퍼티이다.
// square 함수는 Object.prototype 객체로부터 __proto__ 접근자 프로퍼티를 상속받는다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {get: ƒ, set: ƒ, enumerable: false, configurable: true}
```

`arguments`, `caller`, `length`, `name`, `prototype` 프로퍼티는 모두 함수 객체의 **데이터 프로퍼티**이다. 하지만 `__proto__`는 접근자 프로퍼티이며 `Object.prototype` 객체의 프로퍼티를 상속 받은 것이다.

&nbsp;  

### 2.1. arguments 프로퍼티

함수 객체의 arguments 프로퍼티 값은 **arguments 객체**이다. arguments 객체는 **함수 호출시 전달된 인수(arguments)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체(array-like object)이며 함수 내부에서 지역 변수처럼 사용된다.** 함수 외부에서는 참조할 수 없다.

> **arguments 프로퍼티**
>
> 함수 객체의 arguments 프로퍼티는 현재 일부 브라우저에서 지원하고 있지만, ES5부터 표준에서 폐지(deprecated)되었다. 따라서 Function.arguments와 같은 사용 방법은 권장되지 않으며 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체를 참조하도록 한다.



this, arguments, new.target은 함수 몸체내서 참조할 수 있다.

p.hasOwnProperty(); // hasOwnProperty에 빨간 줄이 그어지는 이유는 해당 메소드를 사용하는 객체는 Object.prototype과 같은 프로토타입 체인에 존재해야한다고 가정하기 때문이다. 객체 중에는 프로토타입이 Object.prototype이 아닐 수도 있다.(ex. Object.create(null))

