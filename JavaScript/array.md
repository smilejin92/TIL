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

배열이 가지고 있는 값을 **요소(element)**라고 부른다. **자바스크립트의 모든 값은 배열의 요소가 될 수 있다.**

배열의 요소는 배열에서 **자신의 위치**를 나타내는 0 이상의 정수인 **인덱스(index)**를 갖는다. 인덱스는 배열의 요소에 접근할 때 사용한다. 대부분의 프로그래밍 언어에서 인덱스는 0부터 시작한다.

배열의 요소에 접근할 때는 대괄호 표기법을 사용한다. 대괄호 내에는 접근하고 싶은 요소의 인덱스를 지정한다.

```javascript
arr[0] // apple
arr[1] // banana
arr[2] // orange
```

배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 갖는다.

```javascript
arr.length // 3
```

배열은 인덱스와 **length 프로퍼티**를 갖기 때문에 for 문을 통해 **순차적으로 값에 접근**할 수 있다.

```javascript
// 배열의 순회
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

자바스크립트에 배열이라는 타입은 존재하지 않는다. **배열은 객체 타입이다.**

```javascript
typeof arr // object
```

배열은 배열 리터럴 또는 Array 생성자 함수로 생성할 수 있다. 두 경우 모두 배열의 생성자 함수는 Array이며 배열의 프로토타입 객체는 Array.prototype이다. Array.prototype은 배열을 위한 빌트인 메소드를 제공한다.

```javascript
const arr = [1, 2, 3];

