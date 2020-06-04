# 배열

## 1. 배열이란?

* 배열은 여러 개의 값을 **순차적**으로 나열한 자료 구조이다.
* 배열이 가지고 있는 값을 **요소**라고 부른다. 자바스크립트의 모든 값은 배열의 요소가 될 수 있다.
* 배열의 요소는 배열에서 자신의 **위치**를 나타내는 0 이상의 정수인 **인덱스**를 가진다. 인덱스는 배열의 요소에 접근할 때 사용한다.
* 배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 가진다.
* 배열의 인덱스와 length 프로퍼티를 사용하여 for 문으로 배열의 요소에 **순차적으로 접근**할 수 있다.
* 자바스크립트의 배열은 **객체 타입**이다.
* 일반 객체와 배열을 구분하는 가장 명확한 차이는 **값의 순서**와 **length 프로퍼티**이다.

&nbsp;  

배열(array)은 여러 개의 값을 순차적으로 나열한 자료 구조이다. 배열은 사용 빈도가 매우 높은 가장 기본적인 자료 구조이다.

```javascript
const arr = ['apple', 'banana', 'orange'];
```

&nbsp;  

배열이 가지고 있는 값을 <strong>요소(element)</strong>라고 부른다. **자바스크립트의 모든 값은 배열의 요소가 될 수 있다.**

배열의 요소는 배열에서 **자신의 위치**를 나타내는 0 이상의 정수인 <strong>인덱스(index)</strong>를 갖는다. 인덱스는 배열의 요소에 접근할 때 사용한다. 대부분의 프로그래밍 언어에서 인덱스는 0부터 시작한다.

배열의 요소에 접근할 때는 대괄호 표기법을 사용한다. 대괄호 내에는 접근하고 싶은 요소의 인덱스를 지정한다.

```javascript
arr[0] // apple
arr[1] // banana
arr[2] // orange
```

&nbsp;  

배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 갖는다.

```javascript
arr.length // 3
```

&nbsp;  

배열은 인덱스와 **length 프로퍼티**를 갖기 때문에 for 문을 통해 **순차적으로 값에 접근**할 수 있다.

```javascript
// 배열의 순회
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

&nbsp;  

자바스크립트에 배열이라는 타입은 존재하지 않는다. **배열은 객체 타입이다.**

```javascript
typeof arr // object
```

&nbsp;  

배열은 배열 리터럴 또는 Array 생성자 함수로 생성할 수 있다. 두 경우 모두 배열의 생성자 함수는 Array이며 배열의 프로토타입 객체는 Array.prototype이다. Array.prototype은 배열을 위한 빌트인 메소드를 제공한다.

```javascript
const arr = [1, 2, 3];

arr.constructor === Array // true
Object.getPrototypeOf(arr) === Array.prototype // true
```

&nbsp;  

배열은 객체이지만 **일반 객체와는 구별되는 독특한 특징이 있다.**

| 구분            | 객체                      | 배열          |
| --------------- | ------------------------- | ------------- |
| 구조            | 프로퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
| 값의 참조       | 프로퍼티 키               | 인덱스        |
| 값의 순서       | X                         | O             |
| length 프로퍼티 | X                         | O             |

일반 객체와 배열을 구분하는 가장 명확한 차이는 **값의 순서**와 **length 프로퍼티**이다. 값의 순서(인덱스)와 length 프로퍼티를 갖는 배열은 반복문을 통해 순차적으로 값에 접근하기 적합한 자료 구조이다.

```javascript
const arr = [1, 2, 3];

// 반복문으로 자료 구조를 순회하기 위해서는 자료 구조의 길이를 알아야 한다.
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

배열의 장점은 처음부터 순차적으로 요소에 접근할 수 있고, 역순으로 요소에 접근할 수 도 있으며 특정 위치부터 순차적으로 요소에 접근할 수도 있다는 것이다. 이는 배열이 인덱스(값의 순서)와 length 프로퍼티를 갖기 때문에 가능한 것이다.

&nbsp;  

## 2. 자바스크립트 배열은 배열이 아니다.

* 일반적으로 배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료 구조를 말한다.
* 배열의 요소가 **하나의 타입**으로 통일되어 있으며, 서로 **연속적으로 인접**해 있는 배열을 **밀집 배열**이라 한다.
* 자바스크립트 배열의 요소를 위한 메모리 공간은 동일한 크기를 갖지 않을 수 있으며, 연속적으로 이어져 있지 않을 수도 있다.
* 배열의 요소가 연속적으로 이어져 있지 않는 배열을 **희소 배열**이라 한다.
* 자바스크립트의 배열은 일반적인 배열의 동작을 흉내낸 특수한 객체이다.
* 자바스크립트 배열은 **인덱스를 프로퍼티 키로 가지며, length 프로퍼티를 가진 특수한 객체**이다.
* 자바스크립트 배열의 **요소는 사실 프로퍼티 값**이다.
* 자바스크립트 배열은 **해시 테이블**로 구현된 객체이므로, 일반 배열보다 인덱스로 **배열 요소에 접근하는 속도가 느리다.**
* 자바스크립트 배열은 **해시 테이블**로 구현된 객체이므로, 일반 배열보다 **요소 추가/삭제/검색이 빠르다.**
* 대부분의 모던 자바스크립트 엔진은 배열을 일반 객체와 구별하여 보다 배열처럼 동작하도록 최적화하여 구현하였다.

&nbsp;  

일반적으로 배열이라는 자료 구조의 개념은 **동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료 구조**를 말한다. 즉, 배열의 요소는 **하나의 타입**으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열은 <strong>밀집 배열(dense array)</strong>이라 한다.

<img src="https://user-images.githubusercontent.com/32444914/82526770-bf37c600-9b6f-11ea-974a-9bc12ed42164.png" width="60%" />

이처럼 자료 구조(data structure)에서 말하는 배열의 경우, 각 요소는 동일한 크기를 가지며 빈틈없이 연속적으로 이어져 있으므로 인덱스를 통해 단 한번의 연산으로 임의의 요소에 접근(random access, O(1))할 수 있다. 이는 매우 효율적이며 고속으로 동작한다.

&nbsp;  

> 검색 대상 요소의 메모리 주소 = 배열의 시작 메모리 주소 + 인덱스 * 요소의 바이트 수

&nbsp;  

예를 들어, 위 그림처럼 메모리 주소 1000에서 시작하고 각 요소의 크기가 8byte인 배열을 생각해 보자.

* 인덱스가 0인 요소의 메모리 주소: 1000 + 0 * 8 = 1000
* 인덱스가 1인 요소의 메모리 주소: 1000 + 1 * 8 = 1008
* 인덱스가 2인 요소의 메모리 주소: 1000 + 2 * 8 = 1016

