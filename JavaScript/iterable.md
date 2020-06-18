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

## 2. 빌트인 이터러블

자바스크립트는 이터레이션 프로토콜을 준수한 객체인 빌트인 이터러블을 제공한다. 다음의 표준 빌트인 객체들은 빌트인 이터러블이다.

| 빌트인 이터러블 | 프로퍼티 키가 Symbol.iterator인 메소드                       |
| --------------- | ------------------------------------------------------------ |
| Array           | Array.prototype[Symbol.iterator]                             |
| String          | String.prototype[symbol.iterator]                            |
| Map             | Map.prototype[Symbol.iterator]                               |
| Set             | Set.prototype[Symbol.iterator]                               |
| TypedArray      | TypedArray.prototype[Symbol.iterator]                        |
| arguments       | arguments[Symbol.iterator]                                   |
| DOM 컬렉션      | * NodeList.prototype[Symbol.iterator]<br />* HTMLCollection.prototype[Symbol.iterator] |

&nbsp;  

## 3. for...of 문

for...of 문은 이터러블을 순회하면서 이터러블의 요소를 변수에 할당한다. for...of 문의 문법은 다음과 같다.

```pseudocode
for (변수선언문 of 이터러블) { ... }
```

&nbsp;  

for...of 문은 내부적으로 이터레이터의 next 메소드를 호출하여 이터러블을 순회한다. 이때 next 메소드가 반환한 이터레이터 리절트 객체의 value 프로퍼티 값을 for...of 문의 변수에 할당한다. 그리고 이터레이터 리절트 객체의 done 프로퍼티 값이 false이면 이터러블을 계속 순회하고, true이면 이터러블 순회를 중단한다.

```javascript
for (const item of [1, 2, 3]) {
  console.log(item); // 1 2 3
}
```

&nbsp;  

for...of 문이 내부적으로 동작하는 것을 for 문으로 표현하면 다음과 같다.

```javascript
// 이터러블
const iterable = [1, 2, 3];

//Symbol.iterator 메소드를 호출하여 이터레이터 생성
const iterator = iterable[Symbol.iterator]();

for (;;) {
  // 이터레이터의 next 메소드를 호출하여 이터러블을 순회한다.
  const res = iterator.next();
  
  // next 메소드가 반환한 이터레이터 리절트 객체의 done 프로퍼티가 true가 될 때까지 반복한다.
  if (res.done) break;
  
  console.log(res.value); // 1 2 3
}
```



&nbsp;  

> **for...in 문**
>
> for...of 문은 for...in 문의 형식과 매우 유사하다.

```pseudocode
for (변수선언문 in 객체) { ... }
```

for...in 문은 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 true인 프로퍼티를 순회하며 열거(enumeration)한다. 이때 프로퍼티 키가 심벌인 프로퍼티는 열거하지 않으며 열거 순서를 보장하지 않는다.

&nbsp;  

## 4. 이터러블과 유사 배열 객체

유사 배열 객체(Array-like Object)는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고, length 프로퍼티를 갖는 객체를 말한다. 유사 배열 객체는 length 프로퍼티를 갖기 때문에 for 문으로 순회할 수 있다.

```javascript
// 유사 배열 객체
const arrayLikeObj = {
  0: 1,
  1: 2,
  2: 3,
  length: 3
};

for (let i = 0; i < arrayLikeObj.length; i++) {
  console.log(arrayLikeObj[i]); // 1 2 3
}

// 유사 배열 객체는 Symbol.iterator 메소드가 없기 때문에 for...of 문으로 순회할 수 없다.
for (const item of arrayLikeObj) {
  console.log(item); // 1 2 3
}
// TypeError: arrayLikeObj is not iterable
```

단, arguments, NodeList, HTMLCollection은 유사 배열 객체이면서 이터러블이다. 정확히 말하면 ES6에서 이터러블이 도입되며 유사 배열 객체인 arguments, NodeList, HTMLCollection 객체에 Symbol.iterator 메소드를 구현하여 이터러블이 되었다. 하지만 이터러블이 된 이후에도 length 프로퍼티를 가지며, 인덱스로 접근할 수 있는 것은 변함 없으므로 유사 배열 객체이면서 이터러블인 것이다.

배열도 마찬가지로 ES6에서 이터러블이 도입되며 Symbol.iterator 메소드를 구현하여 이터러블이 되었다.

하지만 모든 유사 배열 객체가 이터러블인 것은 아니다. 위 예제의 `arrayLikeObj` 객체는 유사 배열 객체이지만 이터러블이 아니다. 다만 ES6에서 새롭게 도입된 Array.from 메소드를 사용하면 배열로 간단히 변환할 수 있다.

```javascript
// 유사 배열 객체
const arrayLikeObj = {
  0: 1,
  1: 2,
  2: 3,
  length: 3
};

// Array.from은 유사 배열 객체 또는 이터러블을 배열로 변환한다.
const arr = Array.from(arrayLikeObj);
console.log(arr); // [1, 2, 3]
```

