# 프로퍼티 정의

## 1. 프로퍼티 정의란?

프로퍼티 정의란 **프로퍼티 어트리뷰트의 값을 정의하여 프로퍼티의 상태를 관리하는 것을 말한다.** 예를 들어 프로퍼티 값을 **갱신** 가능하도록 할 것인지 (ex. `setX()`, `setY()`), 프로퍼티를 **열거** 가능하도록 할 것인지 (ex. `getX()`), 프로퍼티를 **재정의** 가능하도록 할 것인지 정의할 수 있다. 이를 통해 객체의 프로퍼티가 어떻게 동작해야 하는지를 명확히 정의할 수 있다.

**자바스크립트 엔진은 프로퍼티를 생성(객체 리터럴의 평가 혹은 프로퍼티 동적 생성)할 때, 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.**

```javascript
const obj = {};

// obj의 프로퍼티를 동적 생성
obj.prop = 10;

// 정의된 프로퍼티 어트리뷰트는 Object.getOwnPropertyDescriptor 메소드로 확인 가능
// 객체 obj의 'prop'의 프로퍼티 디스크립터를 descriptor에 저장
const descriptor = Object.getOwnPropertyDescriptor(obj, 'prop');
console.log(descriptor);
// {value: 10, writable: true, enumerable: true, configurable: true} - 기본값
```

위의 예제에서 `obj.prop = 10`은 `obj`에 존재하지 않는 프로퍼티를 동적으로 생성하여 값을 할당하는 것이고, 프로퍼티 정의는 프로퍼티 어트리뷰트를 정의하는 것이다. **프로퍼티 어트리뷰트는 프로퍼티의 상태를 나타낸다. 프로퍼티 상태는** 프로퍼티의 **값(value)**, **값의 갱신 가능 여부(writable)**, **열거 가능 여부(enumerable)**, **재정의 가능 여부(configurable)**를 말한다.

프로퍼티 어트리뷰트는 `Object.getOwnPropertyDescriptor` 메소드를 사용해 참조할 수 있다. 인수는 객체의 참조와 데이터 프로퍼티의 키를 문자열로 전달한다. 인수로 전달한 데이터 프로퍼티 키가 해당 객체에 존재한다면, **프로퍼티 디스크립터**를 반환한다. 존재하지 않는 프로퍼티나 상속받은 프로퍼티에 대해서는 `undefined`를 반환한다.

```javascript
const obj = {};
const descriptor = Object.getOwnPropertyDescriptor(obj, 'prop');
console.log(descriptor); // undefined;
```



## 2. 내부슬롯/메소드

내부 슬롯(Internal Slot)과 내부 메소드(Internal method)는 ECMAScript 스펙에서 요구하는 객체와 관련된 내부 상태와 내부 동작을 정의한 것이다. 다시 말해, 내부 슬롯과 내부 메소드는 자바스크립트 엔진이 코드를 실행하는 알고리즘을 설명하기 위해 ECMAScript 스펙에서 사용하는 **의사 프로퍼티(Pseudo property)와 의사 메소드(Pseudo method)이다.** ECMAScript 스펙에 등장하는 이중 대괄호([[..]])로 감싼 이름들이 내부 슬롯과 내부 메소드이다. 슬롯은 상태 (value)를 나타내고 메소드는 알고리즘(behavior)을 설명한다.

![](./images/internal-method.png)

내부 슬롯과 내부 메소드는 자바스크립트 엔진의 내부 구현 사양을 정의한 것으로 자바스크립트 엔진은 ECMAScript 스펙에서 정의한 내부 슬롯과 내부 메소드의 사양을 만족시키는 것이 요구될 뿐, 이를 외부로 노출시키지는 않는다.

(즉, 내부 슬롯과 내부 메소드는 **객체의 프로퍼티가 아니다.** 따라서 내부 슬롯과 내부 메소드는 직접적으로 접근하거나 호출할 수 있는 방법을 원칙적으로 제공하지 않는다. 단, 일부 내부 슬롯과 내부 메소드에 **간접적으로 접근할 수 있는 수단은 있다.**)



## 3. 접근자 프로퍼티