이처럼 **배열은 인덱스를 통해 효율적으로 요소에 접근할 수 있다는 장점이 있다.** 하지만 정렬되지 않은 배열에서 특정한 값을 검색하는 경우, 모든 배열 요소를 처음부터 값을 발견할 때까지 차례대로 선형 검색(O(n))해야 한다.

또한 **배열에 요소를 삽입하거나 삭제하는 경우**, 배열 요소를 연속적으로 유지하기 위해 요소를 이동시켜야 하는 **단점**도 있다.

<img src="https://user-images.githubusercontent.com/32444914/82527158-b267a200-9b70-11ea-8370-3eabbafa4d27.png" width="60%" />

자바스크립트의 배열은 지금까지 살펴본 자료 구조에서 말하는 일반적이 의미의 배열과 다르다. 즉, 배열의 요소를 위한 각각의 메모리 공간은 동일할 크기를 갖지 않을 수 있으며, 연속적으로 이어져 있지 않을 수도 있다. 배열의 요소가 연속적으로 이어져 있지 않는 배열을 <strong>희소 배열(sparse array)</strong>이라 한다.

이처럼 자바스크립트의 배열은 엄밀히 말해 일반적 의미의 배열이 아니다. **자바스크립트의 배열은 일반적인 배열의 동작을 흉내낸 특수한 객체이다.**

```javascript
console.log(Object.getOwnPropertyDescriptors([1, 2, 3]));
/*
{
	'0': {value: 1, writable: true, enumerable: true, configurable: true},
	'1': {value: 2, writable: true, enumerable: true, configurable: true},
  '2': {value: 3, writable: true, enumerable: true, configurable: true},
  length: {value: 3, writable: true, enumerable: false, configurable: false}
}
*/
```

이처럼 자바스크립트 배열은 **인덱스를 프로퍼티 키로 가지며**, length 프로퍼티를 가지는 특수한 객체이다. **자바스크립트 배열의 요소는 사실 프로퍼티 값이다.** 자바스크립트에서 사용할 수 있는 모든 값은 객체의 프로퍼티 값이 될 수 있으므로 어떤 타입의 값이라도 배열의 요소가 될 수 있다.

```javascript
const arr = [
  'string',
  10,
  true,
  null,
  undefined,
  NaN,
  Infinity,
  [],
  {},
  function () {}
];
```

&nbsp;  

일반적인 배열과 자바스크립트 배열의 장단점은 아래와 같다.

| 일반 배열                                                    | 자바스크립트의 배열                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 인덱스로 배열 요소에 빠르게 접근할 수 있다.                  | 자바스크립트 배열은 해시 테이블로 구현된 객체이므로, 일반 배열보다 인덱스로 배열 요소에 접근하는 속도가 느리다. |
| 특정 요소를 검색하거나 요소를 삽입 또는 삭제하는 경우에는 효율적이지 않다. | 특정 요소를 검색하거나 요소를 삽입 또는 삭제하는 경우에는 일반 배열보다 빠른 성능을 기대할 수 있다. |

이처럼 인덱스로 배열 요소에 접근할 때 일반 배열보다 느릴 수 밖에 없는 구조적인 단점을 보완하기 위해 대부분의 모던 자바스크립트 엔진은 배열을 일반 객체와 구별하여 보다 배열처럼 동작하도록 최적화하여 구현하였다.

&nbsp;  

## 3. length 프로퍼티와 희소 배열

* 배열의 **length 프로퍼티**는 요소의 개수, 즉 **배열의 길이**를 나타내는 정수를 값으로 가진다.
* length 프로퍼티 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.
* length 프로퍼티의 값을 명시적으로 변경할 수 있다.
* length 프로퍼티에 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우, **length 프로퍼티 값은 변경되지만, 실제 배열에는 아무런 변함이 없다.** 값이 없이 비어있는 요소를 위해 메모리 공간을 확보하지 않으며, 빈 요소를 생성하지도 않는다.
* 희소 배열의 empty는 요소의 값이 아니다. empty가 표시된 인덱스의 요소에 접근하면 undefined를 출력한다. 즉, 해당 인덱스(프로퍼티)를 갖지 않는다.
* 희소 배열은 length 프로퍼티의 값이 배열 요소의 개수보다 항상 크다.
* **배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.**

&nbsp;  

length 프로퍼티는 요소의 개수, 즉 **배열의 길이**를 나타내는 정수를 값으로 가진다. 빈 배열일 경우 length 프로퍼티의 값은  0이며, 빈 배열이 아닐 경우 가장 큰 인덱스에 1을 더한 것과 같다.

```javascript
[].length // 0
[1, 2, 3].length // 3
```

length 프로퍼티의 값은 0과 2^32 미만의 양의 정수이다. 즉, 배열은 요소를 최대 2^32 - 1개 가질 수 있다. 따라서 배열에서 사용할 수 있는 가장 작은 인덱스는 0이며 가장 큰 인덱스는 2^32 - 2이다.

&nbsp;  

length 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.

```javascript
const arr = [1, 2, 3];
console.log(arr.length); // 3

// 요소 추가
arr.push(4);
console.log(arr.length); // 4

// 요소 삭제
arr.pop();
console.log(arr.length); // 3
```

&nbsp;  

length 프로퍼티의 값은 요소의 개수를 바탕으로 결정되지만, 임의의 숫자 값을 명시적으로 할당할 수도 있다.

```javascript
const arr = [1, 2, 3, 4, 5];

// length 프로퍼티에 현재 length 프로퍼티 값보다 작은 숫자 값을 할당
arr.length = 3;

// 배열의 길이가 줄어든다.
console.log(arr); // [1, 2, 3]
```

&nbsp;  

주의할 것은 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우다. **이때 length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.**

```javascript
const arr = [1];

// length 프로퍼티에 현재 배열의 길이보다 더 큰 값을 할당
arr.length = 3;

// length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.
console.log(arr.length); // 3
console.log(arr); // [1, empty * 2]
```

위 예제의 출력 결과에서 empty * 2는 실제로 추가된 배열의 요소가 아니다. 즉, arr[1]과 arr[2]에는 값이 존재하지 않는다.

이와 같이 length 프로퍼티에 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우, **length 프로퍼티 값은 변경되지만, 실제 배열에는 아무런 변함이 없다.** 값이 없이 비어있는 요소를 위해 메모리 공간을 확보하지 않으며, 빈 요소를 생성하지도 않는다.

