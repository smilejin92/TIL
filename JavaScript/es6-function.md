# ES6 함수의 추가 기능

## 1. 함수의 구분

ES6 이전까지 자바스크립트의 함수는 다른 프로그래밍 언어와는 다르게 별다른 구분없이 다양한 목적으로 사용되었다. 이는 언뜻 보면 편리한 것 같지만 실수를 유발할 수 있으며 성능면에서도 손해이다.

```javascript
var foo = function () {
  return 1;
};

// 1. 일반 함수로서 호출
foo(); // 1

// 2. 생성자 함수로서 호출
new foo(); // foo {}

// 3. 메소드로서 호출
var obj = { a: foo };
obj.a(); // 1
```

이처럼 ES6 이전까지 함수는 사용 목적에 따라 명확히 구분되지 않는다. 다시 말해, ES6 이전의 모든 함수는 callable이며 constructor이다.

> **callabe과 constructor / non-constructor**
>
> 호출할 수 있는 함수 객체를 callable이라 하며, 인스턴스를 생성할 수 있는 함수 객체를 constructor, 인스턴스를 생성할 수 없는 함수 객체를 non-constructor라고 부른다.

```javascript
// foo는 일반 함수이다.
var foo = function () {};

// ES6 이전의 모든 함수는 일반 함수로서 호출할 수 있고, 생성자 함수로서 호출할 수도 있다.
foo(); // undefined
new foo(); // foo {}
```

**주의할 것은 ES6 이전에 일반적으로 메소드라고 부르던 객체에 바인딩된 함수도 callable이며 constructor라는 것이다.** 따라서 객체에 바인딩된 함수도 일반 함수로서 호출할 수 있고, 생성자 함수로서 호출할 수도 있다.

```javascript
// 프로퍼티 f에 바인딩된 것은 constructor이다.
var obj = {
  x: 10,
  f: function () { return this.x; }
};

// 프로퍼티 f에 바인딩된 함수를 메소드로서 호출
obj.f(); // 10

// 프로퍼티 f에 바인딩된 함수를 일반 함수로서 호출
var bar = obj.f;
bar(); // undefined

// 프로퍼티 f에 바인딩된 함수를 생성자 함수로서 호출
new obj.f(); // f {}
```

위 예제와 같이 객체에 바인딩된 함수를 생성자 함수로 호출하는 경우가 흔치 않겠지만, 문법상 가능하다는 것은 문제가 있다. 그리고 이는 성능면에서도 문제가 있다. 객체에 바인딩된 함수가 constructor라는 것은 객체에 바인딩된 함수가 prototype 프로퍼티를 가지며, 프로토타입 객체도 생성한다는 것을 의미하기 때문이다.

함수에 전달되어 보조 함수의 역할 만을 수행하는 콜백 함수도 마찬가지이다. 콜백 함수도 constructor이기 때문에 불필요한 프로토타입 객체를 생성한다.

```javascript
// 콜백 함수를 사용하는 고차 함수 map.
// 콜백 함수도 constructor이며 프로토타입을 생성한다.
[1, 2, 3].map(function (item) {
  return item * 2;
}); // [2, 4, 6]
```

이처럼 **ES6 이전의 모든 함수는 사용 목적에 따라 명확한 구분이 없으므로 호출 방식에 특별한 제약이 없고, 생성자 함수로 호출되지 않아도 프로토타입 객체를 생성한다.** 이는 혼란스러우며 실수를 유발시킬 가능성이 있고 성능에도 좋지 않다.

이러한 문제를 해결하기 위해 **ES6에서는 사용 목적에 따라 함수를 3가지 종류로 명확히 구분하였다.**

| ES6 함수의 구분    | constructor | prototype | super | arguments |
| ------------------ | ----------- | --------- | ----- | --------- |
| 일반 함수(Normal)  | O           | O         | X     | O         |
| 메소드(Method)     | X           | X         | O     | O         |
| 화살표 함수(Arrow) | X           | X         | X     | X         |

일반 함수는 함수 선언문과 함수 표현식으로 정의한 함수를 말하며 ES6 이전의 함수와 차이가 없다. 하지만 ES6의 메소드와 화살표 함수는 ES6 이전의 함수와 명확한 차이가 있다.

## 2. 메소드

**ES6 사양에서 메소드는 메소드 축약 표현으로 정의된 함수 만을 의미한다.**

```javascript
const obj = {
  x: 1,
  // foo는 메소드이다.
  foo() { return this.x; },
  // bar에 바인딩된 함수는 메소드가 아닌 일반 함수이다.
  bar: function() { return this.x; }
};

console.log(obj.foo()); // 1
console.log(obj.bar()); // 1
```

**ES6 사양에서 정의한 메소드는 인스턴스를 생성할 수 없는 non-constructor이다.** 따라서 ES6 메소드는 생성자 함수로서 호출할 수 없다.

```javascript
new obj.foo(); // TypeError: obj.foo is not a constructor
new obj.bar(); // bar  {}
```

**ES6 메소드는 인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고, 프로토타입도 생성하지 않는다.**

```javascript
// obj.foo는 ES6 메소드이므로 prototype 프로퍼티가 없다.
obj.foo.hasOwnProperty('prototype'); // false

// obj.bar는 constructor인 일반 함수이므로 prototype 프로퍼티가 있다.
obj.bar.hasOwnProperty('prototype'); // true
```

참고로 표준 빌트인 객체가 제공하는 프로토타입 메소드와 정적 메소드는 모두 non-contructor이다.

```javascript
String.prototype.toUpperCase.prototype; // undefined
String.fromCharCode.prototype; // undefined

Number.prototype.toFixed.prototype; // undefined
Number.isFinite.prototype; // undefined

Array.prototype.map.prototype; // undefined
Array.from.prototype; // undefined
```

ES6 메소드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다. super 참조는 내부 슬롯 [[HomeObject]]를 갖는 ES6 메소드 만이 super 키워드를 사용할 수 있다.

```javascript
const base = {
  name: 'Kim',
  sayHi() {
    return `Hi! ${this.name}`;
  }
};

const derived = {
  __proto__: base,
  // ES6 메소드는 [[HomeObject]]를 갖는다.
  // sayHi의 [[HomeObject]]는 derived이고
  // super는 sayHi의 [[HomeObject]]의 프로토타입인 base이다.
  sayHi() {
    return `${super.sayHi()}. How are you doing?`;
  }
};

console.log(derived.sayHi()); // Hi! Kim. How are you doing?
```

ES6 메소드가 아닌 함수는 super 키워드를 사용할 수 없다. ES6 메소드가 아닌 함수는 내부 슬롯 [[HomeObject]]를 갖지 않기 때문이다.

```javascript
const derived = {
  __proto__: base,
  sayHi: function () {
    // SyntaxError: 'super' keyword unexpected here
    return `${super.sayHi()}. How are you doing?`;
  }
};
```

이처럼 ES6에서는 메소드 본연의 기능(super)은 추가하고 의미적으로 맞지 않는 기능(constructor)은 제거하였다. 따라서 메소드를 정의할 때, 프로퍼티 값으로 익명 함수 표현식을 할당하는 ES6 이전의 방식은 더이상 사용하지 않는 것이 좋다.

&nbsp;  

## 3. 화살표 함수

































