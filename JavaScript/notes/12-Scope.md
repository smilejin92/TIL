# Scope

## 1. 스코프란?

- 유효범위, 생명주기
- **모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다.**
- **식별자를 검색할 때 사용하는 규칙**
- `var` 키워드로 선언한 변수는 같은 스코프 내에서 중복 선언이 허용된다. 의도치 않은 부작용을 발생시킨다.
- `let`과 `const`로 선언된 변수는 같은 스코프 내에서 중복 선얼을 **허용하지 않는다.**



## 2. 스코프의 종류

코드는 전역(global)과 지역(local)으로 구분할 수 있다.

| 구분 | 설명                  | 스코프      | 변수      |
| ---- | --------------------- | ----------- | --------- |
| 전역 | 코드의 가장 바깥 영역 | 전역 스코프 | 전역 변수 |
| 지역 | 함수 몸체 내부        | 지역 스코프 | 지역 변수 |

변수는 자신이 선언된 위치(전역 또는 지역)에 의해 자신이 유효한 범위인 스코프가 결정된다.



### 2.1 전역과 전역 스코프

* 전역 변수는 어디서든지 참조할 수 있다.



### 2.2 지역과 지역 스코프

* 함수 몸체 내부
* 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효하다.
* 같은 이름의 식별자가 있으면 자바스크립트 엔진은 환경에 맞게 해석한다.



## 3. 스코프 체인

* 함수는 중첩될 수 있으므로 함수의 지역 스코프도 중첩될 수 있다.
* **스코프는 함수의 중첩에 의해 계층적 구조 (스코프 체인)를 갖는다**
  * 변수를 참조할 때, 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.
* 렉시컬 환경
  * 스코피 체인은 렉시컬 환경을 단방향으로 연결한 것이다.
* 식별자를 검색하는 규칙



## 4. 스코프 체인에 의한 변수 검색

* 상위 스코프에서 유효한 변수는 하위 스코프에서 자유롭게 참조할 수 있지만 하위 스코프에서 유효한 변수를 상위 스코프에서 참조할 수 없다.



## 5. 스코프 체인에 의한 함수 검색

* 함수 이름과 동일한 이름의 변수에 함수를 할당하는 것 외에는 별 다른 점이 없다.
* 변수의 스코프와 똑같이 작용한다.



## 6. 함수 레벨 스코프

* **자바스크립트에서는 `var` 키워드로 변수를 생성하면, 코드 블록이 아닌 함수에 의해서만 지역 스코프가 생성된다 (if..else, for, while, try/catch 같은 블록문에서는 생성되지 않는다) **. 이를 **함수 레벨 스코프**라 한다.
* ES6에서 도입된 let, const 키워드는 블록 레벨 스코프를 지원한다 (`var` 제외).

``` javascript
var x = 1;

if (true) {
  // var 키워드로 선언된 변수는 함수의 코드 블록 만을 지역 스코프로 인정한다.
  // 함수 밖에서 선언된 변수는 코드 블록 내에서 선언되었다 할 지라도 모두 전역 변수이다.
  // 따라서 x는 전역 변수이다. 이미 선언된 전역 변수 x가 있으므로 변수 x는 중복 선언된다.
  // 이는 의도치 않게 변수값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}

console.log(x); // 10

var i = 10;

// for문에서 선언한 i는 전역 변수이다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i < 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// 의도치 않게 변수의 값이 변경되었다.
console.log(i); // 5
```



## 7. 렉시컬 스코프

1. **함수를 어디서 호출**했는지에 따라 함수의 상위 스코프를 결정한다. (동적 스코프)
2. **함수를 어디서 정의**했는지에 따라 함수의 상위 스코프를 결정한다. (정적 스코프 - 렉시컬 스코프)