```javascript
console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': {value: 1, writable: true, enumerable: true, configurable: true},
  length: {value: 3, writable: true, enumerable: false, configurable: false}
}
*/
```

**이처럼 배열의 요소가 연속적으로 위치하지 않고 일부가 비어있는 배열을 희소 배열이라 한다.** 자바스크립트는 희소 배열을 문법적으로 허용한다. 위 예제는 배열의 뒷부분만이 비어 있어서 요소가 연속적으로 위치하는 것처럼 보일 수 있으나, 중간이나 앞 부분이 비어 있을 수도 있다.

```javascript
// 희소 배열
const sparse = [, 2, , 4];

// 희소 배열의 length 프로퍼티 값은 요소의 개수와 일치하지 않는다.
console.log(sparse.length); // 4
console.log(sparse); // [empty, 2, empty, 4]

// 배열 arr에는 인덱스가 0, 2인 요소가 존재하지 않는다.
console.log(Object.getOwnPropertyDescriptors(sparse));
/*
{
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '3': { value: 4, writable: true, enumerable: true, configurable: true },
  length: { value: 4, writable: true, enumerable: false, configurable: false }
}
*/
```

일반적인 배열의 length는 배열 요소의 개수와 언제나 일치한다. 하지만 **희소 배열은 length와 배열 요소의 개수가 일치하지 않는다.** 희소 배열은 length 프로퍼티의 값이 언제나 배열 요소의 개수보다 크다.

희소 배열은 연속적인 값의 집합이라는 배열의 기본적인 개념과 맞지 않으며, 성능에도 좋지 않은 영향을 준다. 최적화가 잘되어 있는 모던 자바스크립트 엔진은 요소의 타입이 일치하는 배열을 생성할 때, 일반 배열처럼 연속된 메모리 공간을 확보하는 것으로 알려져 있다.

따라서 배열을 생성할 경우 희소 배열을 생성하지 않도록 주의해야한다. **배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.**

&nbsp;  

## 4. 배열 생성

* 배열 리터럴
* Array 생성자 함수
* Array.of
* Array.from

&nbsp;  

### 4.1. 배열 리터럴

객체와 마찬가지로 배열도 다양한 생성 방식이 있다. 가장 일반적이고 간편한 배열 생성 방식은 배열 리터럴을 사용하는 것이다.

```javascript
const arr = []; // 빈 배열
const arr2 = [1, 2];
const sparse = [1, , 3]; // 희소 배열

// 희소 배열의 length는 배열의 실제 요소 개수보다 언제나 크다.
console.log(sparse.length); // 3
console.log(sparse); // [1, empty, 3]
console.log(sparse[1]); // undefined
```

위 예제의 `sparse` 배열은 인덱스가 1인 요소를 갖지 않는다. `sparse[1]`이 undefined인 이유는 객체인 `sparse`에 프로퍼티 키가 `1`인 프로퍼티가 존재하지 않기 때문이다.

&nbsp;  

### 4.2. Array 생성자 함수

Object 생성자 함수를 통해 객체를 생성할 수 있듯이, Array 생성자 함수를 통해 배열을 생성할 수도 있다. **Array 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작한다.**

&nbsp;  

**1. 전달된 인수가 1개이고 숫자인 경우, 인수를 length로 배열을 생성한다.**

```javascript
const arr = new Array(10);

console.log(arr); // [empty * 10]
console.log(arr.length); // 10
```

이때 생성된 배열은 **희소 배열**이다. length 프로퍼티의 값은 0이 아니지만, 실제로 배열의 요소는 존재하지 않는다.

```javascript
console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  length: {value: 10, writable: true, enumerable: false, configurable: false}
}
*/
```

배열은 요소를 최대 2^32 - 1개 가질 수 있다. 따라서 Array 생성자 함수에 전달한 인수는 0 또는 2^32 미만의 **양의 정수**이어야 한다. 전달된 인수가 범위를 벗어나면 RangeError가 발생한다.

```javascript
// 전달된 인수가 음수이면 에러 발생
new Array(-1); // RangeError: Invalid array length

// 배열은 요소를 최대 2^32 - 1개 (4,294,967,295) 가질 수 있다.
new Array(4294967296); // RangeError: Invalid array length
```

&nbsp;  

**2. 전달된 인수가 없는 경우, 빈 배열을 생성한다. 즉 배열 리터럴 `[]`과 같다**

```javascript
const empty = new Array();
console.log(empty); // []
```

&nbsp;  

**3. 전달된 인수가 2개 이상이거나 숫자가 아닌 경우, 인수를 요소로 가지는 배열을 생성한다.**

```javascript
// 전달된 인수가 2개 이상
const arr1 = new Array(1, 2); // [1, 2]

// 전달된 인수가 1개지만 숫자가 아닐 때
const arr2 = new Array({}); // [{}]
```

&nbsp;  

**4. Array 생성자 함수는 new 연산자와 함께 호출하지 않더라도 배열을 생성하는 생성자 함수로 동작한다.**

```javascript
const arr = Array(1, 2, 3); // [1, 2, 3]
```

이는 Array 생성자 함수 내부에서 `new.target`을 확인하기 때문이다.

&nbsp;  

### 4.3. Array.of

ES6에서 새롭게 도입된 `Array.of` 메소드는 전달된 인수를 요소로 가지는 배열을 생성한다. `Array.of`는 `Array` 생성자 함수와 다르게 **전달된 인수가 1개이고 숫자이더라도 인수를 요소로 가지는 배열을 생성**한다.

```javascript
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 가지는 배열을 생성한다.
const arr1 = Array.of(1); // [1]

const arr2 = Array.of(1, 2, 3); // [1, 2, 3]

const arr3 = Array.of('string'); // ['string']
```

&nbsp;  

### 4.4. Array.from

ES6에서 새롭게 도입된 `Array.from` 메소드는 **유사 배열 객체(array-like object) 또는 이터러블 객체(iterable object)를 변환하여 새로운 배열을 생성한다.**

```javascript
// 문자열은 이터러블이다.
const arr1 = Array.from('Hello'); // ['H', 'e', 'l', 'l', 'o']

// 유사 배열 객체를 변환하여 새로운 배열을 생성한다.
const arr2 = Array.from({ 0: 'a', 1: 'b', length: 2 }); // ['a', 'b']
```

`Array.from`을 사용하면 **두번째 인수로 전달한 콜백 함수**를 통해 값을 만들면서 요소를 채울 수 있다. 두번째 인수로 전달한 콜백 함수는 **첫번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달받아 새로운 요소를 생성**할 수 있다.

