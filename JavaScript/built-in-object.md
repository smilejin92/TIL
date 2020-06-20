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

* ECMAScript 사양에 정의된 객체를 말한다. 즉, 실행 환경에 관계 없이 어디서든 사용할 수 있다.
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
* 원시 값에 대한 래퍼 객체는 생성되어 프로토타입 체인상에 존재하는 프로퍼티와 메소드를 참조할 수 있다.
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

문자열, 숫자, 불리언, 심벌 이외의 원시 값인 **null과 undefined는 래퍼 객체를 생성하지 않는다.** 따라서 null과 undefined 값을 객체처럼 사용하면 에러가 발생한다.

&nbsp;  

## 4. 전역 객체

<strong>전역 객체(global object)</strong>는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이며, 어떤 객체에도 속하지 않은 최상위 객체이다.

전역 객체는 자바스크립 환경에 따라 지칭하는 이름이 제각각이다. 브라우저 환경에서는 window(또는 self, this, framse)가 전역 객체를 가리키지만, Node.js 환경에서는 global이 전역 객체를 가리킨다.

&nbsp;  

> **globalThis**
>
> 2020년 5월, 전역 객체를 가리키는 식별자를 globalThis로 통일하는 제안이 stage 4에 올라와 있다. globalThis는 크롬 71, 파이어폭스 65, 사파리 12.1, Edge 79, Node.js 12.0.0 이상에 이미 구현되어 있다.

&nbsp;  

전역 객체는 표준 빌트인 객체(Object, String Number, Function, Array 등), 호스트 객체(클라이언트 web API 또는 Node.js의 호스트 API), `var` 키워드로 선언한 전역 변수 및 전역 함수를 프로퍼티로 갖는다.

전역 객체는 **계층적 구조상 어떤 객체에도 속하지 않은 모든 빌트인 객체(표준 빌트인 객체와 호스트 객체)의 최상위 객체다.** 전역 객체가 최상위 객체라는 것은 **프로토타입 상속 관계상에서 최상위 객체라는 의미가 아니다.** 전역 객체 자신은 어떤 객체의 프로퍼티도 아니며 그저 객체의 계층적 구조상 표준 빌트인 객체와 호스트 객체를 프로퍼티로 소유한다.

&nbsp;  

**전역 객체의 특징**

* 전역 객체는 개발자가 의도적으로 생성할 수 없다. 전역 객체를 생성할 수 있는 생성자 함수가 제공되지 않는다.
* 전역 객체의 프로퍼티를 참조할 때 전역 객체를 가리키는 식별자를 생략할 수 있다.
* 모든 표준 빌트인 객체(Object, String, Number, Boolean 등)를 프로퍼티로 가지고 있다.
* 실행 환경(브라우저 또는 Node.js)에 따라 추가적으로 프로퍼티와 메소드를 가진다 (호스트 객체).
* var 키워드로 선언한 전역 변수와 함수 선언문으로 정의한 전역 함수를 자신의 프로퍼티로 가진다.
* 선언하지 않은 변수에 값을 할당한 암묵적 전역을 자신의 프로퍼티로 가진다. (ex. `x = 100; // window.x = 100;`)
* let이나 const 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. (전역 렉시컬 환경의 선언적 환경 레코드에 따로 존재한다.)
* 브라우저 환경의 모든 자바스크립트 코드는 하나의 전역 객체 window를 공유한다. 어려 개의 script 태그를 통해 자바스크립트 코드를 분리하여도 하나의 전역 객체 window를 공유하는 것은 변함이 없다. 따라서 분리되어 있는 자바스크립트 코드가 하나의 전역을 공유한다는 의미다.

&nbsp;  

전역 객체는 몇 가지 프로퍼티와 메소드를 가지고 있다. 전역 객체의 프로퍼티와 메소드는 전역 객체를 가리키는 식별자를 생략하여 참조 / 호출할 수 있으므로 전역 변수와 전역 함수처럼 사용할 수 있다.

&nbsp;  

### 4.1. 빌트인 전역 프로퍼티

빌트인 전역 프로퍼티(built-in global property)는 **전역 객체의 프로퍼티**를 의미한다. 주로 애플리케이션 전역에서 사용하는 값을 제공한다.

| 전역 프로퍼티 | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| Infinity      | 무한대를 나타내는 숫자값                                     |
| NaN           | 숫자가 아님(Not-a-Number)을 나타내는 숫자값. Number.NaN 프로퍼티와 같다. |
| undefined     | 원시 타입 undefined 값을 가진다.                             |

&nbsp;  

## 4.2. 빌트인 전역 함수

빌트인 전역 함수(built-in global function)는 애플리케이션 전역에서 호출할 수 있는 빌트인 함수로서 **전역 객체의 메소드**이다.

