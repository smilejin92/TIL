# 클로저 (Closure)

클로저는 자바스크립트 고유의 개념이 아니다. 함수를 일급 객체로 취급하는 함수형 프로그래밍 언어(Functional Programming Language: 하스켈, 리스프, 얼랭, 스칼라 등)에서 사용되는 중요한 특성이다.

클로저는 자바스크립트 고유의 개념이 아니므로 ECMAScript 사양에 클로저의 정의가 등장하지 않는다. 클로저에 대해 MDN은 아래와 같이 정의하고 있다.

> "A closure is the combination of a function and the **lexical environment** within which that function was declared."
>
>
> 클로저는 함수와 그 함수가 선언된 **렉시컬 환경**과의 조합이다.



```javascript
const x = 1;

function outer() {
  const x = 10;
    
  function inner() {
    console.log(x);
  }
    
  inner();
}
outer(); // 10
```

함수 `outer` 내부에서 중첩 함수 `inner`가 정의되고 호출된다. 이때 중첩 함수 `inner`의 상위 스코프(OuterLexicalEnvironment)는 외부 함수 `outer`의 렉시컬 환경(LexicalEnvironment)이다. 따라서 중첩 함수 `inner` 내부에서 자신을 포함하는 외부 함수 `outer`의 변수 `x`를 스코프 체인을 따라 접근할 수 있다.

만약 함수 `inner`가 함수 `outer` 내부에서 정의된 중첩 함수가 아니라면 함수 `inner`를 함수 `outer` 내부에서 호출하여도 함수 `outer`의 변수에 접근할 수 없다 (두 함수 모두 OuterLexicalEnvironment가 전역을 가리킨다). 

```javascript
const x = 1;

function outer() {
  const x = 10;
  inner();
}

function inner() {
  console.log(x);
}
outer(); // 1
```

이와 같은 현상이 발생하는 이유는 자바스크립트가 렉시컬 스코프를 따르는 프로그래밍 언어이기 때문이다.

(질문. 책 본문의 위 예제 잘못돼있음)



## 1. 렉시컬 스코프

**자바스크립트는 함수를 어디서 호출했는지가 아니라 어디에 정의했는지에 따라 상위 스코프를 결정한다.** 이를 **렉시컬 스코프(정적 스코프)**라 한다.

```javascript
const x = 1;

function foo() {
  const x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

위 예제의 함수 `foo`와 함수 `bar`는 모두 전역에서 정의된 전역 함수이다. 함수의 상위 스코프는 함수를 어디서 정의했는지에 따라 결정되므로 함수 `foo`와 함수 `bar`의 상위 스코프는 전역이다. 함수를 어디서 호출하는지는 함수의 상위 스코프 결정에 어떠한 영향도 주지 못한다.

모든 실행 컨텍스트는 렉시컬 환경을 가지고 있고, 렉시컬 환경의 컴포넌트인 Outer Lexical Environment(외부 렉시컬 환경)에 상위 스코프에 대한 참조를 가지고 있으며, 이는 현재 자신(running execution context)을 평가하고 있는 렉시컬 환경이다. 함수의 경우, 함수 정의를 평가하는 렉시컬 환경(위 예제의 전역 환경)의 참조를 자신의 Outer Lexical Environment(상위 스코프)의 값으로 가지고 있으며 이것이 **렉시컬 스코프**이다.



## 2. 함수 객체의 내부 슬롯 [[Environment]]

함수는 자신이 호출되는 환경과는 상관없이 자신이 정의된 환경, 즉 상위 스코프(함수 정의가 위치하는 스코프)를 기억해야 한다. 이를 위해 **함수는 자신의 내부 슬롯 [[Environment]]에 자신이 정의된 환경, 즉 상위 스코프의 참조를 저장한다. 이때 저장된 상위 스코프의 참조는 Running execution context의 렉시컬 환경이다.**

함수 객체의 **내부 슬롯[[Environment]]**에 Running execution context의 렉시컬 환경의 참조가 저장되는 건 **함수가 평가될 때** 이루어지고, 함수 렉시컬 환경의 **Outer Lexical Environment**에 상위 스코프의 참조가 저장되는건 **함수가 호출될 때** 이루어진다.

```javascript
const x = 1;

