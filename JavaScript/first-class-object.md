# 함수와 일급 객체

## 1. 일급 객체

* 아래와 같은 조건을 만족하는 객체를 일급 객체(first-class object)라 한다.
  * 무명의 리터럴로 생성할 수 있다(런타임에 생성이 가능하다).
  * 변수나 자료 구조(객체, 배열 등)에 저장할 수 있다.
  * 함수의 매개 변수에게 전달할 수 있다.
  * 함수의 결과값으로 반환할 수 있다.
* 자바스크립트의 함수는 일급 객체이다.
* 일급 객체로서 함수가 가지는 가장 큰 장점은 값으로 평가될 수 있다는 것이다(함수형 프로그래밍).
* 함수 객체와 일반 객체에는 차이가 있다.
  * 함수는 호출할 수 있다.
  * 함수 객체만 가지는 고유한 프로퍼티가 있다.

&nbsp;  

자바스크립트의 함수는 위의 조건을 모두 만족하므로 일급 객체이다. 일급 객체로서 함수가 가지는 가장 큰 특징은 값으로 평가될 수 있다는 것이다. 이는 함수형 프로그래밍을 가능케하는 자바스크립트의 장점 중에 하나이다.

```javascript
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수 있다.
const increase = function (count) {
  return ++count;
};

const decrease = function (count) {
  return --count;
};

// 2. 함수는 자료 구조(객체)에 저장할 수 있다.
const predicates = {
  increase,
  decrease
};

// 3. 함수는 매개 변수에게 전달될 수 있다.
// 4. 함수는 결과값으로 반환될 수 있다.
function makeCounter(predicate) {
  let num = 0;
  
  return function () {
    num = predicate(num);
    return num;
  };
}

// 3. 함수는 매개 변수에게 전달될 수 있다.
const increaser = makeCounter(predicates.increase);
console.log(increaser()); // 1
```

1. 함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미다.
2. 객체는 값이므로 함수는 값과 동일하게 취급할 수 있다.
3. 따라서 함수는 값을 사용할 수 있는 곳이라면 리터럴로 정의할 수 있으며 런타임에 함수 객체로 평가된다.

&nbsp;  

**함수는 객체이지만 일반 객체와는 차이가 있다.** 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있다. 그리고 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.

(무명 함수 리터럴은 반드시 할당해야한다. 유명 함수 리터럴은 함수 선언문으로 해석될 수 있다.)

(함수면 [[Call]] 내부 슬롯이 무조건 있지만, 모든 함수가 [[Construct]] 내부 슬롯을 가지진 않는다.)

&nbsp;  

## 2. 함수 객체의 프로퍼티

* 함수 객체만이 가지는 고유한(own property) 프로퍼티가 있다.
  * arguments: **함수 호출시 전달된 인수(arguments)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체(array-like object)이며, 함수 내부에서 지역 변수처럼 사용된다.**
  * caller: 자신을 호출한 함수(비표준)
  * length: 함수 정의시 선언한 매개변수의 수
  * name: 함수 이름
  * prototype: 생성자 함수로 호출될 때, 생성할 인스턴스의 프로토타입 객체를 가리킨다.

&nbsp;  

함수는 객체이다. 따라서 함수도 프로퍼티를 가질 수 있다. 브라우저 콘솔에서 `console.dir` 메소드를 사용하여 함수 객체의 내부를 들여다 보면 아래와 같이 출력된다.

<img src="https://user-images.githubusercontent.com/32444914/81144671-86b0bd80-8faf-11ea-8afa-ff613db1ae9b.png" width="80%" />

일반 객체에는 없는 `arguments`, `caller`, `length`, `name`, `prototype` 프로퍼티가 함수 객체에는 존재한다. square 함수의 모든 프로퍼티의 프로퍼티 어트리뷰트를 `Object.getOwnPropertyDescriptors` 메소드로 확인해 보면 아래와 같다.

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

* 함수 객체의 arguments 프로퍼티 값은 arguments 객체이다.
* arguments 객체는 함수 호출시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다.
* arguments 객체는 인수를 프로퍼티 값으로 소유하며, 프로퍼티 키는 인수의 순서를 나타낸다.
* arguments 객체의 callee 프로퍼티는 arguments 객체를 생성한 함수를 가리킨다.
* arguments 객체의 length 프로퍼티는 함수 호출시 전달된 인수의 수를 나타낸다.
* arguments 객체의 Symbol(Symbol.iterator) 프로퍼티는 arguments 객체를 이터러블로 만드는 프로퍼티이다.
* arguments 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하게 사용된다.
* arguments 객체는 유사 배열 객체(ES5)이며 이터러블(ES6)이다.
* rest 파라미터(ES6)를 사용하여 전달된 인수를 배열로 관리할 수 있다.

&nbsp;  

함수 객체의 arguments 프로퍼티 값은 **arguments 객체**이다. arguments 객체는 **함수 호출시 전달된 인수(arguments)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체(array-like object)이며 함수 내부에서 지역 변수처럼 사용된다.** 함수 외부에서는 참조할 수 없다.

> **arguments 프로퍼티**
>
> 함수 객체의 arguments 프로퍼티는 현재 일부 브라우저에서 지원하고 있지만, ES5부터 표준에서 폐지(deprecated)되었다. 따라서 Function.arguments와 같은 사용 방법은 권장되지 않으며 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체를 참조하도록 한다.

