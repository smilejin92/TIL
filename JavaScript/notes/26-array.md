# 배열 (Array)

## 1. 배열이란?

* 순서가 있는 값들의 연속적인 나열
* 자료구조
* **객체**

**사용 이유**: 순서가 있는 여러 개의 값을 하나의 자료 구조로 묶어 관리하기 위함

**장점 **- `length` 프로퍼티가 있다

* 하나의 변수에 여러 개의 값을 저장할 수 있다.
* 처음부터 순차적으로 요소에 접근할 수 있다.
* 마지막부터 역방향으로 요소에 접근할 수 있다.
* 특정 위치부터 순차적으로 요소에 접근할 수 있다.

**요소(element)**: 배열이 가지고 있는 값. **자바스크립트에서 값으로 인정하는 모든 것은 배열의 요소가 될 수 있다.**

**인덱스(index)**: 각 요소가 자신의 위치를 나타내는 0 이상의 정수

**length**: 요소의 개수, 배열의 길이를 나타내는 프로퍼티

```javascript
const arr = ['apple', 'banana', 'orange'];
arr[0] // 'apple'
arr[1] // 'banana'
arr[2] // 'orange'

arr.length // 3
typeof arr // object
```



배열은 배열 리터럴 또는 Array 생성자 함수로 생성할 수 있다.

```javascript
const arr = [1, 2, 3]; // [1, 2, 3]
const arr2 = new Array(1, 2, 3); // [1, 2, 3]

arr.constructor === Array // true
Object.getPrototypeOf(arr) === Array.prototype // true
```



배열은 객체이지만 일반 객체와는 다른 독특한 특징이 있다.

| 구분            | 객체                      | 배열          |
| --------------- | ------------------------- | ------------- |
| 구조            | 프로퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
| 값의 참조       | 프로퍼티 키               | 인덱스        |
| 값의 순서       | X                         | O             |
| length 프로퍼티 | X                         | O             |

일반 객체와 배열을 구분하는 가장 명확한 차이는 **값의 순서**와 **`length` 프로퍼티**이다. 따라서 반복문을 통해 순차적으로 값에 접근하기 적합한 자료 구조이다.

```javascript
const arr = [1, 2, 3];

// 반복문으로 자료 구조를 순회하기 위해 length 프로퍼티를 사용한다.
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]); // 1 2 3
}
```



## 2. 자바스크립트 배열은 배열이 아니다.

일반적으로 배열이라는 자료 구조의 개념은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다. 배열의 요소는 하나의 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열을 **밀집 배열(Dense array)**이라 한다.

자바스크립트의 배열은 배열의 요소를 위한 각 메모리 공간이 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을 수도 있다. 배열의 요소가 연속적으로 이어져 있지 않는 배열을 **희소 배열(sparse array)**이라 한다.

따라서 자바스크립트의 배열은 엄밀히 말해 일반적 의미의 배열이 아니다. 자바스크립트의 배열은 일번적인 배열의 동작을 흉내낸 특수한 객체이다.

```javascript
const arr = [1, 2, 3];

console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '2': { value: 3, writable: true, enumerable: true, configurable: true },
  length: { value: 3, writable: true, enumerable: false, configurable: false }
}
키와 값의 쌍으로 이루어져 있다. 해시 함수를 이용한 해시 테이블로 구성되어있다.
객체의 프로퍼티를 인덱스(프로퍼티 키)와 요소(프로퍼티 값)으로 가지고 있으며,
length 프로퍼티를 갖는 특수한 객체이다.
*/
```

자바스크립트 배열은 **인덱스를 프로퍼티 키로 갖으며 `length` 프로퍼티를 갖는 특수한 객체이다.**

| 밀집 배열                                            | 희소 배열                                                    |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| 인덱스로 배열 요소에 빠르게 접근할 수 있다.          | 인덱스로 배열 요소에 접근할 때 성능적인 면에서 일반적인 배열보다 느릴 수 밖에 없다 (해시 테이블). |
| 요소를 삽입하거나 삭제하는 경우에는 효율적이지 않다. | 요소를 삽입하거나 삭제하는 경우 일반적인 배열보다 빠른 성능을 기대할 수 있다. |
| 특정 요소를 탐색하는 경우 효율적이지 않다.           | 특정 요소를 탐색하는 경우 일반 배열보다 빠른 성능을 기대할 수 있다. |

