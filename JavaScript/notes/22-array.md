# 배열

## 1. 배열이란?

* 순서가 있는 값들의 연속적인 나열
* 자료구조
* **객체**

**사용 이유**: 순서가 있는 여러 개의 값을 하나의 자료 구조로 묶어 관리하기 위함

**장점**: 하나의 변수에 여러 개의 값을 저장할 수 있다.

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
const arr = [1, 2, 3];

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

따라서 자바스크립트의 배열은 엄밀히 말해 일반적 의미의 배열이 아니다.

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
객체의 프로퍼티를 인덱스(프로퍼티 키)와 요소(값)으로 가지고 있다.
*/
```

자바스크립트 배열은 **인덱스를 프로퍼티 키로 갖으며 `length` 프로퍼티를 갖는 특수한 객체이다.**

| 밀집 배열                                            | 희소 배열                                                    |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| 인덱스로 배열 요소에 빠르게 접근할 수 있다.          | 인덱스로 배열 요소에 접근할 때 성능적인 면에서 일반적인 배열보다 느릴 수 밖에 없다. |
| 요소를 삽입하거나 삭제하는 경우에는 효율적이지 않다. | 요소를 삽입하거나 삭제하는 경우 일반적인 배열보다 빠르다.    |

해시 테이블로 구현되어 있지만, 임의 접근 속도가 느린 구조적 문제를 해결하기 위해 브라우저 제조사에서 최적화를 진행하여 일반 객체에 비해 임의 접근 속도를 약 2배 빠르게 구현하였고, 성능상 일반 배열보다 임의 접근 속도가 느리지 않다.



## 3. `length` 프로퍼티와 희소 배열

`length` 프로퍼티는 요소의 개수로 배열의 길이를 나타내는 정수를 값으로 갖는다.

```javascript
[].length // 0
[1, 2, 3].length // 3
```

`length` 프로퍼티의 값은 0과 2^32 -1 미만의 양의 정수이다. 



`length` 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.

```javascript
const arr = [1, 2, 3];

console.log(arr.length); // 3

arr.push(4); // [1, 2, 3, 4]
console.log(arr.length); // 4

arr.pop(); // [1, 2, 3]
console.log(arr.length); // 3
```



`length` 프로퍼티의 값은 요소의 개수를 바탕으로 결정되지만 임의의 숫자 값을 명시적으로 할당할 수도 있다.

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

느려진다. 실질적인 배열의 길이와 `length` 프로퍼티의 값을 일치시키며 같은 데이터 타입만을 담아 사용하는 것이 바람직하다.



## 4. 배열 생성

### 4.1 배열 리터럴

배열에 무엇이 들어갈지 알고 있다는 가정

```javascript
const arr = [1, 2, 3];
console.log(arr.length); // 0
```



### 4.2 Array 생성자 함수

인수를 어떻게 주느냐에 따라 생성 방법이 달라진다. 희소 배열이 만들어진다. 권장하지 않는다.



### 4.3 Array.of



### 4.4 Array.from

유사 배열, 이터러블을 인수로 받을 수 있다.

콜백 함수를 인수로 받을 수 있다.



## 5. 배열 요소의 참조

대괄호 표기법으로 인덱스로 참조

존재하지 않으면 undefined

희소 배열에 존재하지 않는 요소에 접근해도 undefined (객체에 프로퍼티 키가 없으면 undefined로)



## 6. 배열 요소의 추가와 갱신

프로퍼티 동적 추가와 비슷





## 7. 배열 요소의 삭제

delete 연산자 쓰지마라



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