function foo() {
  const x = 10;
  
  // 상위 스코프는 함수 정의 환경에 따라 결정된다.
  // 함수 호출 위치와 상위 스코프는 아무런 관계가 없다.
  bar();
}

// 함수 bar는 자신의 상위 스코프인 전역 렉시컬 환경을 기억한다.
function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\environment-internal-slot.png" style="zoom:50%;" />



## 3. 클로저와 렉시컬 환경

```javascript
const x = 1;

function outer() {
  const x = 10;
  const inner = function () {
    console.log(x);
  };
  return inner;
}

// 함수 outer를 호출하면 중첩 함수 inner를 반환한다
// 그리고 함수 outer의 실행 컨텍스트는 실행 컨텍스트 스택에서 pop된다.
const innerFunc = outer();
innerFunc(); // ?
```

**클로저를 이해하지 못한 경우**

함수 `outer`를 호출하면 함수 `outer`는 중첩 함수 `inner`를 반환하고 생명 주기를 마감한다. 즉, 함수 `outer`의 호출이 종료되었으므로 `outer` 실행 컨텍스트는 콜 스택에서 pop된다. 따라서 함수 `outer`의 지역 변수 `x`와 변수값 10을 저장하고 있던 `outer` 렉시컬 환경도 사라지므로 `outer`의 지역변수 `x`는 더 이상 유효하지 않게 되어 `x`를 참조할 수 있는 방법이 없다. 따라서 `innerFunc()`의 결과는 `ReferenceError`이다. 



**클로저를 이해한 경우**

함수 `outer`를 호출(3)하면 함수 `outer`는 중첩 함수 `inner`를 반환하고 생명 주기를 마감한다. 즉, 함수 `outer`의 호출이 종료되었으므로 `outer` 실행 컨텍스트는 콜 스택에서 pop된다. **하지만**, 함수 `outer`의 지역 변수 `x`와 변수 값 10을 저장하고 있던 `outer` **렉시컬 환경까지 소멸한 것은 아니다.** `inner` 함수 내부 슬롯 [[Environment]]에 `outer` 함수의 렉시컬 환경이 **참조되고 있으므로 가비지 컬렉션의 대상이 되지 않는다.** `innerFunc`의 내부 슬롯 [[Environment]] 값은 `innerFunc` 렉시컬 환경의 Outer Lexical Environment에 저장되어, 식별자 `x`를 스코프 체인 내에서 검색한다. 따라서 `innerFunc()`의 결과는 10이다.

이처럼 자신을 포함하고 있는 **외부 함수보다 중첩 함수가 더 오래 유지되는 경우**, 외부 함수 밖에서 중첩 함수를 호출하더라도 **외부 함수의 지역 변수에 접근할 수 있는** 함수를 **클로저(closure)**라 한다.

위 예제의 경우, `outer` 함수가 평가되어 함수 객체를 생성할 때 Running execution context의 렉시컬 환경을 `outer` 함수 객체의 [[Environment]] 내부 슬롯에 상위 스코프로서 저장한다.

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\closure-1.png" style="zoom:50%;" />





`outer` 함수를 호출하면 `outer` 함수의 렉시컬 환경이 생성되고 앞서 `outer` 함수 객체의 [[Environment]] 내부 슬롯에 저장된 전역 렉시컬 환경을 `outer` 렉시컬 환경의 Outer Lexical Environment에 할당한다.

그리고 중첩함수 `inner`가 평가되며 `inner`의 내부 슬롯 [[Environment]]에 Running execution context의 렉시컬 환경을 상위 스코프로서 저장한다.

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\closure-2.png" style="zoom:50%;" />





`outer` 함수의 실행이 종료되면 `inner` 함수를 반환하면서 `outer` 실행 컨텍스트는 콜 스택에서 pop된다. 이때 `outer` 렉시컬 환경은 **소멸되지 않는다.** `outer` 렉시컬 환경은 `inner` 함수의 내부 슬롯 [[Environment]]에 의해 참조되고 있으므로 가비지 컬렉션의 대상이 되지 않기 때문이다.

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\closure-3.png" style="zoom:50%;" />