해시 테이블로 구현되어 있지만, 임의 접근 속도가 느린 구조적 문제를 해결하기 위해 브라우저 제조사에서 최적화를 진행하여 일반 객체에 비해 임의 접근 속도를 약 2배 빠르게 구현하였고, 성능상 일반 배열보다 임의 접근 속도가 느리지 않다.



## 3. `length` 프로퍼티와 희소 배열

`length` 프로퍼티는 요소의 개수로, 배열의 길이를 나타내는 정수를 값으로 갖는다.

```javascript
[].length // 0
[1, 2, 3].length // 3
```

`length` 프로퍼티의 값은 0과 2^32 -1 (약 43억) 미만의 양의 정수이다. 



`length` 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.

```javascript
const arr = [1, 2, 3];

console.log(arr.length); // 3

arr.push(4); // [1, 2, 3, 4]
console.log(arr.length); // 4

arr.pop(); // [1, 2, 3]
console.log(arr.length); // 3
```



`length` 프로퍼티의 값은 요소의 개수를 바탕으로 결정되지만 임의의 숫자 값을 **명시적으로 할당할 수도 있다.**

```javascript
const arr = [1, 2, 3, 4, 5];

// length 프로퍼티에 현재 length 프로퍼티 값보다 작은 숫자 값을 할당
arr.length = 3;

// 배열의 길이가 줄어든다.
console.log(arr); // [1, 2, 3]
```



주의할 것은 실질적인 배열을 길이보다 `length` 프로퍼티를 크게 할당하는 경우다. 이때 `length` 프로퍼티 값은 변경되지만 실제로 **배열의 길이가 늘어나지는 않는다.**

```javascript
const arr = [1];

// length 프로퍼티에 현재 length 프로퍼티 값보다 큰 숫자 값을 할당
arr.length = 3;

// length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.
console.log(arr.length); // 3
console.log(arr); // [1, empty * 2]

```

값이 없이 비어있는 요소를 위해 **메모리 공간을 확보하지 않으며 빈 요소를 생성하지도 않는다.**

```javascript
console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  length: { value: 3, writable: true, enumerable: false, configurable: false }
}
*/
```

이처럼 배열의 요소가 **연속적으로 위치하지 않고 일부가 비어있는 배열**을 **희소 배열**이라 한다. 희소 배열은 `length`와 배열 요소의 개수가 일치하지 않는다. 희소 배열의 `length`는 배열의 실제 요소 개수보다 언제나 크다.

배열을 생성할 경우에는 희소 배열을 생성하지 않도록 주의해야한다. 배열에는 **같은 타입**의 요소를 **연속적으로** 위치시키는 것이 최선이다.



## 4. 배열 생성

### 4.1 배열 리터럴

배열 리터럴은 0개 이상의 요소를 쉼표로 구분ㄴ하여 대괄호[]로 묶는다. 객체 리터럴과 달리 프로퍼티 이름이 없고 값만이 존재한다. 대부분의 경우 배열에 무엇이 들어 갈지 알고 있을 때 사용한다.

```javascript
const arr = [1, 2, 3];
console.log(arr.length); // 3

const arr2 = [];
console.log(arr2.length); // 0
```



배열 리터럴에 요소를 생략하면 희소 배열이 생성된다.

```javascript
const arr = [1, , 3]; // 희소 배열

// 희소 배열의 length는 배열의 실제 요소 개수보다 언제나 크다
console.log(arr.length); // 3
console.log(arr); // [1, empty, 3]
console.log(arr[1]); // undefined
```

위 예제의 배열은 인덱스가 1인 요소를 갖지 않는다. `arr[1]`이 `undefined`인 이유는 `arr`에 프로퍼티 키가 '1'인 프로퍼티가 존재하지 않기 때문이다.



### 4.2 Array 생성자 함수