```javascript
// Array.from에 length만 존재하는 유사 배열을 전달하면 undefined를 요소로 채운다.
const arr1 = Array.from({ length: 5 });
console.log(arr1); // [undefined, undefined, undefined, undefined, undefined]

// Array.from의 두번째 인수로 배열의 모든 요소에 대해 호출할 콜백 함수를 전달할 수 있다.
// 이 콜백 함수는 첫번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달 받아 호출된다.
const arr2 = Array.from({ length: 5 }, (_, i) => i);
console.log(arr2); // [0, 1, 2, 3, 4]
```

&nbsp;  

> **유사 배열 객체와 이터러블 객체**
>
> 유사 배열 객체(array-like Object)는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고, length 프로퍼티를 가지는 객체를 말한다. 따라서 for 문으로 순회할 수도 있다.
>
> 이터러블 객체(iterable object)는 Symbol.iterator 메소드를 구현하여 for...of 문으로 순회할 수 있으며, 스프레드 문법의 대상으로 사용할 수 있는 객체를 말한다.

&nbsp;  

## 5. 배열 요소의 참조

배열 요소를 참조할 때는 대괄호(`[]`) 표기법을 사용한다. **대괄호 안에는 인덱스가 와야 한다.** 정수로 평가되는 표현식이라면 인덱스 대신 사용할 수 있다. **인덱스는 값을 참조할 수 있다는 의미에서 객체의 프로퍼티 키와 같은 역할을 한다.**

```javascript
const arr = [1, 2];

// 인덱스가 0인 요소를 참조
console.log(arr[0]); // 1
```

&nbsp;  

존재하지 않는 요소에 접근하면 undefined가 반환된다.

```javascript
const arr = [1, 2];

// 인덱스가 2인 요소를 참조
// 배열 arr에 인덱스가 2인 요소는 존재하지 않는다.
console.log(arr[2]); // undefined
```

&nbsp;  

**배열은 사실 인덱스를 프로퍼티 키로 가지는 객체이다.** 따라서 존재하지 않는 프로퍼티 키로 객체의 프로퍼티에 접근했을 때 undefined를 반환하는 것 처럼 **배열도 존재하지 않는 요소를 참조하면 undefined가 반환된다.**

같은 이유로 희소 배열의 존재하지 않는 요소를 참조하여도 undefined가 반환된다.

```javascript
// 희소 배열
const arr = [1, , 3];

// 배열 arr에는 인덱스가 1인 요소가 존재하지 않는다.
console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': {value: 1, writable: true, enumerable: true, configurable: true},
  '2': {value: 3, writable: true, enumerable: true, configurable: true},
  length: {value: 3, writable: true, enumerable: false, configurable: false}
*/

// 존재하지 않는 요소를 참조하면 undefined가 반환된다.
console.log(arr[1]); // undefined
console.log(arr[3]); // undefined
```

&nbsp;  

## 6. 배열 요소의 추가와 갱신

객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼, **배열에도 요소를 동적으로 추가할 수 있다.** 요소가 존재하지 않는 인덱스의 배열 요소에 값을 할당하면 새로운 요소가 추가된다. 이때 **length 프로퍼티 값은 자동 갱신된다.**

```javascript
const arr = [0];

// 배열 요소의 추가
arr[1] = 1;

console.log(arr); // [0, 1]
console.log(arr.length); // 2
```

&nbsp;  

만약 **현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 된다.**

```javascript
arr[100] = 100;

console.log(arr); // [0, 1, empty * 98, 100]
console.log(arr.length); // 101
```

&nbsp;  

이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.

```javascript
// 요소값의 갱신
arr[1] = 10;

console.log(arr); // [0, 10, empty * 98, 100]
```

&nbsp;  

인덱스는 요소의 위치를 나타내므로 반드시 0 이상의 정수(**또는 정수 형태의 문자열**)을 사용하여야 한다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다. 이때 **추가된 프로퍼티는 length 프로퍼티의 값에 영향을 주지 않는다.**

```javascript
const arr = [];

// 배열 요소의 추가
arr[0] = 1;
arr['1'] = 2;

// 프로퍼티 추가
arr['foo'] = 3;
arr.bar = 4;
arr[1.1] = 5;
arr[-1] = 6;

console.log(arr); // [1, 2, foo: 3, bar: 4, '1.1': 5, '-1': 6]

// 프로퍼티는 length에 영향을 주지 않는다.
console.log(arr.length); // 2
```

&nbsp;  

## 7. 배열 요소의 삭제

* `delete` 연산자
* `Array.prototype.splice`

&nbsp;  

배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 `delete` 연산자를 사용할 수 있다.

```javascript
const arr = [1, 2, 3];

// 배열 요소의 삭제
delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
console.log(arr.length); // 3
```

`delete` 연산자는 객체의 프로퍼티를 삭제한다. 따라서 위 예제의 `delete arr[1]`은 arr에서 프로퍼티 키가 `'1'`인 프로퍼티를 삭제한다. 이때 **배열은 희소 배열이 되며 length 프로퍼티 값은 변하지 않는다.** 따라서 희소 배열을 만드는 `delete` 연산자는 사용하지 않는 것이 좋다.

희소 배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 `Array.prototype.splice` 메소드를 사용한다.

```javascript
const arr = [1, 2, 3];

// Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소 수)
// arr[1]부터 1개의 요소를 제거
arr.splice(1, 1);
console.log(arr); // [1, 3]

// length 프로퍼티에 변경이 반영된다.
console.log(arr.length); // 2
```

&nbsp;  

## 8. 배열 메소드

배열은 배열을 다룰 때 필요한 다양한 메소드를 제공한다. Array 생성자 함수는 정적 메소드를 제공하며, 배열 객체의 프로토타입인 `Array.prototype`은 프로토타입 메소드를 제공한다.

배열 메소드는 결과물을 반환하는 패턴이 2가지이므로 주의가 필요하다. 배열에는 <strong>원본 배열을 직접 변경하는 메소드(mutator)</strong>와 원본 배열을 직접 변경하지 않고 <strong>새로운 배열 생성하여 반환하는 메소드(accessor)</strong>가 있다.

```javascript
const arr = [1];

// push 메소드는 원본 배열(arr)을 직접 변경한다.
arr.push(2);
console.log(arr); // [1, 2]

// concat 메소드는 원본 배열(arr)을 직접 변경하지 않고 새로운 배열을 생성하여 반환한다.
const result = arr.concat(3);
console.log(arr); // [1, 2]
console.log(result); // [1, 2, 3]
```

원본 배열을 직접 변경하는 메소드는 외부 상태를 직접 변경하는 부수 효과(side effect)가 있으므로 사용에 주의해야 한다. 따라서 가급적 원본 배열을 직접 변경하지 않는 메소드(accessor)를 사용하는 편이 좋다.

