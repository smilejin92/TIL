# 빌트인 객체

## 1. 자바스크립트 객체의 분류

자바스크립트 객체는 다음과 같이 크게 3개의 객체로 분류할 수 있다.

**1. 표준 빌트인 객체**

표준 빌트인 객체(standard built-in objects)는 ECMAScript 사양에 정의된 객체를 말하며, **애플리케이션 전역의 공통 기능을 제공한다.** 표준 빌트인 객체는 ECMAScript 사양에 정의된 객체이므로 자바스크립트 **실행 환경과 관계없이 언제나 사용할 수 있다.** 표준 빌트인 객체는 **전역 객체의 프로퍼티**로서 제공된다. 따라서 별도의 선언 없이 전역 변수처럼 언제나 참조할 수 있다.

&nbsp;  

**2. 호스트 객체**

호스트 객체(host objects)는 ECMAScript 사양에 정의되어 있지 않지만, **자바스크립트 실행 환경에서 추가로 제공하는 객체**를 말한다. **브라우저 환경에서는** DOM, BOM, Canvas, XMLHttpRequest, fetch, requestAnimationFrame, SVG, Web Storage, Web Component, Web worker와 같은 **클라이언트 사이드 Web API를 호스트 객체로 제공하고**, Node.js 환경에서는 Node.js 고유의 API를 호스트 객체로 제공한다.

&nbsp;  

**3. 사용자 정의 객체**

사용자 정의 객체(user-defined objects)는 표준 빌트인 객체와 호스트 객체처럼 기본 제공되는 객체가 아닌 **사용자가 직접 정의한 객체**를 말한다.

&nbsp;  

## 2. 표준 빌트인 객체

* ECMAScript 사양에 정의된 객체를 말한다. 즉, 실행 환경에 관계 없이 언제나 사용할 수 있다.
* 전역 객체의 프로퍼티로서 제공된다.
* 애플리케이션 전역의 공통 기능을 제공한다.
* Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체다.
* 생성자 함수 객체인 표준 빌트인 객체는 프로토타입 메소드와 정적 메소드를 제공한다.
* 생성자 함수 객체가 아닌 표준 빌트인 객체는 정적 메소드만 제공한다.

&nbsp;  

자바스크립트는 Object, String, Number, Boolean, Symbol, Date, Math, RegExp, Array, Map / Set, WeakMap / WeakSet, Function, Promise, Reflect, Proxy, JSON, Error 등 40여개의 [표준 빌트인 객체](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)를 제공한다.

Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체다. 생성자 함수 객체인 표준 빌트인 객체는 프로토타입 메소드와 정적 메소드를 제공하고 생성자 함수 객체가 아닌 표준 빌트인 객체는 정적 메소드만 제공한다.

예를 들어, 표준 빌트인 객체인 String, Number, Boolean, Function, Array, Date는 생성자 함수로 호출하여 인스턴스를 생성할 수 있다.

```javascript
// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('foo'); // String {"foo"}
console.log(typeof strObj); // object

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123); // Number {123}
console.log(typeof numObj); // object

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj = new Boolean(true); // Boolean {true}

// Function 생성자 함수에 의한 Funtion 객체(함수) 생성
const func = new Function('x', 'return x * x'); // f
console.log(typeof func); // function

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3); // [1, 2, 3]
console.log(typeof arr); // object

// Date 생성자 함수에 의한 Date 객체 생성
const date = new Date(); // Fri Jun 05 2020 15:27:25 GMT+0900 (대한민국 표준시) {}

console.log(typeof date); // object
```

&nbsp;  

생성자 함수인 표준 빌트인 객체가 생성한 인스턴스의 프로토타입은 표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체이다. 예를 들어, 표준 빌트인 객체인 String을 생성자 함수로서 호출하여 생성한 String 인스턴스의 프로토타입은 String.prototype이다.

```javascript
const strObj = new String('foo');
console.log(Object.getPrototypeOf(strObj) === String.prototype); // true
```

&nbsp;  

표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체는 다양한 기능의 빌트인 프로토타입 메소드를 제공한다. 또한 표준 빌트인 객체는 인스턴스 없이도 호출 가능한 빌트인 정적 메소드를 제공한다.

예를 들어, 표준 빌트인 객체인 Number의 prototype 프로퍼티에 바인딩된 객체, `Number.prototype`은 다양한 기능의 빌트인 프로토타입 메소드를 제공한다. 이 프로토타입 메소드는 모든 Number 인스턴스가 상속을 통해 사용할 수 있다. 그리고 표준 빌트인 객체인 `Number`는 인스턴스 없이 정적으로 호출할 수 있는 정적 메소드를 제공한다.

```javascript
// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(1.5); // Number {1.5}

// toFixed는 Number.prototype의 프로토타입 메소드다. Number 인스턴스로 호출한다.
console.log(numObj.toFixed()); // 2

// isInteger는 Number의 정적 메소드다. Number 함수 객체로 호출한다.
console.log(Number.isInteger(0.5)); // false
```

&nbsp;  

## 3. 원시 값과 래퍼 객체