프로퍼티는 **데이터 프로퍼티**와 **접근자 프로퍼티**로 구분할 수 있다.

* 데이터 프로퍼티(Data property) - 키와 값으로 구성된 일반적인 프로퍼티
* 접근자 프로퍼티(Accessor property) - 자체적으로는 값을 갖지 않고, 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(Accessor function)로 구성된 프로퍼티

접근자 함수는 **getter / setter** 함수라고도 부른다. 접근자 프로퍼티는 getter와 setter 함수를 모두 정의할 수도 있고 하나만 정의할 수도 있다.

```javascript
const person = {
  // 데이터 프로퍼티
  firstName: 'Jinhyun',
  lastName: 'Kim',
  
  // fullName은 접근자 함수로 구성된 접근자 프로퍼티이다.
  // getter 함수
  get fullName() {
    return this.firstName + ' ' + this.lastName;
  },
  // setter 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
};

// 데이터 프로퍼티를 동한 프로퍼티 값의 참조
console.log(person.firstName + ' ' + person.lastName); // Jinhyun Kim

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = 'Jin Kim';
console.log(person);
// { firstName: 'Jin', lastName: 'Kim', fullName: [Getter/Setter] }

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // Jin Kim

// firstName은 데이터 프로퍼티이다.
// 데이터 프로퍼티는 value, writable, enumerable, configurable 프로퍼티 어트리뷰트를 갖는다.
let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log(descriptor);
// { value: 'Jin', writable: true, enumerable: true, configurable: true }

// fullName은 접근자 프로퍼티이다.
// 접근자 프로퍼티는 get, set, enumerable, configurable 프로퍼티 어트리뷰트를 갖는다.
descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log(descriptor);
// {
//   get: [Function: get fullName],
//   set: [Function: set fullName],
//   enumerable: true,
//   configurable: true
// }
```

메소드 앞에 `get`, `set`이 붙은 메소드가 getter와 setter 함수이고 getter/setter 함수의 이름 `fullName`이 접근자 프로퍼티이다. 접근자 프로퍼티는 자체적으로 값(value, 프로퍼티 어트리뷰트 - **???? 왜 안가짐**)을 가지지 않으며, 다만 데이터 프로퍼티의 값을 읽거나 저장할 때 관여할 뿐이다.

이를 내부 슬록 / 메소드 관점에서 설명하면 다음과 같다. 접근자 프로퍼티 `fullName`으로 프로퍼티 값에 접근하면 내부적으로 [[Get]] 내부 메소드가 호줄되어 아래와 같이 동작한다.

1. 프로퍼티 키가 유효한지 확인한다. 프로퍼티 키 'fullName'은 문자열이므로 유효한 프로퍼티 키이다.
2. 프로토타입 체인에서 해당 프로퍼티를 검색한다. `person` 객체에 `fullName` 프로퍼티가 존재한다.
3. 검색된 `fullName` 프로퍼티가 데이터 프로퍼티인지 접근자 프로퍼티인지 확인한다. `fullName` 프로퍼티는 접근자 프로퍼티이다.
4. 접근자 프로퍼티 `fullName`의 프로퍼티 어트리뷰트 [[Get]]의 값, getter 함수를 호출하여 그 결과를 반환한다. 프로퍼티 `fullName`의 프로퍼티 어트리뷰트 [[Get]]의 값은 `Object.getOwnPropertyDescriptor` 메소드가 반환하는 **프로퍼티 디스크립터(PropertyDescriptor) 객체의 get 프로퍼티 값과 같다.**



접근자 프로퍼티와 데이터 프로퍼티 구별 방법

```javascript
// 일반 객체의 __proto__는 접근자 프로퍼티이다.
Object.getOwnPropertyDescriptor(Object.prototype, '__proto__');
// {
//   get: [Function: get __proto__],
//   set: [Function: set __proto__],
//   enumerable: false,
//   configurable: true
// }

// 함수 객체의 prototype의 데이터 프로퍼티이다.
Object.getOwnPropertyDescriptor(function() {}, 'prototype');
// { value: {}, writable: true, enumerable: false, configurable: false }

```



## 4. 프로퍼티 어트리뷰트