| 메소드                                               | 요약                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| Array.isArray(value)                                 | value가 배열이면 true, 아니면 false를 반환                   |
| Array.prototype.indexOf(value, startIdx)             | * 배열에 value가 있는 경우, 해당 요소의 인덱스를 반환(중복되는 요소가 있는 경우, 첫번째 인덱스를 반환).<br />* 배열에 value가 없는 경우 -1을 반환.<br />* (옵션) startIdx는 검색을 시작할 인덱스이다.<br />* 배열에 특정 요소가 존재하는지 확인할 때 유용하다. |
| Array.prototype.push(value1, value2, value3 ...)     | * 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가한다.<br />* 변경된 length 프로퍼티 값을 반환한다.<br />* mutator |
| Array.prototype.pop()                                | * 원본 배열의 마지막 요소를 제거한다.<br />* 제거한 요소를 반환한다.<br />* 원본 배열이 빈 배열이면 undefined를 반환한다.<br />* 스택 구현에 사용된다.<br />* mutator |
| Array.prototype.unshift(value1, value2, value3 ...)  | * 인수로 전달받은 모든 값을 원본 배열의 선두에 추가한다.<br />* 변경된 length 프로퍼티 값을 반환한다.<br />* mutator |
| Array.prototype.shift()                              | * 원본 배열의 첫번째 요소를 제거한다.<br />* 제거한 요소를 반환한다.<br />* 원본 배열이 빈 배열이면 undefined를 반환한다.<br />* 큐(Queue) 구현에 사용된다.<br />* mutator |
| Array.prototype.splice(startIdx, deleteCount, items) | * 원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거한다.<br />* startIdx는 원본 배열의 요소를 제거하기 시작할 인덱스이다.<br />* (옵션) deleteCount는 startIdx부터 제거할 요소의 개수이다.<br />* (옵션) items는 제거한 위치에 삽입될 요소들의 목록이다.<br /><br />* 원본 배열에서 제거된 요소를 담은 배열을 반환한다.<br />* mutator |
| Array.prototype.concat(value)                        | * value(배열 또는 원시값)을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다.<br />* value가 배열일 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.<br />* push와 unshift 메소드를 대체할 수 있다.<br />* accessor |
| Array.prototype.slice(startIdx, endIdx)              | * 인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다.<br />* (옵션) startIdx는 복사를 시작할 인덱스이다.<br />* (옵션) endIdx는 복사를 종료할 인덱스이다.(exclusive)<br />* 인수를 모두 생략하면 원본 배열의 새로운 복사본을 생성하여 반환한다.<br />* 생성된 복사본은 얕은 복사(shallow copy)를 통해 생성된다.<br />* accessor |
| Array.prototype.join(seperator)                      | * 원본 배열의 모든 요소를 문자열로 변환한 후, seperator로 연결한 문자열을 반환한다.<br />* (옵션) seperator는 문자열이며, 생략하면 기본 seperator는 `,`이다.<br />* accessor |
| Array.prototype.reverse()                            | * 원본 배열의 요소 순서를 반대로 변경한다.<br />* 변경된 배열을 반환한다.<br />* mutator |
| Array.prototype.fill(value, startIdx, endIdx)        | * 인수로 전달 받은 값을 요소로 배열의 처음부터 끝까지 채운다.<br />* (옵션) startIdx는 요소 채우기를 시작할 인덱스이다.<br />* (옵션) endIdx는 요소 채우기를 멈출 인덱스이다.(exclusive)<br />* mutator |
| Array.prototype.includes(value, startIdx)            | * 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 혹은 false를 반환한다.<br />* value는 검색할 대상을 의미한다.<br />* (옵션) startIdx는 검색을 시작할 인덱스이다.<br />* NaN이 포함되어 있는지 확일할 수 있다. |
| Array.prototype.flat(depth)                          | * 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다.<br />* 평탄화한 배열을 반환한다.<br />* (옵션) depth는 중첩 배열을 평탄화할 깊이를 의미한다.<br />* depth를 지정하지 않으면 기본값은 1이다.<br />* depth를 Infinity로 설정하면 중첩 배열 모두를 평탄화한다. |

&nbsp;  

## 9. 배열 고차 함수

고차 함수(High-Order Function, HOF)는 함수를 인자로 전달받거나, 함수를 반환하는 함수를 말한다. 자바스크립트의 함수는 일급 객체이므로 값처럼 인자로 전달할 수 있으며 반환할 수도 있다. 고차 함수는 외부 상태 변경이나 가변(mutable) 데이터를 피하고 **불변성(immutability)을 지향**하는 함수형 프로그래밍에 기반을 두고 있다.

함수형 프로그래밍은 순수 함수(pure function)와 보조 함수의 조합을 통해 로직 내에 존재하는 **조건문과 반복문을 제거하여 복잡성을 해결**하고 **변수의 사용을 억제**하여 상태 변경을 피하려는 프로그래밍 패러다임이다. 조건문이나 반복문은 로직의 흐름을 이해하기 어렵게 하여 가독성을 해치고, 변수의 값은 누군가에 의해 언제든지 변경될 수 있어 오류 발생의 근본적 원인이 될 수 있기 때문이다. 함수형 프로그래밍은 결국 **순수 함수를 통해 부수 효과(side effect)를 최대한 억제**하여 오류를 피하고 프로그램의 안정성을 높이려는 노력의 한 방법이라고 할 수 있다.

&nbsp;  

### 9.1. Array.prototype.sort

sort 메소드는 배열의 요소를 정렬한다. **원본 배열을 직접 변경**하며(mutator) 정렬된 배열을 반환한다. sort 메소드는 기본적으로 요소를 오름차순으로 정렬한다.

```javascript
const fruits = ['Banana', 'Orange', 'Apple'];

// 오름차순(ascending) 정렬
fruits.sort();

// sort 메소드는 원본 배열을 직접 변경한다.
console.log(fruits); // ['Apple', 'Banana', 'Orange']
```

&nbsp;  

문자열 요소들로 이루어진 배열의 정렬은 아무 문제가 없다. 하지만 **숫자 요소들로 이루어진 배열을 정렬할 때는 주의가 필요하다.**

```javascript
const points = [40, 100, 1, 5, 2, 25, 10];

points.sort();

// 숫자 요소들로 이루어진 배열은 의도한 대로 정렬되지 않는다.
console.log(points); // [1, 10, 100, 2, 25, 40, 5]
```