* 문자열, 숫자, 불리언 (그리고 심벌) 값에 대해 객체처럼 접근하면 자바스크립트 엔진이 일시적으로 원시 값을 연관된 객체로 변환하는데, 이를 래퍼 객체라 한다.
* 원시 값에 대한 래퍼 객체가 생성되어 프로토타입 체인상에 존재하는 프로퍼티와 메소드를 참조할 수 있다.
* 래퍼 객체로 프로퍼티에 접근하거나 메소드를 호출한 후 다시 원시 값으로 되돌린다.
* null과 undefined는 래퍼 객체를 생성하지 않는다. 따라서 null과 undefined 값을 객체처럼 사용하면 에러가 발생한다.

&nbsp;  

문자열이나 숫자, 불리언 등의 원시 값이 있는데도 String, Number, Boolean 등의 표준 빌트인 생성자 함수가 존재하는 이유는 무엇일까?

다음 예제를 살펴보자. 원시 값은 객체가 아니므로 프로퍼티나 메소드를 가질 수 없는데도 마치 객체처럼 동작한다.

```javascript
const str = 'hello';

console.log(str.length); // 5
console.log(str.toUpperCase()); // HELLO
```

이는 원시 값인 **문자열, 숫자, 불리언** 값에 대해 마치 객체처럼 마침표 표기법(또는 대괄호 표기법)으로 접근하면 **자바스크립트 엔진이 일시적으로 원시 값을 연관된 객체로 변환해 주기 때문이다.** 즉, 원시 값을 객체처럼 사용하면 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성하여 생성된 객체로 프로퍼티에 접근하거나 메소드를 호출하고 **다시 원시 값으로 되돌린다.**

이처럼 <strong>문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체를 래퍼 객체(wrapper object)</strong>라 한다.

예를 들어, 문자열에 대해 마침표 표기법으로 접근하면 그 순간 래퍼 객체인 String 생성자 함수의 인스턴스가 생성되고, 래퍼 객체의 [[StringData]] 내부 슬롯에 문자열이 할당된다.

```javascript
const str = 'hi';

// 원시 타입인 문자열이 래퍼 객체인 String 인스턴스로 변환된다.
console.log(str.length); // 2
console.log(str.toUpperCase()); // HI

// 래퍼 객체로 프로퍼티에 접근하거나 메소드를 호출한 후, 다시 원시값으로 되돌린다.
console.log(typeof str); // string
```

이때 문자열 래퍼 객체인 String 생성자 함수의 인스턴스는 `String.prototype` 메소드를 상속받아 사용할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/83861677-d8d63180-a75b-11ea-81f4-c3e64bbf9499.png" width="60%" />

그 후, 래퍼 객체의 처리가 종료되면 식별자가 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된 원시값을 갖도록 되돌리고 래퍼 객체는 가비지 컬렉션의 대상이 된다. 다음 예제를 살펴보자.

```javascript
// 1. 식별자 str은 문자열을 값으로 가지고 있다.
const str = 'hello';

// 2. 식별자 str은 암묵적으로 생성된 래퍼 객체를 가리킨다.
// 이때 래퍼 객체에 name 프로퍼티가 동적 추가된다.
str.name = 'Kim';

// 3. 식별자 str은 다시 원래의 문자열 값을 가진다.
// 이때 2에서 생성된 래퍼 객체는 아무도 참조하지 않는 상태이므로 가비지 컬렉션의 대상이 된다.
console.log(str); // 'hello'

// 4. 식별자 str은 암묵적으로 생성된 래퍼 객체를 가리킨다.
// 이때 생성된 래퍼 객체는 2에서 생성된 래퍼 객체와 다른 객체이다.
// 따라서 새롭게 생성된 래퍼 객체에는 name 프로퍼티가 존재하지 않는다.
console.log(str.name); // undefined

// 5. 식별자 str은 다시 원래의 문자열 값을 가진다.
// 이때 4에서 생성된 래퍼 객체는 아무도 참조하지 않는 상태이므로 가비지 컬렉션의 대상이 된다.
console.log(str); // 'hello'
```

숫자 값과 불리언 값을 가지는 식별자에 마침표 표기법으로 접근하면 위 예제처럼 래퍼 객체가 생성되어 프로토타입 체인상에 존재하는 프로퍼티와 메소드를 참조할 수 있다.

ES6에서 새롭게 도입된 원시 값인 심벌도 래퍼 객체를 생성한다. 심벌은 일반적인 원시 값과는 달리 리터럴 표기법으로 생성할 수 없고, Symbol 함수를 통해 생성해야 하므로 다른 원시 값과는 차이가 있다.

&nbsp;  

이처럼 문자열, 숫자, 불리언, 심벌은 암묵적으로 생성되는 래퍼 객체에 의해 마치 객체처럼 사용할 수 있으며, 표준 빌트인 객체인 String, Number, Boolean, Symbol의 프로토타입 메소드 또는 프로퍼티를 참조할 수 있다. 따라서 **String, Number, Boolean 생성자 함수를 `new` 연산자와 함께 호출하여 인스턴스를 생성할 필요가 없다.** Symbol은 생성자 함수가 아니므로 이 논의에서 제외한다.

문자열, 숫자, 불리언, 심벌 이외의 원시 값인 null과 undefined는 래퍼 객체를 생성하지 않는다. 따라서 null과 undefined 값을 객체처럼 사용하면 에러가 발생한다.

&nbsp;  

## 4. 전역 객체



