`outer` 함수가 반환한 `inner` 함수를 호출하면 `inner` 실행 컨텍스트가 생성되고 콜 스택에 push된다. 그리고 `inner` 렉시컬 환경의 Outer Lexical Environment에 대한 참조에는 `inner` 함수 객체의 내부 슬롯 [[Environment]]의 값이 할당된다.

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\closure-4.png" style="zoom:50%;" />

중첩 함수 `inner`는 외부 함수 `outer`보다 더 오래 생존하였다. 이때 함수는 외부 함수 실행 컨텍스트의 유무와 상관 없이 자신이 정의된 위치에 의해 결정된 상위 스코프를 기억한다. 따라서, 중첩 함수의 내부에서 상위 스코프를 참조할 수 있으므로 상위 스코프의 식별자를 참조할 수 있고, 식별자의 값을 변경할 수도 있다.



이론적으로, 자바스크립트의 모든 함수는 상위 스코프를 기억하므로 클로저이다. 하지만 일반적으로 모든 함수를 클로저라고 하지는 않으며, **클로저가 되기 위해서는 두 가지 조건이 필요하다.**

1. **중첩 함수가 상위 스코프의 식별자를 참조해야한다.**
2. **중첩 함수가 외부 함수보다 더 오래 유지되어야 한다 (외부 함수가 중첩 함수를 반환한다).**

```javascript
function foo() {
  const x = 1;
  const y = 2;
    
  // 일반적으로 클로저라 하지 않는다
  function bar() {
    const z = 3;
    // 상위 스코프의 식별자를 참조하지 않는다.
    console.log(z);
  }
  return bar;
}

const bar = foo();
bar();
```

위 예제의 중첩 함수 `bar`는 상위 스코프의 어떤 식별자도 참조하지 않는다. 따라서 `bar` 함수는 클로저라 할 수 없다.



```javascript
function foo() {
  const x = 1;
    
  function bar() {
    console.log(x);
  }
  bar();
}
foo();
```

위 예제의 중첩 함수 `bar`는 상위 스코프의 식별자를 참조하고 있으므로 클로저이다. **하지만 외부 함수로부터 외부로 반환되지 않는다. 즉, 외부 함수와 생명 주기가 같다.** `bar`는 클로저였지만 외부 함수와 더불어 소멸되기 때문에 클로저라 하지 않는다. 



```javascript
function foo() {
  const x = 1;
  const y = 2;
  
  // 클로저
  function bar() {
    console.log(x);
  }
  return bar;
}

const bar = foo();
bar(); // 1
```

위 예제의 중첩 함수 `bar`는 상위 스코프의 식별자를 참조하며, 외부 함수 `foo`로부터 외부로 반환되어 외부 함수 `foo`보다 더 오래 살아 남는다. 따라서 클로저이다.

다만 클로저인 중첩 함수 `bar`는 상위 스코프의 식별자 `x`, `y` 중에서 `x`만을 참조하고 있다. 이런 경우, 대부분의 모던 브라우저는 최적화를 통해 상위 스코프의 식별자 중에서 **클로저가 참조하고 있는 식별자만을 기억한다.**

클로저에 의해 참조되는 상위 스코프의 변수를 **자유 변수(Free variable)**라고 부른다. 클로저(Closure)란 "자유 변수와 묶여있는 함수"라고 할 수 있다.



## 4. 클로저의 활용

**클로저는 상태를 안전하게 유지하기 위해 사용한다.** 즉, 상태가 의도치 않게 변경되지 않도록 안전하게 **은닉(Information hiding)**한다. 그리고 이전 상태를 기억하다가 상태가 변경되면 **최신 상태(state)를 유지**한다.

변수 값은 누군가에 의해 언제든지 변경될 수 있어 오류 발생의 근본적 원인이 될 수 있다. 상태 변경이나 가변(mutable) 데이터를 피하고 불변성(Immutability)을 지향하는 함수형 프로그래밍에서 부수 효과(Side effect)를 최대한 억제하여 오류를 피하고 프로그램의 안정성을 높이기 위해 클로저는 적극적으로 사용된다.

아래는 함수형 프로그래밍에서 클로저를 활용하는 간단한 예제이다.