**sort 메소드의 기본 정렬 순서는 문자열 Unicode 포인트 순서에 따른다.** 배열의 요소가 숫자 타입이라 할지라도 배열의 요소를 **일시적으로 문자열로 변환한 후, 정렬한다.**

따라서 숫자 요소를 정렬하기 위해서는 sort 메소드에 **정렬 순서를 정의하는 비교 함수를 인수로 전달**한다. 비교 함수를 생략하면 배열의 각 요소는 일시적으로 문자열로 변환되어 Unicode 포인트 순서에 따라 정렬된다.

```javascript
const points = [40, 100, 1, 5, 2, 25, 10];

// 숫자 배열 오름차순 정렬
// 비교 함수의 반환 값이 0보다 작은 경우, a를 우선하여 정렬한다.
points.sort((a, b) => a - b);
cosole.log(points); // [1, 2, 5, 10, 25, 40, 100]

// 숫자 배열 내림차순 정렬
// 비교 함수의 반환값이 0보다 큰 경우, b를 우선하여 정렬한다.
points.sort((a, b) => b - a);
console.log(points); // [100, 40, 25, 10, 5, 2, 1]

// 요소가 문자열인 경우 산술 연산으로 비교하면 NaN이 나오므로 비교 연산을 사용한다.
points.sort((a, b) => a < b ? -1 : (a > b ? 1 : 0));
```

&nbsp;  

> **Array.prototype.sort 메소드의 알고리즘**
>
> Array.prototype.sort 메소드는 10개 이상의 요소가 있는 배열을 정렬할 때 불안정하다고 알려진 quickSort 알고리즘을 사용했었다. ECMAScript 2019(ES10)에서는 timesort 알고리즘을 적용하도록 변경되었다. timesort 알고리즘은 합병 정렬과 삽입 정렬을 이용해 구현되었다 한다.

&nbsp;  

### 9.2. Array.prototype.forEach

forEach 메소드는 for 문을 대체할 수 있는 메소드이다. forEach 메소드는 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 호출한다.

```javascript
const numbers = [1, 2, 3];
let pows = [];

// for 문으로 배열 순회
for (let i = 0; i < number.length; i++) {
  pows.push(numbers[i] ** 2);
}
console.log(pows); // [1, 4, 9]

// forEach 메소드로 배열 순회
numbers.forEach(item => pows.push(item ** 2));
console.log(pows); // [1, 4, 9]
```

&nbsp;  

forEach 메소드의 콜백 함수는 요소값, 인덱스, forEach 메소드를 호출한 배열(this)를 전달 받을 수 있다.

```javascript
// forEach 메소드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
[1, 2, 3].forEach((item, index, arr) => {
  console.log(`${arr}의 ${index}번째 요소 = ${item}`);
});
/*
1,2,3의 0번째 요소 = 1
1,2,3의 1번째 요소 = 2
1,2,3의 2번째 요소 = 3
*/
```

&nbsp;  

forEach 메소드는 원본 배열을 변경하지 않는다. 하지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.

```javascript
const numbers = [1, 2, 3];

// forEach 메소드는 원본 배열을 변경하지 않는다.
// 하지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.
// 원본 배열을 직접 변경하려면 콜백 함수의 3번째 인자를 사용한다.
numbers.forEach((item, index, arr) => {
  arr[index] = item ** 2;
});

console.log(numbers); // [1, 4, 9]
```

&nbsp;  

forEach 메소드의 반환값은 언제나 undefined이다.

```javascript
const result = [1, 2, 3].forEach(item => console.log(item));
// 1
// 2
// 3

console.log(result); // undefined
```

&nbsp;  

forEach 메소드에 두번째 인수로 forEach 메소드 내부에서 this로 사용될 객체를 전달할 수 있다.

```javascript
class Numbers {
  numberArray = [];

	multiply(arr) {
    arr.forEach(function (item) {
      // 외부에서 this를 전달하지 않으면 this는 undefined(엄격 모드 적용)을 가리킨다.
      // multiply 내부의 this는 인스턴스를 가리킨다.
      this.numberArray.push(item * item);
    }, this); // forEach 메소드 내부에서 this로 사용될 객체를 전달
  }
}

const numbers = new Numbers();
numbers.multiply([1, 2, 3]);
console.log(numbers.numberArray); // [1, 4, 9]
```

보다 나은 방법은 ES6 화살표 함수를 사용하는 것이다.

```javascript
class Number {
  numberArray = [];

	multiply(arr) {
    // 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다.
    arr.forEach(item => this.numberArray.push(item * item));
  }
}

const numbers = new Numbers();
numbers.multiply([1, 2, 3]);
console.log(numbers.numberArray); // [1, 4, 9]
```

&nbsp;  

forEach 메소드의 동작을 이해하기 위해 forEach 메소드의 폴리필(최신 사양의 기능을 지원하지 않는 브라우저를 위해 누락된 최신 사양의 기능을 구현하여 추가하는 것을 폴리필(pollyfill)이라 한다.)을 살펴보자.

```javascript
// 만약 Array.prototype에 forEach 메소드가 존재하지 않으면 폴리필을 추가한다.
if (!Array.prototype.forEach) {
  Array.prototype.forEach = function (callback, thisArg) {
    // 전달받은 첫번째 인수가 함수가 아니면 TypeError를 발생시킨다.
  	if (typeof callback !== 'function') {
      throw new TypeError(callback + ' must be a function');
    }
    
    // this로 사용할 두번째 인수를 전달받지 못하면 전역 객체를 this로 사용한다.
    thisArg = thisArg || window;
    
    // for 문으로 배열(this)을 순회하면서 콜백 함수를 호출한다.
    for (var i = 0; i < this.length; i++) {
      // call 메소드를 통해 두번째 인수로 전달받은 thisArg를 전달하면서 콜백 함수를 호출한다.
      // 이때 콜백 함수의 인수로 배열 요소, 인덱스, 배열 자신을 전달한다.
      callback.call(thisArg, this[i], i, this);
    }
  };
}
```

이처럼 forEach 메소드도 내부에서는 반복문을 통해 배열을 순회할 수 밖에 없다. 단, 반복문을 메소드 내부로 은닉하여 로직의 흐름을 이해하기 쉽게 하고 복잡성을 해결한다.

&nbsp;  

forEach 메소드는 for 문과는 달리 break, continue 문을 사용할 수 없다. 배열의 모든 요소를 빠짐없이 순회하며 중간에 순회를 중단할 수 없다.

```javascript
[1, 2, 3].forEach(item => {
  console.log(item);
  if (item > 1) break; // SyntaxError: Illegal break statement
  // if (item > 1) continue; // SyntaxError: Illegal break statement
})
```