&nbsp;  

```javascript
function multiply(x, y) {
  console.log(arguments);
  return x * y;
}

console.log(multiply()); // NaN
console.log(multiply(1)); // NaN
console.log(multiply(1, 2)); // 2
console.log(multiply(1, 2, 3)); // 2
```

자바스크립트 함수 호출의 특징은 아래와 같다.

* 매개변수와 인수의 개수가 일치하는지 확인하지 않는다.
* 함수 호출시 매개변수 개수만큼 인수를 전달하지 않아도 에러가 발생하지 않는다.
* 함수 호출시 전달된 인수가 함수 매개 변수의 수보다 적을 경우, 인수를 전달 받지 못한 매개변수는 undefined로 초기화된 상태를 유지한다.
* 매개변수의 개수보다 인수를 더 많이 전달한 경우 초과된 인수는 무시된다(arguments 객체의 프로퍼티로 보관된다).

&nbsp;  

위 예제를 브라우저 콘솔에서 실행하면 아래와 같은 결과가 나온다.

<img src="https://user-images.githubusercontent.com/32444914/81642981-9886da80-945f-11ea-86a8-2e7d07823ed3.png" width="80%" />

* arguments 객체는 인수를 프로퍼티 값으로 소유하며, 프로퍼티 키는 인수의 순서를 나타낸다.
* arguments 객체의 callee 프로퍼티는 호출되어 arguments 객체를 생성한 함수를 기리킨다.
* arguments 객체의 length 프로퍼티는 인수의 개수를 가리킨다.
* arguments 객체의 Symbol(Symbol.iterator) 프로퍼티는 arguments 객체를 이터러블로 만들기 위한 프로퍼티이다.

&nbsp;  

**arguments 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하게 사용된다.**

```javascript
function sum() {
  let res = 0;
  
  // arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for 문으로 순회할 수 있다.
  for (let i = 0; i < arguments.length; i++) {
    res += arguments[i];
  }
  return res;
}

console.log(sum()); // 0
console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3)); // 6
```

arguments 객체는 배열의 형태로 인자 정보를 담고 있지만 실제 배열이 아닌 유사 배열 객체(array-like object)이다. 유사 배열 객체란 length 프로퍼티를 가진 객체로 for 문으로 순회할 수 있는 객체를 말한다.

> **유사 배열 객체와 이터러블**
>
> ES6에서 도입된 이터레이션 프로토콜을 준수하면 순회 가능한 자료 구조인 이터러블이 된다. 이터러블의 개념이 없었던 ES5에서 arguments 객체는 유사 배열 객체로 구분되었다. 하지만 **이터러블이 도입된 ES6부터 arguments 객체는 유사 배열 객체이면서 동시에 이터러블이다.**

&nbsp;  

유사 배열 객체인 arguments를 순회하여 가변 인자 함수를 구현할 수 있지만, 이러한 번거로움을 해결하기 위해 ES6에서는 Rest 파마리터를 도입했다.

```javascript
// ES6 Rest parameter
function sum(...args) {
  console.log(args); // [1, 2, 3, 4, 5] 배열로 인수를 보관한다.
  return args.reduce((pre, cur) => pre + cur, 0); // 따라서 배열 메소드를 사용할 수 있다.
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

&nbsp;  

### 2.2. caller 프로퍼티

함수 객체의 caller 프로퍼티는 함수 자신을 호출한 함수를 가리킨다. caller 프로퍼티는 ECMAScript 스펙에 포함되지 않은 비표준 프로퍼티이다.

&nbsp;  

### 2.3. length 프로퍼티

함수 객체의 length 프로퍼티는 **함수 정의 시 선언한 매개변수의 개수**를 가리킨다. arguments 객체의 length 프로퍼티는 인자(argument)의 개수를 가리킨다. 

&nbsp;  

### 2.4. name 프로퍼티

함수 객체의 name 프로퍼티는 함수 이름을 나타낸다. name 프로퍼티는 ES6 이전까지는 비표준이었지만, ES6에서 정식 표준이 되었다.

주의해야 할 것은 name 프로퍼티의 값이 ES5와 ES6에서 다르다는 것이다. **익명 함수 표현식의 경우, ES5에서 name 프로퍼티는 빈 문자열을 값으로 가진다. 하지만 ES6에서는 함수 객체를 가리키는 식별자를 값으로 가진다.**

```javascript
// 익명 함수 표현식
var anonymousFunc = function() {};
// ES5: anonymousFunc.name = '';
// ES6: anonymousFunc.name = anonymousFunc
```

&nbsp;  

### 2.5. prototype 프로퍼티

prototype 프로퍼티는 함수 객체만이 소유하는 프로퍼티이다. 일반 객체에는 prototype 프로퍼티가 없다.

```javascript
// 함수 객체는 prototype 프로퍼티를 소유한다.
const foo = function () {};
console.log(foo.hasOwnProperty('prototype')); // true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
const obj = {};
console.log(obj.hasOwnProperty('prototype')); // false
```

prototype 프로퍼티는 함수가 객체를 생성하는 생성자 함수로 사용될 때, 생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가리킨다.

&nbsp;  

## 참고 자료

* [poiemaweb.com - 일급 객체](https://poiemaweb.com/fastcampus/first-class-object)