| 전역 함수               | 설명                                                         |
| ----------------------- | ------------------------------------------------------------ |
| eval(code)              | * 자바스크립트 코드를 나타내는 문자열을 인수로 전달 받는다.<br />* 전달받은 문자열 코드가 표현식이라면 런타임에 평가하여 값을 생성한다.<br />* 전달받은 인수가 표현식이 아닌 문이라면 런타임에 실행한다.<br />* 문자열 코드가 여러 개의 문으로 이루어져 있다면 모든 문을 실행한다.<br />* eval 함수는 자신이 호출된 위치에 해당하는 기존의 스코프를 동적으로 수정한다.<br />* strict mode에서 eval함수는 기존의 스코프를 수정하지 않고 자신의 자체적인 스코프를 생성한다.<br />* 인수로 전달받은 문자열 코드가 let, const 키워드를 사용한 변수 선언문이라면 암묵적으로 strict mode가 적용된다(자신의 자체적인 스코프를 생성한다).<br />* eval 함수의 사용은 금지해야 한다. |
| isFinite(value)         | * value가 정상적인 유한수인지 검사하여 true / false를 반환<br />* value의 타입이 숫자가 아니면, 숫자로 타입을 변환한 후 검사를 수행한다. 이때 인수가 NaN으로 평가되는 값이라면 false를 반환한다. |
| isNaN(value)            | * value가 NaN인지 검사하여 true / false를 반환<br />* value의 타입이 숫자가 아니면, 숫자로 타입을 변환한 후 검사를 수행한다. |
| parseFloat(string)      | * 전달받은 문자열 인수를 부동 소수점 숫자(floating point number), 즉 실수로 해석하여 반환한다.<br />* 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.<br />* 문자열의 앞뒤 공백은 무시된다. |
| parseInt(string, radix) | * 전달받은 문자열 인수를 정수(integer)로 해석하여 반환한다.<br />* 전달받은 인수가 문자열이 아니면 문자열로 변환한 후 정수로 해석하여 반환한다.<br />* 두 번째 인수로 진법을 나타내는 기수(raidx, 2 ~ 36)를 전달할 수 있다. 기수를 지정하면 첫 번째 인수로 전달된 문자열을 해당 기수의 숫자로 해석하여 반환한다. 이때 반환 값은 언제나 10진수다.<br />* 기수를 생략하면 첫 번째 인수로 전달된 문자열을 10진수로 해석하여 반환한다. |

&nbsp;  

### 4.3. 암묵적 전역

먼저 다음 예제를 살펴보자.

```javascript
var x = 10; // 전역 별수

function foo() {
  // 선언하지 않은 식별자에 값을 할당
  y = 20; // window.y = 20;
}

foo();

// 선언하지 않은 식별자 y를 전역에서 참조할 수 있다.
console.log(x + y); // 30
```

선언하지 않은 식별자에 값을 할당하면 전역 객체의 프로퍼티가 된다. 이러한 현상을 <strong>암묵적 전역(implicit global)</strong>이라 한다.

위 예제의 `foo` 함수가 호출되면 자바스크립트 엔진은 `y` 변수에 값을 할당하기 위해 먼저 스코프 체인을 통해 선언된 변수인지 확인한다. 이때 `foo` 함수의 스코프와 전역 스코프 어디에서 `y` 변수의 선언을 찾을 수 없으므로 참조 에러가 발생할 것처럼 보이나, 자바스크립트 엔진은 `window.y = 20`으로 해석하여 전역 객체에 프로퍼티를 동적으로 생성한다. 결국 `y`는 전역 객체의 프로퍼티가 되어 마치 전역 변수처럼 동작한다.

&nbsp;  

하지만 `y`는 변수 선언 없이 단지 전역 객체의 프로퍼티로 추가되었을 뿐이다. 따라서 `y`는 변수가 아니다. `y`는 변수가 아니므로 변수 호이스팅이 발생하지 않는다.

```javascript
// 전역 변수 x는 호이스팅이 발생한다.
console.log(x); // undefined

// 전역 변수가 아니라 단지 전역 객체의 프로퍼티인 y는 호이스팅이 발생하지 않는다.
console.log(y); // ReferenceError: y is not defined;

var x = 10;

// 선언하지 않은 식별자에 값을 할당
y = 20; // window.y = 20;
```

&nbsp;  

또한 변수가 아니라 단지 전역 객체의 프로퍼티인 `y`는 `delete` 연산자로 삭제할 수 있다. 하지만 전역 변수는 전역 객체의 프로퍼티이지만, delete 연산자로 삭제할 수 없다.

```javascript
var x = 10; // 전역 변수
y = 20; // window.y = 20;

console.log(window.x); // 10
console.log(window.y); // 20

delete x; // 전역 변수는 삭제되지 않는다.
delete y ; // 프로퍼티는 삭제된다.

console.log(window.x); // 10
console.log(window.y); // undefined
```

&nbsp;  

## 출처

* [poiemaweb.com - 빌트인 객체](https://poiemaweb.com/fastcampus/built-in-object)