자바스크립트를 비롯한 대부분의 프로그래밍 언어는 **렉시컬 스코프를 따른다.** 즉, 자바스크립트는 **함수를 어디서 호출했는지가 아니라 어디에 정의했는지에 따라 상위 스코프를 결정한다.** 모든 함수 정의는 평가되어 함수 객체를 생성할 때, 자신이 정의된 스코프 (렉시컬 환경)를 기억한다. 그리고 함수가 호출되면 언제나 자신이 정의된 스코프와 상위 스코프를 사용한다.

```javascript
var x = 1;

function foo() {
  var x = 10;
  // bar 함수를 foo 함수 내에서 호출했지만, bar는 전역에서 정의되었기 때문에 x를 전역에 정의된 x로 인식한다
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```



> **렉시컬 환경과 함수 객체의 내부 슬롯 [[Environment]]**
>
> 정확히 말하자면 함수 객체가 기억하는 것은 렉시컬 환경(Lexical Envrionment)이다. 함수 정의가 평가되어 함수 객체를 생성할 때, 자신이 정의된 렉시컬 환경을 생성한 함수 객체의 내부 슬롯 [[Environment]]에 저장한다. 렉시컬 환경은 자바스크립트 엔진이 식별자와 스코프를 관리하기 위해 사용하는 일종의 자료 구조로서 스코프를 구분하여 식별자를 등록하고 관리하는 저장소 역할을 한다.



## 8. 암묵적 전역 변수

```javascript
function foo() {
  // 선언하지 않은 변수에 값을 할당하면 암묵적 전역 변수가 된다.
  x = 10;
}

foo(); // 호출 시 foo 함수 내의 x를 var로 선언하여 전역 변수로 취급

console.log(x); // 10
```

**선언하지 않은 변수에 값을 할당하면 자바스크립트 엔진은 아무런 에러 없이 암묵적으로 전역 변수를 선언하고 값을 할당한다.**

1. `foo` 호출
2.  `foo` 내에서 `x`의 선언을 탐색
3.  찾을 수 없으므로 전역 스코프로(종점) 이동
4.  `x`의 선언을 탐색 
5. 찾을 수 없으므로 **암묵적으로 x를 선언**



2개의 분리된 자바스크립트 파일이 있다고 가정하자.

```javascript
// x.js
function foo() {
  i = 0; // 암묵적 전역 변수
  // ...
}

// y.js
// var 키워드로 선언된 변수는 함수의 코드 블록 만을 지역 스코프로 인정한다.
// 따라서 for문에서 선언한 i는 전역 변수이다.
// 이미 암묵적 전역 변수 i가 있으므로 변수 i는 중복 선언된다.
for (var i = 0; i < 5; i++) {
  foo();
  console.log(i);
}
```

HTML에서 이 2개의 파일을 로드하면 변수 `i`는 중복된다.

```html
<!DOCTYPE html>
<html>
<body>
  <script src='x.js'></script>
  <script src='y.js'></script>
</body>
</html>
```

HTML에서 로드한 자바스크립트 파일은 여러 개로 분리되어 있다해도 **하나의 전역 스코프를 공유**한다. 다시 말해 **자바스크립트는 파일마다 독립적인 파일 스코프를 갖지 않는다.** 따라서 자바스크립트 파일을 여러 개로 분리하여도 결국 하나의 자바스크립트 파일로 통합된 것처럼 동작한다. 이러한 특징은 자바스크립트에 모듈이라는 개념이 없기 때문이다.

위 예제의 **x.js**와 **y.js**에 모두 변수 `i`가 존재한다. **x.js**의 변수 `i`는 암묵적 전역 변수이다. **y.js**의 변수 `i`는 `for` 문을 위한 변수이지만 `var` 키워드로 선언된 변수는 블록 레벨 스코프를 따르지 않으므로 전역 변수이다.

따라서 전역 변수 `i`는 중복되고 나중에 선언된 변수 `i`의 값이 먼저 선언된 변수 `i`의 값을 덮어쓰게 된다. 자바스크립트는 변수의 중복 선언을 허용하므로 어떠한 에러도 발생하지 않고 무한 반복 상태에 빠지게 된다.