&nbsp;  

## 5. 이터레이션 프로토콜의 필요성

for...of 문, 스프레드 문법, 배열 디스트럭처링 할당 등은 Array, String, Map, Set, TypedArray, DOM 컬렉션, arguments와 같이 다양한 데이터 소스를 사용할 수 있다. 이러한 데이터 소스는 모두 이터레이션 프로토콜을 준수하는 이터러블이다.

**이터러블은** for...of 문, 스프레드 문법, 배열 디스트럭처링 할당과 같은 데이터 소비자(Data consumer)에 의해 사용되므로 **데이터 공급자(Data provider)의 역할을 한다고 할 수 있다**.

**만약 다양한 데이터 공급자가 각자의 순회 방식을 가진다면 데이터 소비자는 다양한 데이터 소스의 순회 방식을 모두 지원해야한다.** 하지만 데이터 소스가 이터레이션 프로토콜을 준수하도록 규정하면, 데이터 소비자는 이터레이션 프로토콜만을 지원하도록 구현하면 된다.

이처럼 이터레이션 프로토콜은 다양한 데이터 소스가 하나의 순회 방식을 갖도록 규정하여 데이터 소비자가 효율적으로 다양한 데이터 소스를 사용할 수 있도록 **데이터 소비자와 데이터 소스를 연결하는 인터페이스의 역할을 한다.**

<img src="https://user-images.githubusercontent.com/32444914/85007226-30ca5a80-b196-11ea-934f-0f8226641acb.png" width="70%" />

&nbsp;  

## 6. 사용자 정의 이터러블

### 6.1. 사용자 정의 이터러블 구현

이터레이션 프로토콜을 준수하지 않는 일반 객체도 이터레이션 프로토콜을 준수하도록 구현하면 사용자 정의 이터러블이 된다. 예를 들어 피보나치 수열(1, 2, 3, 5, 8, 13...)을 구현하는 간단한 사용자 정의 이터러블을 구현해 보자.

```javascript
// 피보나치 수열을 구현한 사용자 정의 이터러블
const fibonacci = {
  // Symbol.iterator 메소드를 구현하여 이터러블 프로토콜을 준수
  [Symbol.iterator]() {
    let [pre, cur] = [0, 1];
    const max = 10; // 수열의 최대값
    
    // Symbol.iterator 메소드는 next 메소드를 소요한 객체(이터레이터)를 반환해야 한다.
    // 이터레이터의 next 메소드는 이터레이터 리절드 객체를 반환해야 한다.
    return {
      next() {
        [pre, cur] = [cur, cur + pre];
        return {
          value: cur,
          done: cur >= max
        };
      }
    };
  }
};

// 이터러블인 fibonacci 객체를 순회할 때마다 next 메소드가 호출된다.
// 이터러블의 최대값을 외부에서 전달할 수 없다.
for (const num of fibonacci) {
  // for ... of 내부에서 break는 가능하다.
  // if (num >= 10) break;
  console.log(num);
}
```

사용자 정의 이터러블은 이터레이션 프로토콜을 준수하도록 Symbol.iterator 메소드를 구현하고, Symbol.iterator 메소드가 next 메소드를 가진 객체(이터레이터)를 반환하도록 한다. 그리고 이터레이터의 next 메소드는 value와 done 프로퍼티를 가지는 이터레이터 리절트 객체를 반환한다. for...of 문은 done 프로퍼티가 true가 될 때까지 반복하며 done 프로퍼티가 true가 되면 반복을 중지한다.

&nbsp;  

이터러블은 for...of 문 뿐만 아니라 스프레드 문법, 배열 디스트럭처링 할당에도 사용할 수 있다.

```javascript
// 이터러블은 스프레드 문법의 대상이 될 수 있다.
const arr = [...fibonacci];
console.log(arr); // [1, 2, 3, 5, 8]

// 이터러블은 배열 디스트럭처링 할당의 대상이 될 수 있다.
const [first, second, ...rest] = fibonacci;
console.log(first, second, rest); // 1 2 [3, 5, 8]
```

&nbsp;  

### 6.2. 이터러블을 생성하는 함수

위에서 살펴본 fibonacci 이터러블은 내부에 수열의 최대값 max를 가지고 있다. 수열의 최대값을 외부에서 전달할 수 있도록 수정해 보자. 수열의 최대값을 인수로 전달받아 이터러블을 반환하는 함수를 만들면 된다.

```javascript
// 피보나치 수열을 구현한 사용자 정의 이터러블을 반환하는 함수
// 수열의 최대값을 인수로 전달받는다.
const fibonacciFunc = max => {
  let [pre, cur] = [0, 1];
  
  // Symbol.iterator 메소드를 구현한 객체(이터러블)를 반환
	return {
    [Symbol.iterator]() {
      // Symbol.iterator 메소드는 객체(이터레이터)를 반환
      return {
        next() {
          [pre, cur] = [cur, pre + cur];
					// 이터레이터는 객체(이터레이터 리절트)를 반환
          return {
            value: cur,
            done: cur >= max
          };
        }
      };
    }
  };
};

console.log([...fibonacci(10)]); // [1, 2, 3, 5, 8]
```