희소 배열의 존재하지 않는 요소는 순회 대상에서 제외된다. 이는 map, filter, reduce 메소드 등에서도 마찬가지이다.

```javascript
// 희소 배열
const arr = [1, , 3];

// for 문으로 희소 배열을 순회
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]); // 1, undefined, 3
}

// forEach 메소드는 희소 배열의 존재하지 않는 요소를 순회 대상에서 제외한다.
arr.forEach(item => console.log(item)); // 1, 3
```

&nbsp;  

### 9.3. Array.prototype.map

map 메소드는 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다. 그리고 **콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.** 이때 원본 배열은 변경되지 않는다.

```javascript
const numbers = [1, 4, 9];
const roots = numbers.map(item => Math.sqrt(item));

// map 메소드는 새로운 배열을 반환한다.
console.log(roots); // [1, 2, 3]
// map 메소드는 원본 배열은 변경하지 않는다.
console.log(numbers); // [1, 4, 9]
```

&nbsp;  

forEach 메소드는 배열을 순회하며 요소 값을 참조하여 무언가를 하기 위한 함수이며, map 메소드는 **배열을 순회하며 요소 값을 다른 값으로 맵핑하기 위한 함수이다.** 따라서 **map 메소드가 생성하여 반환하는 새로운 배열의 length는 map 메소드를 호출한 배열(this)의 length와 반드시 일치한다.** 즉, 1:1 매핑(mapping)한다.

<img src="https://user-images.githubusercontent.com/32444914/82622654-5016ac00-9c19-11ea-9e94-4133988651d9.png" width="80%" />

&nbsp;  

forEach 메소드와 마찬가지로 map 메소드의 콜백 함수는 요소값, 인덱스, map 메소드를 호출한 배열(this)를 전달 받을 수 있다.

```javascript
[1, 2, 3].map((item, index, arr) => {
  console.log(`${arr}의 ${index}번째 요소 = ${item}`);
  return item;
});

/*
1,2,3의 0번째 요소 = 1
1,2,3의 1번째 요소 = 2
1,2,3의 2번째 요소 = 3
*/
```

&nbsp;  

forEach 메소드와 마찬가지로 map 메소드에 두번째 인자로 map 메소드 내부에서 this로 사용될 객체를 전달할 수 있다.

```javascript
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }
  
  prefixArray(arr) {
    return arr.map(function (item) {
      // 외부에서 this를 전달하지 않으면 this는 undefined를 가리킨다.
      return this.prefix + item;
    }, this); // map 메소드 내부에서 this로 사용될 객체를 전달(인스턴스)
  }
}

const prefixer = new Prefixer('-webkit-');
const preArr = prefixer.prefixArray(['linear-gradient', 'border-radius']);
console.log(preArr); // ['-webkit-linear-gradient', '-webkit-border-radius']
```

보다 나은 방법은 ES6의 화살표 함수를 사용하는 것이다.

```javascript
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }
  
  prefixArray(arr) {
    return arr.map(item => this.prefix + item);
  }
}
const prefixer = new Prefixer('-webkit-');
const preArr = prefixer.prefixArray(['linear-gradient', 'border-radius']);
console.log(preArr); // ['-webkit-linear-gradient', '-webkit-border-radius']
```

&nbsp;  

### 9.4. Array.prototype.filter

filter 메소드는 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다. 그리고 **콜백 함수의 반환값이 true인 요소만을 추출한 새로운 배열을 반환**한다. 이때 원본 배열은 변경되지 않는다.

```javascript
const numbers = [1, 2, 3, 4, 5];

// 홀수만을 필터링 한다
const odds = numbers.filter(num => num % 2);
console.log(odds); // [1, 3, 5];
```

filter 메소드는 배열에서 특정 요소만을 필터링 조건으로 추출하여 새로운 배열을 만들고 싶을 때 사용한다. 따라서 **filter 메소드가 생성하여 반환하는 새로운 배열의 length는 filter 메소드를 호출한 배열, 즉 this의 length와 같거나 작다.**

<img src="https://user-images.githubusercontent.com/32444914/82731358-29ec2b80-9d41-11ea-93a7-3a9e5d889055.png" width="60%" />

forEach, map 메소드와 마찬가지로 filter 메소드의 콜백 함수는 요소값, 인덱스, filter 메소드를 호출한 배열(this)를 전달 받을 수 있다.

```javascript
[1, 2, 3].filter((item, index, arr) => {
  console.log(`${arr}의 ${index}번째 요소 = ${item}`);
  return item % 2;
});
/*
요소값: 1, 인덱스: 0, this: 1,2,3
요소값: 2, 인덱스: 1, this: 1,2,3
요소값: 3, 인덱스: 2, this: 1,2,3
*/
```

forEach, map 메소드와 마찬가지로 filter 메소드에 두번째 인자로 filter 메소드 내부에서 사용할 this 객체를 전달할 수 있다. 보다 나은 방법은 화살표 함수를 사용하는 것이다.

```javascript
class Users {
  constructor() {
    this.users = [
      { id: 1, name: 'Kim' },
      { id: 2, name: 'Park' }
    ];
  }

	// 요소 추출
	findById(id) {
    // id가 일치하는 사용자만 반환
    return this.users.filter(user => user.id === id);
  }
  
  // 요소 제거
  remove(id) {
    // id가 일치하지 않는 사용자를 모두 반환
    this.users = this.users.filter(user => user.id !== id);
  }
}

const users = new Users();

let user = users.findById(1);
console.log(user); // [{ id: 1, name: 'Kim' }]

users.remove(1);

user = users.findById(1);
console.log(user); // []
```

&nbsp;  

### 9.5. Array.prototype.reduce

reduce 메소드는 배열을 순회하며 콜백 함수의 이전 반환값과 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행해 **하나의 결과값**을 반환한다. 이때 원본 배열은 변경되지 않는다.

reduce 메소드는 첫번째 인수로 콜백 함수, **두번째 인수로 초기값을 전달받는다.** reduce 메소드의 콜백 함수에는 4개의 인수, 초기값 또는 콜백 함수의 이전 반환값, 요소값, 인덱스, reduce 메소드를 호출한 배열(this)이 전달된다.

아래 예제를 살펴보자. 예제의 reduce 메소드는 2개의 인수, 즉 콜백 함수와 초기값 0을 전달받아 배열의 모든 요소의 누적을 구한다.

```javascript
// 1부터 4까지 누적을 구한다.
const sum = [1, 2, 3, 4].reduce((accumulator, currentValue, index, array) => accumulator + currentValue, 0);

console.log(sum); // 10
```