`Array` 생성자 함수를 통해 배열을 생성할 수도 있다. `Array` 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작한다. 

**전달된 인수가 1개이고 숫자인 경우, `length` = 인수의 배열을 생성**

```javascript
const arr = new Array(10);

console.log(arr); // [empty * 10]
console.log(arr.length); // 10
```

희소 배열이 만들어진다. 권장하지 않는다. 



**전달된 인수가 2개 이상이거나 숫자가 아닌 경우, 인수를 요소로 갖는 배열을 생성**

```javascript
// 전달된 인수가 1개이지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성한다.
const arr1 = new Array('Jin');
console.log(arr1); // ['Jin']

// 전달된 인수가 2개 이상이면 인수를 요소로 갖는 배열을 생성
const arr2 = new Array(1, 2, 3);
console.log(arr2); // [1, 2, 3]
```



### 4.3 Array.of

ES6에 새롭게 도입된 `Array.of` 메소드는 **전달된 인수를 요소로 갖는 배열**을 생성한다.

```javascript
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성
const arr = Array.of(1);
console.log(arr); // [1]
```



### 4.4 Array.from

ES6에서 새롭게 도입된 `Array.from` 메소드는 유사 배열 객체(array-like-object) 또는 이터러블 객체(iterable object)를 변환하여 새로운 배열을 생성한다.

> **유사 배열 객체와 이터러블 객체**
>
> 유사 배열 객체(Array-like Object)는 마치 배열처럼 **인덱스로 프로퍼티 값에 접근할 수 있고 `length` 프로퍼티를 갖기 때문에 `for` 문으로 순회할 수도 있다.**

```javascript
// 문자열은 이터러블이다.
const arr1 = Array.from("Jin");
console.log(arr1); // ['J', 'i', 'n']

// 유사 배열 객체를 새로운 배열을 변환하여 반환한다.
const obj = {
  length: 2,
  0: 'a',
  1: 'b'
};
const objToArr = Array.from(obj);
console.log(objToArr); // ['a', 'b']
```



`Array.from`을 사용하면 두번째 인수로 전달한 **함수**를 통해 값을 만들면서 요소를 채울 수 있다. 두번째 인수로 전달한 함수는 **첫번째 인수에 배열의 요소 값, 두번째 인수에 인덱스**를 전달 받아 새로운 요소를 생성할 수 있다.

```javascript
// Array.from의 두번째 인수로 배열의 모든 요소에 대해 호출할 함수를 전달할 수 있다.
// 이 함수는 첫번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달받아 호출된다.
const name = 'Jin';
const arr3 = Array.from(name, (v, i) => `${v} ${i}`);

console.log(arr3); // ['J 0', 'i 1', 'n 2']

```



## 5. 배열 요소의 참조

배열 요소를 참조할 때는 대괄호[] 표기법을 사용한다. 대괄호 안에는 인덱스가 와야 한다. 정수로 평가되는 표현식이라면 인덱스로 사용할 수 있다. 인덱스는 값을 참조할 수 있다는 의미에서 객체의 **프로퍼티 키**와 같은 역할을 한다.

```javascript
const arr = [1, 2];

// 인덱스가 0인 요소를 참조
console.log(arr[0]); // 1

```

존재하지 않는 요소에 접근하면 `undefined`가 반환된다.

```javascript
const arr = [1, 2];

// 배열 arr에 인덱스가 2인 요소는 존재하지 않는다.
console.log(arr[2]); // undefined

```

**배열은 인덱스를 프로퍼티 키로 갖는 객체이다.** 따라서 존재하지 않는 프로퍼티 키로 객체의 프로퍼티에 접근했을 때 `undefined`를 반환하는 것처럼 배열도 존재하지 않는 요소를 참조하면 `undefined`가 반환된다. 같은 이유로 희소 배열의 존재하지 않는 요소를 참조하여도 `undefined`가 반환된다.



## 6. 배열 요소의 추가와 갱신

객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼 **배열에도 요소를 동적으로 추가할 수 있다.** 요소가 존재하지 않는 인덱스의 배열 요소에 값을 할당하면 새로운 요소가 추가된다. 이때 **`length` 프로퍼티 값은 자동 갱신된다.**