```javascript
// 함수를 인수로 전달 받고 함수를 반환하는 고차 함수
// 이 함수가 반환하는 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저이다.
function makeCounter(predicate) {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;
    
  // 클로저를 반환
  return function () {
    // 인수로 전달 받은 보조 함수에 상태 변경을 위임한다.
    counter = predicate(counter);
    return counter;
  };
}

// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// 함수로 함수를 생성한다.
// makeCounter 함수는 보조 함수를 인수로 전달 받아 함수를 반환한다.
const increaser = makeCounter(increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// increaser 함수와는 별개의 독립된 렉시컬 환경을 갖기 때문에 카운터 상태가 연동되지 않는다.
const decreaser = makeCounter(decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```

**함수 `makeCounter`를 호출해 함수를 반환할 때 반환된 함수는 자신만의 독립된 렉시컬 환경을 갖는다.** 이는 함수를 호출하면 그때마다 새로운 `makeCounter` 실행 컨텍스트의 렉시컬 환경이 생성되기 때문이다. 

1. `increaser` 변수에 `makeCounter(increase)`를 할당할 때 `makeCounter` 함수가 호출되어 `makeCounter` 실행 컨텍스트가 생성된다.
2. `makeCounter` 함수는 인수로 전달받은 보조 함수를 사용하여 함수 객체를 생성하여 반환한 후 소멸된다.
3. `makeCounter` 함수가 반환한 함수는 변수 `increaser`에 할당된다.
4. `makeCounter` 실행 컨텍스트는 콜 스택에서 pop되었지만, `makeCounter` 렉시컬 환경은 3에서 반환한 함수의 내부 슬롯 [[Environment]]에 의해 참조되어 있기 때문에 `makeCounter` 렉시컬 환경은 소멸되지 않는다.

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\closure-5.png" style="zoom:50%;" />



5. `decreaser` 변수에 `makeCounter(decrease)`를 할당할 때 `makeCounter` 함수가 호출되어 `makeCounter` 실행 컨텍스트가 **다시 생성된다.**
6. `makeCounter` 함수는 인수로 전달받은 보조 함수를 사용하여 함수 객체를 생성하여 반환한 후 소멸된다.
7. `makeCounter` 함수가 반환한 함수는 변수 `decreaser`에 할당된다.
8. `makeCounter` 실행 컨텍스트는 콜 스택에서 pop되었지만, `makeCounter` 렉시컬 환경은 7에서 반환한 함수의 내부 슬롯 [[Environment]]에 의해 참조되어 있기 때문에 `makeCounter` 렉시컬 환경은 소멸되지 않는다.

<img src="C:\Users\Jinhyun Kim\Documents\dev\TIL\JavaScript\notes\images\closure-6.png" style="zoom:50%;" />



위 예제에서 변수 `increaser`와 `decreaser`에 할당된 함수는 **독립된 렉시컬 환경**을 갖기 때문에 카운트를 유지하기 위한 자유 변수 `counter`를 공유하지 않아 카운터의 증감이 연동되지 않는다. **렉시컬 환경을 공유하는 클로저를 만들기 위해 `makeCounter` 함수를 한번만 호출한다.**

```javascript
// 함수를 반환하는 고차 함수
// 이 함수가 반환하는 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저다.
const count = (function () {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;
    
  // 함수를 인수로 전달 받는 클로저를 반환
  return function (predicate) {
    // 인수로 전달 받은 보조 함수에 상태 변경을 위임한다.
    counter = predicate(counter);
    return counter;
  }
}());

// 보조 함수
function increase(n) {
  return ++n;
}

function decrease(n) {
  return --n;
}

// 보조 함수를 전달하여 호출
console.log(counter(increase)); // 1
console.log(counter(increase)); // 2

// 자유 변수를 공유한다
console.log(counter(decrease)); // 1
console.log(counter(decrease)); // 0
```







자바스크립트의 모든 함수는 클로저이다. 하지만 두 가지 조건을 성립하는 함수만 클로저라 부른다.

* 중첩 함수가 상위 함수보다 오래 살아남거나 (상위 함수가 중첩 함수를 리턴할때)

* 중첩 함수가 상위 함수의 식별자를 바라보는 경우 (상위 함수의 스코프 내의 변수를 가리킬 때)

자유 변수 = 유지해야하는 상태

