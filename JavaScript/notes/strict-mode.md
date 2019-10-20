# 엄격 모드

## 1. Strict Mode란?

Strict Mode는 자바스크립트 언어의 문법을 보다 엄격히 적용하여 기존에는 무시되던 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.



## 2. Strict Mode의 적용

전역의 선두 또는 함수 몸체의 선두에 `use strict;`를 추가한다. 전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

```javascript
'use strict';

function foo() {
  x = 10; // ReferenceError: x is not defined
}
```



함수 몸체의 선두에 추가하면 해당 함수와 중첩된 내부 함수에 strict mode가 적용된다.

```javascript
function foo() {
  'use strict';
  
  x = 10; // ReferenceError: x is not defined 
}
```



## 3. 전역에 strict mode를 적용하는 것은 피하자.

non-strict mode 스크립트를 혼용하는 것은 오류를 발생시킬 수 있다. 특히 외부 third-party 라이브러리를 사용하는 경우, 라이브러리가 non-strict mode일 경우도 있기 때문에 전역에 strict mode를 적용하는 것은 바람직하지 않다.



## 4. 함수 단위로 strict mode를 적용하는 것도 피하자.

어떤 함수는 strict mode를 적용하고 어떤 함수는 strict mode를 적용하지 않는 것은 바람직하지 않으며 모든 함수에 일일이 strict mode를 적용하는 것은 번거로운 일이다. 또한, strict mode가 적용된 함수가 참조할 함수 외부의 컨텍스트에 strict mode를 적용하지 않는다면 이 또한 문제가 발생할 수 있다.

**따라서 strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.**



## 5. strict mode가 발생시키는 에러

* 선언하지 않은 변수를 참조하면 `ReferenceError`가 발생한다.
* `delete` 연산자로 변수, 함수, 매개변수를 삭제하면 `SyntaxError`가 발생한다.
* 중복된 함수 매개변수 이름을 사용하면 `SyntaxError`가 발생한다.
* `with` 문을 사용하면 `SyntaxError`가 발생한다.



## 6. strict mode 적용에 의한 변화

* strict mode에서 함수를 일반함수로서 호출하면 `this`에 `undefined`가 바인딩된다. 
* 함수의 매개변수에 전달된 인수를 재할당하여도 arguments 객체에 반영되지 않는다.

