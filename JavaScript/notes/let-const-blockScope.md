# let, const와 블록 레벨 스코프

## 1. `var` 키워드로 선언한 변수의 문제점

### 1.1 변수 중복 선언 허용

### 1.2 함수 레벨 스코프

그 외 암묵적 **전역 변수**

### 1.3 변수 호이스팅



## `let` 키워드

### 2.1 변수 중복 선언 금지

```javascript
var foo = 123;
// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var foo = 456;

let bar = 123;
// let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
```



### 2.2 블록 레벨 스코프

```javascript
let foo = 123; // 전역 변수

{
  let foo = 456; // 지역 변수
  let bar = 456; // 지역 변수
}

console.log(foo); // 123
console.log(bar); // ReferenceError: bar is not defined
```



### 2.3 변수 호이스팅

`let` 키워드로 선언한 변수는 변수 호이스팅이 **발생하지 않는 것 처럼 동작한다.**

```javascript
let foo = 1; // 전역 변수

{
  console.log(foo); // ReferenceError: foo is not defined
  let foo = 2; // 지역 변수
}
```



### 2.4 전역 객체와 `let`

`var` 키워드로 선언한 변수는 `window`라는 전역 객체의 property로 저장된다. 반면, `let` 키워드로 선언한 전역 변수는 전역 객체 `window`의 property가 아니다.



## 3. `const` 키워드

### 3.1 선언과 초기화

`let` 키워드로 선언한 변수는 재할당이 자유로우나 **const 키워드로 선언한 변수는 재할당이 금지된다.**

```javascript
// 0.1은 변해서는 않되는 상수로서 사용될 값이다.
// 변수 이름을 대문자로 선언하여 상수를 저장하고 있음을 명확히 나타낸다.
const TAX_RATE = 0.1;

// const 키워드로 선언한 변수는 재할당이 금지된다.
// 상수는 재할당이 금지된 변수이다.
TAX_RATE = 0.2; // TypeError: Assignment to constant variable.
```

**`const` 키워드로 선언한 변수는 반드시 선언과 동시에 할당이 이루어져야 한다.**

```javascript
const FOO; // SyntaxError: Missing initializer in const declarationㅜ
```



### 3.2 상수

### 3.3 `const` 키워드와 객체

`const` 키워드로 선언된 변수에 할당된 객체는 변경이 가능하다.



### 4. `var` vs. `let` vs. `const`

- ES6를 사용한다면 var 키워드는 사용하지 않는다.
- 재할당이 필요한 경우에 한정해 let 키워드를 사용한다. 이때 변수의 스코프는 최대한 좁게 만든다.
- 변경이 발생하지 않는(재할당이 필요 없는 상수) 원시 값과 객체에는 const 키워드를 사용한다. const 키워드는 재할당을 금지하므로 var, let 보다 안전하다.