&nbsp;  

### 6.3. 이터러블이면서 이터레이터인 객체를 생성하는 함수

위에서 살펴본 `fibonacciFunc` 함수는 이터러블을 반환한다. 만약 이터레이터를 생성하려면 이터러블의 Symbol.iterator 메소드를 호출해야 한다.

이터러블이면서 이터레이터인 객체를 생성하면 Symbol.iterator 메소드를 호출하지 않아도 된다. 다음 객체는 Symbol.iterator 메소드와 next 메소드를 둘 다 소유한 이터러블이면서 이터레이터이다. Symbol.iterator 메소드는 this를 반환하므로 next 메소드를 갖는 이터레이터를 반환한다.

```javascript
// 이터러블이면서 이터레이터인 객체
{
  [Symbol.iterator]() {
    return this;
  },
  next() {
    return {
      value: any,
      done: boolean
    };
  }
}
```

위에서 살펴본 fibonacciFunc 함수를 이터러블이면서 이터레이터인 객체를 반환하는 함수로 변경해보자.

```javascript
const fibonacciFunc = max => {
  let [pre, cur] = [0, 1];
  
  return {
    [Symbol.iterator]() {
      return this;
    },
    next() {
      [pre, cur] = [cur, pre + cur];
      return {
        value: cur,
        done: cur >= max
      };
    }
  };
};

// iter는 이터러블이면서 이터레이터이다.
let iter = fibonacciFunc(10);

// iter는 이터레이터이다.
console.log(iter.next()); // {value: 1, done: false}
console.log(iter.next()); // {value: 2, done: false}
console.log(iter.next()); // {value: 3, done: false}
console.log(iter.next()); // {value: 5, done: false}
console.log(iter.next()); // {value: 8, done: false}
console.log(iter.next()); // {value: 13, done: true}

iter = fibonacciFunc(10);

// iter는 이터러블이다.
for (const num of iter) {
  console.log(num); // 1 2 3 5 8
}
```

&nbsp;  

### 6.4. 무한 이터러블과 지연 평가

무한 이터러블을 생성하는 함수를 정의해보자. 이를 통해 무한 수열(infinite sequence)을 간단히 구현할 수 있다.

```javascript
const fibonacciFunc = () => {
  let [pre, cur] = [0, 1];

  return {
    [Symbol.iterator]() { 
      return this; 
    },
    next() {
      [pre, cur] = [cur, pre + cur];
      // 무한을 구현해야 하므로 done 프로퍼티를 생략한다.
      return { value: cur };
    }
  };
};

// fibonacciFunc 함수는 무한 이터러블을 생성한다.
for (const num of fibonacciFunc()) {
  if (num > 10000) break;
  console.log(num); // 1 2 3 5 8...
}

// 무한 이터러블에서 3개만을 취득한다.
const [f1, f2, f3] = fibonacciFunc();
console.log(f1, f2, f3); // 1 2 3
```

이터레이션 프로토콜의 필요성에서 살펴보았듯 **이터러블은 데이터 공급자의 역할을 한다.** 배열이나 문자열 등은 모든 데이터를 메모리에 미리 확보한 다음 데이터를 공급한다.

하지만 위 예제의 이터러블은 <strong>지연 평가(Lazy evaluation)</strong>를 통해 값을 생성한다. **지연 평가는 데이터가 필요한 시점 이전까지는 미리 데이터를 생성하지 않다가 데이터가 필요한 시점이 되면 그때야 비로소 데이터를 생성하는 기법이다.** 즉, 평가 결과가 필요할 때까지 평가를 늦추는 기법이 지연 평가이다.

위 예제의 `fibonacciFunc` 함수는 무한 이터러블을 생성한다. 하지만 `fibonacciFunc` 함수가 생성한 무한 이터러블은 **데이터를 공급하는 메커니즘을 구현한 것**으로, 데이터 소비자인 for...of 문이나 배열 디스트럭처링 할당이 실행되기 이전까지 데이터를 생성하지 않는다.

for...of 문의 경우, 이터러블을 순회할 때 내부에서 이터레이터의 next 메소드를 호출하는데 이때 데이터가 생성된다. 즉, 데이터가 필요할 때까지 데이터의 생성을 지연하다가 데이터가 필요한 순간 데이터를 생성한다.

이처럼 지연 평가를 사용하면 불필요한 데이터를 미리 생성하지 않고, 필요한 데이터를 필요한 순간에 생성하므로 보다 빠른 실행 속도를 기대할 수 있고, 불필요한 메모리를 소비하지 않으며 무한도 표현할 수 있다는 장점이 있다.

&nbsp;  

## 출처

* [poiemaweb.com - 이터러블](https://poiemaweb.com/fastcampus/iterable)

