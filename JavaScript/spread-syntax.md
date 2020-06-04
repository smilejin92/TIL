# 스프레드 문법

ES6에서 새롭게 도입된 스프레드 문법(Spread syntax; 전개 문법) `...`은 **하나로 뭉쳐 있는 여러 값들의 집합을 펼쳐서 개별적인 값들의 목록으로 만든다.**

스프레드 문법을 사용할 수 있는 대상은 Array, String, Map, Set, DOM 컬렉션(NodeList, HTMLCollection), Arguments와 같이 for...of 문으로 순회할 수 있는 **이터러블에 한정된다.**

```javascript
// 배열의 요소를 분리하여 값의 목록을 만든다. (1, 2, 3)
console.log(...[1, 2, 3]); // 1 2 3

// 문자열은 이터러블이다.
console.log(...'Hello'); // H e l l o

// Map과 Set은 이터러블이다.
console.log(...new Map([['a', 1], ['b', 2]])); // ['a', 1] ['b', 2]
console.log(...new Set([1, 2, 3])); // 1 2 3
```

&nbsp;  

위 예제에서 `...[1, 2, 3]`은 이터러블인 배열을 펼쳐서 요소값을 개별적인 값들의 목록 1, 2, 3으로 만든다. 이때 1 2 3은 값이 아니라 **값들의 목록이다.** 즉, **스프레드 문법의 결과는 값이 아니다. 따라서 스프레드 문법은 연산자가 아니다.** 따라서 스프레드 문법의 결과를 변수에 할당할 수 없다.

```javascript
const arr = [1, 2, 3];
const list = ...arr; // SyntaxError
```

&nbsp;  

이처럼 스프레드 문법의 결과물은 값으로 사용할 수 없고, 아래와 같이 **쉼표로 구분한 값의 목록을 사용하는 문맥에서만 사용할 수 있다.**

* 함수 호출문의 인수 목록
* 배열 리터럴의 요소 목록
* 객체 리터럴의 프로퍼티 목록 (2020년 3월 Stage 4 제안)

&nbsp;  

## 1. 함수 호출문의 인수 목록에서 사용하는 경우

요소 값들의 집합인 배열을 펼쳐서 개별적인 값들의 목록으로 만든 후, 이를 **함수 인수 목록으로 전달해야 하는 경우가 있다.**

```javascript
const arr = [1, 2, 3];

// 배열 arr의 요소 중 최대값을 구하기 위해 Math.max를 사용한다.
const max = Math.max(arr); // NaN
```

만약 `Math.max` 메소드에 숫자가 아닌 배열을 인수로 전달하면 최대값을 구할 수 없으므로 `NaN`을 반환한다.

이와 같은 문제를 해결하기 위해 배열 `[1, 2, 3]`을 1, 2, 3으로 펼쳐서 `Math.max` 메소드의 인수로 전달해야 한다.

```javascript
// ES6
const arr = [1, 2, 3];
const max = Math.max(...arr); // 3

// 스프레드 문법이 제공되기 이전에는 배열을 펼쳐서 요소값의 목록을 함수의 인수로 전달하고
// 싶은 경우 Function.prototype.apply를 사용했다.
var arr2 = [1, 2, 3];
var max2 = Math.max.apply(null, arr); // 3
```

&nbsp;  

### **&ast;&ast;주의사항&ast;&ast;**

스프레드 문법은 Rest 파라미터와 형태가 동일하여 혼동할 수 있으므로 주의가 필요하다.

* Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받기 위해 매개변수 이름 앞에 `...`을 붙이는 것이다.
* 스프레드 문법은 여러 개의 값이 하나로 뭉쳐 있는 이터러블을 펼쳐서 개별적인 값들의 목록을 만드는 것이다.

&nbsp;  

따라서 **Rest 파라미터와 스프레드 문법은 서로 반대의 개념이다**.

&nbsp;  

## 2. 배열 리터럴 내부에서 사용하는 경우

### 2.1. concat

ES5에서 **기존의 배열 요소들을 새로운 배열의 일부로 만들고 싶은 경우**, 배열 리터럴 만으로 해결할 수 없고 `concat` 메소드를 사용해야 한다.

```javascript
// ES5
var arr = [1, 2].concat([3, 4]);
console.log(arr); // [1, 2, 3 ,4]
```

스프레드 문법을 사용하면 별도의 메소드를 사용하지 않고 배열 리터럴 만으로 기존의 배열 요소들을 새로운 배열의 일부로 만들 수 있다.

```javascript
// ES6
const arr = [...[1, 2], ...[3, 4]];
console.log(arr); // [1, 2, 3, 4]
```

&nbsp;  

### 2.2. push

ES5에서 **기존의 배열에 다른 배열의 요소들을 push하는 경우** 아래와 같은 방법을 사용한다.

```javascript
// ES5
var arr1 = [1, 2];
var arr2 = [3, 4];

Array.prototype.push.apply(arr1, arr2);
// arr1.push(3, 4);

console.log(arr1); // [1, 2, 3, 4]
```

스프레드 문법을 사용하면 아래와 같이 보다 간편하게 표현할 수 있다.

```javascript
// ES6
const arr1 = [1, 2];
const arr2 = [3, 4];

arr1.push(...arr2);

console.log(arr1); // [1, 2, 3, 4]
```