arr.constructor === Array // true
Object.getPrototypeOf(arr) === Array.prototype // true
```

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

일반적으로 배열이라는 자료 구조의 개념은 **동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료 구조**를 말한다. 즉, 배열의 요소는 **하나의 타입**으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열은 **밀집 배열(dense array)**이라 한다.

<img src="https://user-images.githubusercontent.com/32444914/82526770-bf37c600-9b6f-11ea-974a-9bc12ed42164.png" width="60%" />

이처럼 자료 구조(data structure)에서 말하는 배열의 경우, 각 요소는 동일한 크기를 가지며 빈틈없이 연속적으로 이어져 있으므로 인덱스를 통해 단 한번의 연산으로 임의의 요소에 접근(random access, O(1))할 수 있다. 이는 매우 효율적이며 고속으로 동작한다.

> 검색 대상 요소의 메모리 주소 = 배열의 시작 메모리 주소 + 인덱스 * 요소의 바이트 수

예를 들어, 위 그림처럼 메모리 주소 1000에서 시작하고 각 요소의 크기가 8byte인 배열을 생각해 보자.

* 인덱스가 0인 요소의 메모리 주소: 1000 + 0 * 8 = 1000
* 인덱스가 1인 요소의 메모리 주소: 1000 + 1 * 8 = 1008
* 인덱스가 2인 요소의 메모리 주소: 1000 + 2 * 8 = 1016

이처럼 **배열은 인덱스를 통해 효율적으로 요소에 접근할 수 있다는 장점이 있다.** 하지만 정렬되지 않은 배열에서 특정한 값을 검색하는 경우, 모든 배열 요소를 처음부터 값을 발견할 때까지 차례대로 선형 검색(O(n))해야 한다.

또한 **배열에 요소를 삽입하거나 삭제하는 경우**, 배열 요소를 연속적으로 유지하기 위해 요소를 이동시켜야 하는 **단점**도 있다.

<img src="https://user-images.githubusercontent.com/32444914/82527158-b267a200-9b70-11ea-8370-3eabbafa4d27.png" width="60%" />

자바스크립트의 배열은 지금까지 살펴본 자료 구조에서 말하는 일반적이 의미의 배열과 다르다. 즉, 배열의 요소를 위한 각각의 메모리 공간은 동일할 크기를 갖지 않을 수 있으며, 연속적으로 이어져 있지 않을 수도 있다. 배열의 요소가 연속적으로 이어져 있지 않는 배열을 **희소 배열(sparse array)**이라 한다.

이처럼 자바스크립트의 배열은 엄밀히 말해 일반적 의미의 배열이 아니다. **자바스크립트의 배열은 일반적인 배열의 동작을 흉내낸 특수한 객체이다.**

```javascript
console.log(Object.getOwnPropertyDescriptors([1, 2, 3]));
/*
{
	'0': {value: 1, writable: true, enumerable: true, configurable: true}
  '1': {value: 2, writable: true, enumerable: true, configurable: true}
  '2': {value: 3, writable: true, enumerable: true, configurable: true}
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
* 희소 배열은 length와 배열 요소의 개수가 일치하지 않는다.
* **배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.**

&nbsp;  

length 프로퍼티는 요소의 개수, 즉 **배열의 길이**를 나타내는 정수를 값으로 가진다. 빈 배열일 경우 length 프로퍼티의 값은  0이며, 빈 배열이 아닐 경우 가장 큰 인덱스에 1을 더한 것과 같다.

```javascript
[].length // 0
[1, 2, 3].length // 3
```

length 프로퍼티의 값은 0과 2^32 미만의 양의 정수이다. 즉, 배열은 요소를 최대 2^32 - 1개 가질 수 있다. 따라서 배열에서 사용할 수 있는 가장 작은 인덱스는 0이며 가장 큰 인덱스는 2^32 - 2이다.

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

length 프로퍼티의 값은 요소의 개수를 바탕으로 결정되지만, 임의의 숫자 값을 명시적으로 할당할 수도 있다.

```javascript
const arr = [1, 2, 3, 4, 5];

// length 프로퍼티에 현재 length 프로퍼티 값보다 작은 숫자 값을 할당
arr.length = 3;

// 배열의 길이가 줄어든다.
console.log(arr); // [1, 2, 3]
```

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

존재하지 않는 요소에 접근하면 undefined가 반환된다.

```javascript
const arr = [1, 2];

// 인덱스가 2인 요소를 참조
// 배열 arr에 인덱스가 2인 요소는 존재하지 않는다.
console.log(arr[2]); // undefined
```

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

만약 **현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 된다.**

```javascript
arr[100] = 100;

console.log(arr); // [0, 1, empty * 98, 100]
console.log(arr.length); // 101
```

이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.

```javascript
// 요소값의 갱신
arr[1] = 10;

console.log(arr); // [0, 10, empty * 98, 100]
```

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



배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 `delete` 연산자를 사용할 수 있다.

```javascript
const arr = [1, 2, 3];

// 배열 요소의 삭제
delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
console.log(arr.length); // 3
```

`delete` 연산자는 객체의 프로퍼티를 삭제한다. 따라서 위 예제의 `delete arr[1]`은 arr에서 프로퍼티 키가 `'1'`인 프로퍼티를 삭제한다. 이때 배열은 희소 배열이 되며 length 프로퍼티 값은 변하지 않는다. 따라서 희소 배열을 만드는 `delete` 연산자는 사용하지 않는 것이 좋다.

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

배열 메소드는 결과물을 반환하는 패턴이 2가지이므로 주의가 필요하다. 배열에는 **원본 배열을 직접 변경하는 메소드(mutator)**와 원본 배열을 직접 변경하지 않고 **새로운 배열 생성하여 반환하는 메소드(accessor)**가 있다.

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

| 메소드                                   | 요약                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| Array.isArray(value)                     | value가 배열이면 true, 아니면 false를 반환                   |
| Array.prototype.indexOf(value, startIdx) | * 배열에 value가 있는 경우, 해당 요소의 인덱스를 반환(중복되는 요소가 있는 경우, 첫번째 인덱스를 반환).<br />* 배열에 value가 없는 경우 -1을 반환.<br />* startIdx는 검색을 시작할 인덱스이며, 생략 가능하다. |
|                                          |                                                              |

























