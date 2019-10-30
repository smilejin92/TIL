# Spread 문법

ES6에서 새롭게 도입된 Spread 문법 `...`은 **하나로 뭉쳐 있는 여러 값들의 집합을 펼쳐서(전개, 분산하여, spread) 개별적인 값의 목록으로 만든다.** 

**스프레드 문법을 사용할 수 있는 대상은** Array, String, Map, Set, DOM data structure(NodeList, HTMLCollection), Arguments와 같이 `for..of` 문으로 순회할 수 있는 **이터러블에 한정된다.**

이터러블 특징

* `length` 프로퍼티를 갖고 있다.
* 인덱스로 요소에 접근할 수 있다.

> **이터러블**
>
> 이터러블 프로토콜을 준수한 객체를 이터러블(iterable)이라 한다. 이터러블은 Symbol.iterator를 프로퍼티 키로 갖는 메소드를 직접 구현하거나 프로토타입 체인에 의해 상속한 객체를 말한다.



```javascript
// ...[1, 2, 3]은 [1, 2, 3]을 개별 요소로 분리한다.
console.log(...[1, 2, 3]); // 1 2 3

// 문자열은 이터러블이다.
console.log(...'Hello'); // H e l l o

// Map과 Set은 이터러블이다.
console.log(... new Map([['a', '1'], ['b', '2']])); // ['a', '1'] ['b', '2']
console.log(...new Set([1, 2, 3])); // 1 2 3

// 이터러블이 아닌 일반 객체는 스프레드 문법의 대상이 될 수 없다.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```

위 예제에서 `...[1, 2, 3]`은 이터러블인 배열을 펼쳐서 요소값을 개별적인 값들의 목록 1 2 3으로 만든다. 이때 1 2 3은 **값이 아니라 값들의 목록이다.** 즉, 스프레드 문법의 결과는 값이 아니므로, 스프레드는 연산자라고 부를 수 없으며, 스프레드 문법의 결과를 변수에 할당할 수 없다.

```javascript
const list = ...arr; // SyntaxError: Unexpected token ...
```

이처럼 스프레드 문법의 결과물은 단독으로 사용할 수 없고, 아래와 같이 **쉼표로 구분한 값의 목록을 사용하는 문에서 사용한다.**

* 함수 호출문의 인수 목록
* 배열 리터럴의 요소 목록
* 객체 리터럴의 프로퍼티 목록 (2019년 11월 Stage 4 제안)



## 1. 함수 호출문의 인수 목록에서 사용하는 경우

요소값들의 집합인 배열을 펼쳐서 개별적인 값들의 목록으로 만든 후, 함수의 인수 목록으로 전달해야 하는 경우가 있다.

```javascript
const arr = [1, 2, 3];

// 배열 arr의 요소 중에서 최대값을 구하기 위해 Math.max를 사용한다.
console.log(Math.max(arr)); // NaN
```

위 예제에서 `arr`에 담겨 있는 요소 중 최대 값을 구하기 위해 `Math.max` 메소드의 인수로 `arr`을 전달했지만 `Math.max` 메소드는 숫자를 인수로 받는 메소드이다.

 ```javascript
Math.max(1, 2); // 2
Math.max(1, 2, 3); // 3
Math.max([1, 2, 3]); // NaN
 ```

`Math.max` 메소드는 매개변수 개수를 확정할 수 없는 가변 인자 함수이다. 위와 같이 개수가 정해져 있지 않은 여러 개의 숫자를 인수로 전달 받아 인수 중에서 최대값을 반환한다. 만약 숫자가 아닌 배열을 인수로 전달하면 최대값을 구할 수 없으므로 `NaN`을 반환한다.

이와 같은 문제를 해결하기 위해 배열을 펼쳐서 **요소값들을 개별적인 값들의 목록으로 만든 후** `Math.max` 메소드의 인수로 전달해야한다. 스프레드 문법이 제공되기 이전에는 배열을 펼쳐서 요소값의 목록을 인수로 함수의 인수로 전달하고 싶은 경우 `Function.porototype.apply`를 사용하였다.

```javascript
var arr = [1, 2, 3];

// apply 함수의 두 번째 인수는 apply 함수가 호출하는 함수의 인수 목록이다.
// 따라서 배열이 펼쳐져서 인수로 전달되는 효과가 있다.
var maxVal = Math.max.apply(null, arr);

console.log(maxVal); // 3
```



스프레드 문법을  사용하면 보다 간결하고 가독성이 좋다.

```javascript
const arr = [1, 2, 3];

// 스프레드 문법을 사용하여 배열 arr의 요소를
// 값의 목록으로 펼쳐서 Math.max에 전달한다.
// Math.max(...[1, 2, 3])은 Math.max(1, 2, 3)과 같다.
const maxVal = Math.max(...arr);

console.log(maxVal); //3
```



#### Spread 문법 vs. Rest 파라미터

스프레드 문법은 Rest 파라미터와 형태가 동일하여 혼동할 수 있으므로 주의해야 한다.

| Spread 문법                                          | Rest 파라미터                                                |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| 이터러블을 **펼쳐서** 개별적인 값들의 목록을 만든다. | 함수에 전달된 인수들의 목록을 배열로 **묶어서** 전달 받는다. |

```javascript
// Spread 문법
// 배열 arr의 요소를 값의 목록으로 풀어서 Math.max의 인수로 전달한다.
const arr = [1, 2, 3];
const arrMax = Math.max(...arr); // Math.max(1, 2, 3)
console.log(arrMax); // 3

// Rest 파라미터
// 첫번째 매개변수 자리에 1이 전달되고 나머지 매개변수는 배열에 묶여서 전달된다.
function addAll(x, ...rest) {
  console.log(x); // 1
  console.log(rest); // [2, 3]
  ...
}

addAll(1, 2, 3); // addAll(...arr);
```