<img src="https://user-images.githubusercontent.com/32444914/82732994-b7cd1400-9d4b-11ea-804e-977db661b3e4.png" width="60%" />

| iteration | accumulator | currentValue | index | array        | return                          |
| --------- | ----------- | ------------ | ----- | ------------ | ------------------------------- |
| 1         | 0 (초기값)  | 1            | 0     | [1, 2, 3, 4] | 1 (accumulator + currentValue)  |
| 2         | 1           | 2            | 1     | [1, 2, 3, 4] | 3 (accumulator + currentValue)  |
| 3         | 3           | 3            | 2     | [1, 2, 3, 4] | 6 (accumulator + currentValue)  |
| 4         | 6           | 4            | 3     | [1, 2, 3, 4] | 10 (accumulator + currentValue) |

**reduce 메소드를 사용할 때는 언제나 초기값을 전달하는 것이 안전하다**.

```javascript
const sum = [].reduce((acc, cur) => acc + cur);
// TypeError: Reduce of empty array with no initial value
```

이처럼 빈 배열로 reduce 메소드를 호출하면 에러가 발생한다. 이때 reduce 메소드에 초기값을 전달하면 에러가 발생하지 않는다.

```javascript
const sum = [].reduce((acc, cur) => acc + cur, 0);
console.log(sum); // 0
```

reduce 메소드로 객체의 특정 프로퍼티 값을 합산하는 경우을 생각해보자.

```javascript
const products = [
  { id: 1, price: 100 },
  { id: 2, price: 200 },
  { id: 3, price: 300 },
];

// 2번째 순회시, 콜백 함수에 숫자값이 전달된다. 이때 pre.price는 undefineddlek.
// iteration 1: acc = { id: 1, price: 100 }, cur = { id: 2, price: 200 }
// iteration 2: acc = 300, cur = { id: 3, price: 300 }
const priceSum = products.reduce((acc, cur) => acc.price + cur.price);

console.log(priceSum); // NaN
```

이처럼 객체의 특정 프로퍼티 값을 합산하는 경우에는 반드시 초기값을 전달해야 한다.

```javascript
const products = [
  { id: 1, price: 100 },
  { id: 2, price: 200 },
  { id: 3, price: 300 },
];

// iteration 1: acc = 0, cur = { id: 1, price: 100 }
// iteration 2: acc = 100, cur = { id: 2, price: 200 }
// iteration 3: acc = 300, cur = { id: 3, price: 300 }
const sum = products.reduce((acc, cur) => acc + cur.price, 0);
console.log(sum); // 600
```

&nbsp;  

### 9.6. Array.prototype.some

some 메소드는 배열을 순회하며 각 요소에 대해 인수로 전달된 콜백 함수를 호출한다. 이때 some 메소드는 콜백 함수의 반환값이 한번이라도 참이면 true, 모두 거짓이면 false를 반환한다. 즉, 배열의 요소 중 콜백 함수를 통해 정의한 조건을 만족하는 요소가 1개 이상 존재하는지 확인하여 그 결과를 **불리언 타입**으로 반환한다.

forEach, map, filter 메소드와 마찬가지로 some 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열(this)를 전달 받을 수 있다.

```javascript
// 배열의 요소 중 10보다 큰 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(v => v > 10); // true

// 배열의 요소 중 0보다 작은 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(v => v < 0); // false
```

forEach, map, fillter 메소드와 마찬가지로 some 메소드는 두번째 인수로 some 메소드 내부에서 사용할 this 객체를 전달할 수 있다.

&nbsp;  

### 9.7. Array.prototype.every

every 메소드는 배열을 순회하며 각 요소에 대해 인수로 전달된 콜백 함수를 호출한다. 이때 every 메소드는 콜백 함수의 반환값이 모두 참이면 true, 한번이라도 거짓이면 false를 반환한다. 즉, 배열의 모든 요소가 콜백 함수를 통해 정의한 조건을 모두 만족하는지 확인하여 그 결과를 불리언 타입으로 반환한다.

forEach, map, filter 메소드와 마찬가지로 every 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열(this)을 전달 받을 수 있다.

```javascript
// 배열의 모든 요소가 3보다 큰지 확인
[5, 10, 15].every(item => item > 3); // true

// 배열의 모든 요소가 10보다 큰지 확인
[5, 10, 15].every(item => item > 10); // false
```

forEach, map, filter 메소드와 마찬가지로 every 메소드에 두번째 인자로 every 메소드 내부에서 사용할 this 객체를 전달할 수 있다.

&nbsp;  

### 9.8. Array.prototype.find

ES6에서 새롭게 도입된 find 메소드는 배열을 순회하며 각 요소에 대해 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 **첫번째 요소**를 반환한다. 콜백 함수의 호출 결과가 true인 요소가 없다면 undefined를 반환한다.

forEach, map, filter 메소드와 마찬가지로 find 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열(this)을 전달 받을 수 있다.

```javascript
const users = [
  { id: 1, name: 'Kim' },
  { id: 2, name: 'Park' },
  { id: 3, name: 'Lee' }
];

// id가 2인 요소를 반환한다.
const result = users.find(item => item.id === 2);

// Array#find는 배열이 아니라 요소를 반환한다.
console.log(result); // { id: 2, name: 'Kim' }
```

forEach, map, filter 메소드와 마찬가지로 find 메소드에 두번째 인자로 find 메소드 내부에서 사용할 this 객체를 전달할 수 있다.

&nbsp;  

### 9.9. Array.prototype.findIndex

ES6에서 새롭게 도입된 findIndex 메소드는 배열을 순회하며 각 요소에 대해 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 **첫번째 요소의 인덱스**를 반환한다. 콜백 함수의 호출 결과가 true인 요소가 존재하지 않으면 -1을 반환한다.

forEach, map, filter 메소드와 마찬가지로 findIndex 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열(this)을 전달 받을 수 있다.

```javascript
const users = [
  { id: 1, name: 'Kim' },
  { id: 2, name: 'Lee' },
  { id: 3, name: 'Park' },
  { id: 4, name: 'Choi' },
];

// id가 2인 요소의 인덱스를 구한다.
users.findIndex(user => user.id === 2); // 1

// name이 'Park'인 요소의 인덱스를 구한다.
users.findIndex(user => user.name === 'Park'); // 3
```

forEach, map, filter 메소드와 마찬가지로 findIndex 메소드에 두번째 인자로 findIndex 메소드 내부에서 사용할 this 객체를 전달할 수 있다.

&nbsp;  

## 참고 자료

* [poiemaweb.com - 배열](https://poiemaweb.com/fastcampus/array)