```javascript
const arr = [0];

// 배열 요소의 추가
arr[1] = 1;

console.log(arr); // [0, 1]
console.log(arr.length); // 2

arr[arr.length] = 2; // arr[2] = 2;
console.log(arr); // [0, 1, 2]
```



만약 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 된다.

```javascript
const arr = [0]; // [0]
console.log(arr.length); // 1

arr[100] = 100; // [0, empty * 99, 100]
console.log(arr.length); // 101

console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': { value: 0, writable: true, enumerable: true, configurable: true },
  '100': { value: 100, writable: true, enumerable: true, configurable: true },
  length: { value: 101, writable: true, enumerable: false, configurable: false }
*/
```



이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.

```javascript
const arr = [0, 1]; // [0, 1]
arr[0] = 1; // [1, 1]
```



배열도 객체이다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 **프로퍼티가 생성된다.** 이때 추가된 프로퍼티는 `length` 프로퍼티의 값에 영향을 주지 않는다.

```javascript
const arr = [];

// 배열 요소의 추가
arr[0] = 1;
arr['1'] = 2; // 정수로 치환된다.

// 프로퍼티 추가
arr['foo'] = 3;
arr[1.1] = 4;
arr[-1] = 5;

console.log(arr); // [1, 2, foo: 3, 1.1: 4, -1: 5]

// 프로퍼티는 length에 영향을 주지 않는다.
console.log(arr.length); // 2
```



## 7. 배열 요소의 삭제

배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 `delete` 연산자를 사용할 수 있다.

```javascript
const arr = [1, 2, 3];

// 배열 요소의 삭제
delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
console.log(arr.length); // 3
```

`delete` 연산자는 객체의 프로퍼티를 삭제한다. 따라서 위 예제의 `delete arr[1]`은 `arr`에서 프로퍼티 키가 '1'인 프로퍼티를 삭제한다. 이때 배열은 희소 배열이 되며 `length` 프로퍼티 값은 변하지 않는다. 따라서 희소 배열을 만드는 `delete` 연산자는 사용하지 않는 것이 좋다.



## 8. 배열 메소드

`this`를 변경하는 메소드 (mutator mehtod)

`this`를 읽고 새로운 배열을 리턴하는 (accessor method)

accessor method를 권장 (순수 함수)

### 8.1 `Array.isArray`

### 8.2 `Array.prototype.push`

### 8.3 `Array.prototype.pop`

### 8.4 `Array.prototype.unshift`

### 8.5 `Array.prototype.shift`

### 8.6 `Array.prototype.concat`

### 8.7 `Array.prototype.splice`

### 8.8 `Array.prototype.slice`

### 8.9 `Array.prototype.indexOf`

### 8.10 `Array.prototype.join`

### 8.11 `Array.prototype.reverse`

### 8.12 `Array.prototype.fill`

### 8.13 `Array.prototype.includes`



## 9. 배열 고차 함수

### 9.1 `Array.prototype.sort`

```javascript
const numbers = {1, 10, 2};

// 오름차순 (ascending) 정렬
numbers.sort();

// sort 메소드는 원본 배열을 직접 변경한다
console.log(numbers); // [1, 10, 2] ???

// 숫자는 유니코드로 변환되어 문자열로 정렬된다.
// 따라서 sort()에 비교 함수를 넣어 정렬 기준을 정의한다.
numbers.sort((a, b) => a - b);
// number.sort(function (a, b) { return a - b; });
console.log(numbers); // [1, 2, 10]
```

### 9.2 `Array.prototype.forEach`

`continue`, `break` 없이 끝까지 돈다

. 앞의 이터러블을 순회하면서 콜백함수를 실행한다.

### 9.3 `Array.prototype.map`

### 9.4 `Array.prototype.filter`

### 9.5 `Array.prototype.reduce`

### 9.6 `Array.prototype.some`

### 9.7 `Array.prototype.every`

### 9.8 `Array.prototype.find`

### 9.9 `Array.prototype.findIndex`