## 2. 배열 리터럴 내부에서 사용하는 경우

스프레드 문법은 **하나로 뭉쳐 있는 여러 값들의 집합을 펼쳐서 개별적인 값의 목록으로 만든다.**  따라서 **배열**을 사용할 때에 유용하게 쓰인다.



### 2.1 `concat`

```javascript
// ES5
var arr = [1, 2].concat([3, 4]);
console.log(arr); // [1, 2, 3, 4]

// ES6
const arr = [...[1, 2], ...[3, 4]];
console.log(arr); // [1, 2, 3, 4]
```



### 2.2 `push`

```javascript
// ES5
var arr1 = [1, 2];
var arr2 = [3, 4];

Array.prototype.push.apply(arr1, arr2);

console.log(arr1); // [1, 2, 3, 4]

// ES6
const arr1 = [1, 2];
const arr2 = [3, 4];

arr1.push(...arr2); // arr1.push(3, 4)

console.log(arr1); // [1, 2, 3, 4]
```



### 2.3 `splice`

```javascript
// Array.prototype.splice(start, deleteCount, items);
// start: 원본 배열의 요소를 제가하기 시작할 인덱스.
// deleteCount: start 인덱스부터 제가할 요소의 개수 (option)
// items: 제거한 위치에 삽인될 요소들의 목록 (option)

// ES5
var arr1 = [1, 4];
var arr2 = [2, 3];

// apply 메소드의 두 번째 인수는 배열이다. 이것은 인수 목록으로 splice 메소드에 전달된다.
// [1, 0].concat(arr2) -> [1, 0, 2, 3]
// arr1.splice(1, 0, 2, 3) -> arr1[1]부터 0개의 요소를 제거하고
// 그 자리(arr[1])에 새로운 요소 (2, 3)을 삽입한다.
Array.prototype.splice.apply(arr1, [1, 0].concat(arr2));

console.log(arr1); // [1, 2, 3, 4]

// ES6
const arr1 = [1, 4];
const arr2 = [2, 3];

arr1.splice(1, 0, ...arr2);

console.log(arr1); // [1, 2, 3, 4]
```



### 2.4 배열 복사

```javascript
// ES5
var origin = [1, 2];
var copy = origin.slice(); // 얕은 복사 (shallow copy)

console.log(copy); // [1, 2]
console.log(copy === origin); // false

// ES6
const origin = [1, 2];
const copy = [...origin]; // 얕은 복사 (shallow copy)

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```



### 2.5 유사 배열 객체를 배열로 변환

유사 배열 객체(Array-like object)를 배열로 변환하려면 `slice` 메소드를 `apply` 함수로 호출하는 것이 일반적이다.

```javascript
// ES5
function sum() {
  // 유사 배열 객체인 arguments를 배열로 변환
  // args = {'0': 1, '1': 2, '2': 3, length: 3}.slice()를 apply로
  var args = Array.prototype.slice.apply(arguments);
  
  return args.reduce(function (pre, cur) {
    return pre + cur;
  }, 0);
}

console.log(sum(1, 2, 3)); // 6

// ES6
function sum() {
  // 유사 배열 객체인 arguments를 배열로 변환
  const args = [...arguments];
    
  return args.reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2, 3, 4)); // 6
```



## 3. 객체 리터럴 내부에서 사용하는 경우 (TC39 - stage 4)

객체 리터럴의 프로퍼티 목록에서 스프레드 문법을 사용할 수 있는 스프레드 프로퍼티는 Rest 프로퍼티와 함께 2019년 11월 TC39 프로세스의 stage 4(Finished) 단계에 제안되어 있다.

스프레드 문법의 대상은 이터러블이어야 하지만 **스프레드 프로퍼티 제안은 일반 객체를 대상으로도 스프레드 문법의 사용을 허용한다.**

```javascript
// 스프레드 프로퍼티 - 객체를 풀어버린다
const obj = { a: 1, b: 2, ...{ c: 3, d: 4 } };
console.log(obj); // { a: 1, b: 2, c: 3, d: 4 }
```



스프레드 프로퍼티가 도입되기 이전에는 ES6에서 도입된 `Object.assign` 메소드를 사용하여 여러 개의 객체를 병합하거나 특정 프로퍼티를 변경/추가하였다.

```javascript
// 객체의 병합
// 프로퍼티가 중복되는 경우 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = Object.assign({}, { x: 1, y: 2 }, { y: 10, z: 3 });
console.log(merged); // { x: 1, y: 10, z: 3 }

// 특정 프로퍼티 변경
let obj = { x: 1, y: 2 };
obj = Object.assign(obj, { y: 100 });
console.log(obj); // { x: 1, y: 100 };

// 프로퍼티 추가
let obj2 = { x: 1, y: 2 };
obj2 = Object.assign(obj2, { z: 0 });
console.log(obj2); // { x: 1, y: 2, z: 0 }
```



스프레드 프로퍼티는 `Object.assign` 메소드를 대체할 수 있는 간편한 문법이다.

```javascript
// 객체의 병합
// 프로퍼티가 중복되는 경우 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = { ...{ x: 1, y: 2 }, ...{ y: 10, z: 3 } };
console.log(merged); // { x: 1, y: 10, z: 3 }

// 특정 프로퍼티 변경
let obj = { x: 1, y: 2 };
obj = { ...obj, y: 100 };
console.log(obj); // { x: 1, y: 100 };

// 프로퍼티 추가
let obj2 = { x: 1, y: 2 };
obj2 = { ...obj2, z: 0 };
console.log(obj2); // { x: 1, y: 2, z: 0 }
```

