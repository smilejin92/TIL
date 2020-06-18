# 이터러블

## 1. 이터레이션 프로토콜

이터레이션 프로토콜(iteration protocol)은 **순회 가능한(iterable) 데이터 컬렉션(자료구조)을 만들기 위해 ECMAScript 사양에 정의하여 미리 약속한 규칙**이다.

ES6 이전의 순회 가능한 데이터 컬렉션인 배열, 유사 배열 객체, 문자열 등은 통일된 규약 없이 나름대로의 구조를 가지고 for 문, for...in 문, forEach 등 다양한 방법으로 순회할 수 있었다. **ES6에서는 배열, 유사 배열 객체, 문자열 등 순회 가능한 데이터 컬렉션을 이터레이션 프로토콜을 준수하는 이터러블로 통일하여** for...of 문, 스프레드 문법, 배열 디스트럭처링 할당의 대상으로 사용할 수 있도록 일원화하였다.

ES6에서 도입된 이터레이션 프로토콜에는 **이터러블 프로토콜**과 **이터레이터 프로토콜**이 있다.

&nbsp;  

**이터러블 프로토콜**을 준수한 객체(이터러블)는 아래의 사항을 모두 충족한다.

* Wll-Known Symbol인 Symbol.iterator를 프로퍼티 키로 사용한 메소드를 직접 구현하거나, 프로토타입 체인에 의한 상속을 통해 소유
* Symbol.iterator 메소드를 호출하면 **이터레이터 프로토콜**을 준수한 이터레이터를 반환
* for...of 문으로 순회할 수 있으며 스프레트 분법과 배열 디스트럭처링 할당의 대상이 될 수 있다.

&nbsp;  

**이터레이터 프로토콜**을 준수한 객체(이터레이터)는 아래의 사항을 모두 충족한다. 이터레이터는 이터러블의 요소를 탐색하기 위한 포인터 역할을 한다.

* next 메소드를 소유한다.
* next 메소드는 이터러블을 순회하며 value와 done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다.

&nbsp;  

<img src="https://user-images.githubusercontent.com/32444914/84993170-de803e00-b183-11ea-8186-c08a5a43967c.png" width="70%" />

이터레이션 프로토콜 = 이터러블 프로토콜 + 이터레이터 프로토콜

&nbsp;  

### 1.1. 이터러블

이터러블 프로토콜을 준수한 객체를 이터러블이라 한다. 즉, 이터러블은 Symbol.iterator를 프로퍼티 키로 사용한 메소드를 직접 구현하거나, 프로토타입 체인을 통해 상속받은 객체를 말한다. 예를 들어, 배열은 Array.prototype의 Symbol.iterator 메소드를 상속받는 이터러블이다.

```javascript
const array = [1, 2, 3];

// 배열은 Array.prototype의 Symbol.iterator 메소드를 상속받는 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블인 배열은 for...of 문으로 순회 가능하다.
for (const item of array) {
  console.log(item);
}

// 이터러블인 배열은 스프레드 문법의 대상으로 사용할 수 있다.
console.log(...array); // 1 2 3

// 이터러블인 배열은 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
const [a, ...rest] = array;
console.log(a, rest); // 1, [2, 3]
```

&nbsp;  

Symbol.iterator 메소드를 직접 구현하지 않거나, 상속 받지 않은 일반 객체는 이터러블 프로토콜을 준수한 이터러블이 아니다. 따라서 일반 객체는 for...of 문으로 순회할 수 없으며, 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용할 수 없다.

```javascript
const obj = { a: 1, b: 2 };

// 일반 객체는 Symbol.iterator 메소드를 구현하거나 상속받지 않는다.
// 따라서 일반 객체는 이터러블 프로토콜을 준수한 이터러블이 아니다.
console.log(Symbol.iterator in obj); // false

// 이터러블이 아닌 일반 객체는 for...of 문으로 순회할 수 없다.
for (const item of obj) { // TypeError: obj is not iterable
  console.log(item);
}

// 이터러블이 아닌 일반 객체는 배열 디스트럭처링 할당의 대상으로 사용할 수 없다.
const [a, b] = obj; // TypeError: obj is not iterable
```

하지만 일반 객체도 이터러블 프로토콜을 준수하도록 구현하면 이터러블이 된다.

&nbsp;  

> **스프레드 프로퍼티 제안**
> 2020년 5월 stage 4에 올라온 스프레드 프로퍼티 제안은 일반 객체 스프레드 문법의 사용을 허용한다.
>
> ```javascript
> const obj = { a: 1, b: 2 };
> 
> // 스프레드 프로퍼티 제안은 객체 리터럴 내부에서 스프레드 문법의 사용을 허용한다.
> console.log({ ...obj }); // { a: 1, b: 2 }
> ```

&nbsp;  

### 1.2. 이터레이터

이터러블의 Symbol.iterator 메소드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다. 이터러블의 Symbol.iterator 메소드가 반환한 이터레이터는 next 메소드를 갖는다.

```javascript
// 배열은 이터러블 프로토콜을 준수한 이터러블이다.
const array = [1, 2, 3];

// Symbol.iterator 메소드는 이터레이터를 반환한다.
const iterator = array[Symbol.iterator]();

// 이터레이터 프로토콜을 준수한 이터레이터는 next 메소드를 갖는다.
console.log('next' in iterator); // true
```

이터레이터의 **next 메소드는** 이터러블의 각 요소를 순회하기 위한 포인터 역할을 한다. 즉, next 메소드를 호출하면 이터러블을 순차적으로 한 단계씩 순회하며 순회 결과를 나타내는 **이터레이터 리절트 객체를 반환한다.**

```javascript
// 배열은 이터러블 프로토콜을 준수한 이터러블이다.
const array = [1, 2, 3];

// Symbol.iterator 메소드는 이터레이터를 반환한다.
// 이터레이터는 next 메소드를 가진다.
const iterator = array[Symbol.iterator]();

// next 메소드를 호출하면 이터러블을 순회하며
// 순회 결과를 나타내는 이터레이터 리절트 객체를 반환한다.
// 이터레이터 리절트 객체는 value와 done 프로퍼티를 갖는 객체이다.
console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

이터레이터의 next 메소드가 반환하는 이터레이터 리절트 객체의 value 프로퍼티는 현재 순회 중인 이터러블의 값을 나타내며 done 프로퍼티는 이터러블의 순회 완료 여부를 나타낸다.

&nbsp;  