원본 배열을 직접 수정하는 push 메소드를 사용하는 것보다 스프레드 문법을 사용하는 것이 바람직하다.

```javascript
// ES6
const arr1 = [1, 2];
const arr2 = [3, 4];

arr1 = [...arr1, ...arr2];
console.log(arr1); // [1, 2, 3, 4]
```

&nbsp;  

### 2.3 splice

ES5에서 **기존의 배열에 다른 배열의 요소들을 삽입하는 경우** splice 메소드를 사용한다.

```javascript
// ES5
var arr1 = [1, 4];
var arr2 = [2, 3];

// apply 메소드의 2번째 인수는 배열이다. 이것은 인수 목록으로 splice 메소드에 전달된다.
Array.prototype.splice.apply(arr1, [1, 0].concat(arr2));
// Array.prototype.splice.apply(arr1, [1, 0, 2, 3])

console.log(arr1); // [1, 2, 3, 4]
```

스프레드 문법을 사용하면 아래와 같이 보다 간편하게 표현할 수 있다.

```javascript
// ES6
const arr1 = [1, 4];
const arr2 = [2, 3];

arr1.splice(1, 0, ...arr2);

console.log(arr1); // [1, 2, 3, 4]
```

&nbsp;  

### 2.4. 배열 복사

ES5에서 **기존의 배열을 (얕은) 복사하는 경우** slice 메소드를 사용한다.

```javascript
// ES5
var origin = [1, 2];
var copy = origin.slice();

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```

스프레드 문법을 사용하면 보다 간편하게 배열을 (얕은) 복사할 수 있다.

```javascript
// ES6
const origin = [1, 2];
const copy = [...origin];

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```

&nbsp;  

### 2.5. 이터러블을 배열로 변환

**이터러블을 배열로 변환하는 경우** slice 메소드를 apply 함수로 호출하는 것이 일반적이다.

```javascript
// ES5
function sum() {
  // 이터러블이면서 유사 배열 객체인 arguments를 배열로 변환
  var args = Array.prototype.slice.apply(arguments);
  
  return args.reduce(function (pre, cur) {
    return pre + cur;
  }, 0);
}

console.log(sum(1, 2, 3)); // 6
```

스프레드 문법을 사용하면 보다 간편하게 이터러블을 배열로 변환할 수 있다. arguments 객체는 이터러블이면서 유사 배열 객체이다. 따라서 스프레드 문법의 대상이 될 수 있다.

```javascript
// ES6
function sum() {
  // 이터러블이면서 유사 배열 객체인 arguments를 배열로 변환
  return [...arguments].reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2, 3)); // 6
```

&nbsp;  

## 3. 객체 리터럴 내부에서 사용하는 경우

Rest 프로퍼티와 함께 2020년 5월 TC39 프로세스의 stage 4(Finished) 단계에 제안되어 있는 스프레드 프로퍼티를 사용하면 **객체 리터럴의 프로퍼티 목록에서도 스프레드 문법을 사용할 수 있다.**

스프레드 문법의 대상은 이터러블이어야 하지만 스프레드 프로퍼티 제안은 **일반 객체를 대상으로도 스프레드 문법의 사용을 허용한다.**

```javascript
// 스프레드 프로퍼티
// 객체 복사(얕은 복사)
const obj = { x: 1, y: 2 };
const copy = { ...obj };

console.log(copy); // { x: 1, y: 2 }
console.log(obj === copy);

// 객체 병합
const merged = { ...obj, ...{ a: 3, b: 4 } };
console.log(merged); // { x: 1, y: 2, a: 3, b: 4 };
```

&nbsp;  

스프레드 프로퍼티가 제안되기 이전에는 ES6에서 도입된 `Object.assign` 메소드를 사용하여 여러 개의 객체를 병합하거나 특정 프로퍼티를 변경 또는 추가하였다.

```javascript
// 객체의 병합
// 프로퍼티가 중복되는 경우, 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = Object.assign({}, { x: 1, y: 2 }, { y: 10, z: 3 });
// Object.assign에 전달한 객체는 우측에서 좌측으로 merge된다.
console.log(merged); // { x: 1, y: 10, z: 3 }

// 특정 프로퍼티 변경
const changed = Object.assign({}, { x: 1, y: 2 }, { y: 100 });
console.log(changed); // { x: 1, y: 100 }

// 프로퍼티 추가
const added = Object.assign({}, { x: 1, y: 2 }, { z: 0 });
console.log(added); // { x: 1, y: 2, z: 0 }
```

&nbsp;  

스프레드 프로퍼티는 `Object.assign` 메소드를 대체할 수 있는 간편한 문법이다.

```javascript
// 객체의 병합
// 프로퍼티가 중복되는 경우, 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = { ...{ x: 1, y: 2 }, ...{ y: 10, z: 3 } };
console.log(merged); // { x: 1, y: 10, z: 3 }

// 특정 프로퍼티 변경
const changed = { ...{ x: 1, y: 2 }, ...{ y: 100 } };
console.log(changed); // { x: 1, y: 100 }

// 프로퍼티 추가
const added = { ...{ x: 1, y: 2 }, ...{ z: 0 } };
console.log(added); // { x: 1, y: 2, z: 0 }
```

&nbsp;  

## 출처

* [poiemaweb.com - 스프레드 문법](https://poiemaweb.com/fastcampus/spread-syntax)

