# 클로저

* 클로저는 함수와 그 함수가 선언된 렉시컬 환경의 조합이다.

&nbsp;  

클로저는 자바스크립트 고유의 개념이 아니다. 함수를 일급 객체로 취급하는 함수형 프로그래밍 언어(funtional programming language: 하스켈, 리스프, 얼랭, 스칼라 등)에서 사용되는 중요한 특성이다.

클로저는 자바스크립트 고유의 개념이 아니므로 클로저의 정의가 ECMAScript 사양에 등장하지 않는다. 클로저에 대해 MDN은 아래와 같이 정의하고 있다.

&nbsp;  

> "A closure is the combination of a function and the lexical environment within which that function was declared."
>
> 클로저는 함수와 그 함수가 선언된 **렉시컬 환경**과의 조합이다.

&nbsp;  

```javascript
const x = 1;

function outer() {
  const x = 10;
  
  function inner() {
    console.log(x); // 10
  }
  
  inner();
}

outer();
```

함수 `outer` 내부에서 중첩 함수 `inner`가 정의되고 호출되었다. 이때 `inner`의 상위 스코프는 `outer`의 스코프이다. 따라서 `inner` 내부에서 자신을 포함하는 `outer`의 변수 `x`에 접근할 수 있다.

만약 함수 `inner`가 함수 `outer`의 내부에서 정의된 중첩 함수가 아니라면, `inner`를 `outer`의 내부에서 호출한다 하더라도 `outer`의 변수에 접근할 수 없다.

```javascript
const x = 1;

function outer() {
  const x = 10;
  inner();
}

function inner() {
  console.log(x); // 1 (전역 변수)
}

outer();
```

이와 같은 현상이 발생하는 이유는 자바스크립트가 **렉시컬 스코프**를 따르는 프로그래밍 언어이기 때문이다.

&nbsp;  

## 1. 렉시컬 스코프

* 자바스크립트 함수는 어디에 정의했는지에 따라 함수의 상위 스코프를 결정한다(렉시컬 스코프를 따른다).
* 스코프의 실체는 실행 컨텍스트의 렉시컬 환경이다.
* 렉시컬 환경은 외부 렉시컬 환경의 참조(Outer Lexical Evnironment Reference)를 통해 상위 렉시컬 환경과 연결된다(스코프 체인).
* 함수 렉시컬 환경의 외부 렉시컬 환경의 참조는 함수 정의가 평가되는 시점에 함수가 정의된 환경(running execution context의 렉시컬 환경)이다.

&nbsp;  

**자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라, 어디에 정의했는지에 따라 함수의 상위 스코프를 결정한다.** 이를 <strong>렉시컬 스코프(정적 스코프)</strong>라 한다.

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

함수 `bar`는 전역에 정의된 함수이다. 따라서 `bar` 함수를 `foo` 함수 내부에서 호출하여도, `bar` 함수 몸체의 `console.log`는 전역 변수 `x`를 가리킨다.

&nbsp;  

실행 컨텍스트에서 살펴보았듯, **스코프의 실체는 실행 컨텍스트의 렉시컬 환경(Lexical Environment)이다.** 렉시컬 환경은 환경 레코드(Environment Record)와 외부 렉시컬 환경에 대한 참조(Outer Lexcial Environment Reference)로 구성되어 있고, **렉시컬 환경은 Outer Lexical Environment Reference를 통해 상위 렉시컬 환경과 연결된다. 이것이 바로 스코프 체인이다.**

따라서 **함수의 상위 스코프를 결정한다는 것은 함수 렉시컬 환경의 Outer Lexical Envrionment Reference 값을 결정한다는 것과 같다.** 이 개념을 반영해서 다시 한번 렉시컬 스코프를 정의해 보면 아래와 같다.

**렉시컬 환경의 Outer Lexical Environment Reference는 함수 정의가 평가되는 시점에 함수가 정의된 환경(위치)에 의해 결정된다. 이것이 바로 렉시컬 스코프이다.**

&nbsp;  

## 2. 함수 객체의 내부 슬롯 [[Environment]]

* 함수는 함수 정의가 평가되어 함수 객체를 생성할때 자신의 내부 슬롯 [[Environment]]에 자신이 정의된 환경(상위 스코프)의 참조를 저장한다.
* 함수가 호출되었을 때 생성하는 함수 렉시컬 환경의 Outer Lexical Envrionment Reference는 함수 자신의 [[Environment]] 내부 슬롯에 저장된 값이다.

&nbsp;  

함수가 정의된 환경과 호출되는 환경(위치)은 다를 수 있다. 따라서 렉시컬 스코프가 가능하려면 함수는 자신이 호출되는 환경과는 상과없이 자신이 정의된 위치(상위 스코프)를 기억해야 한다. 이를 위해 **함수는 함수 정의가 평가되어 함수 객체를 생성할때 자신의 내부 슬롯 [[Environment]]에 자신이 정의된 환경(상위 스코프)의 참조를 저장한다.** 또한 함수 자신이 호출되었을 때 생성될 함수 렉시컬 환경의 Outer Lexical Environment Reference에 저장될 값은 자신의 내부 슬롯 [[Environment]]에 저장된 참조 값이다. 따라서 함수 객체는 자신이 존재하는 한 상위 스코프([[Environment]] 내부 슬롯의 값)를 기억한다.

```javascript
const x = 1;

function foo() {
  const x = 10;
  
  // 상위 스코프는 함수 정의 환경(위치)에 따라 결정된다.
  // 함수 호출 위치와 상위 스코프는 아무런 관계가 없다.
  bar(); // ①
}

// 함수 bar는 자신의 상위 스코프, 즉 전역 렉시컬 환경을 기억한다.
function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

위 예제의 `foo` 함수 내부에서 `bar` 함수가 호출된 시점(①)의 실행 컨텍스트는 아래와 같다.

<img src="https://user-images.githubusercontent.com/32444914/82112692-41984280-978a-11ea-976b-ee624fa66787.png" width="80%" />

함수 `foo`와 함수 `bar`는 모두 전역에서 함수 선언문으로 정의되었다. 따라서 함수 `foo`와 `bar`는 모두 전역 코드가 평가되는 시점에 평가되어 함수 객체를 생성하고 전역 객체 `window`의 프로퍼티가 된다. 이때 생성된 함수 객체의 내부 슬롯 [[Environment]]에는 함수 정의가 평가되는 시점에 running execution context의 렉시컬 환경에 대한 참조가 저장된다.

&nbsp;  

함수가 호출되면 함수 내부로 코드의 제어권이 이동한다. 그리고 함수 코드를 평가하기 시작한다. 함수 코드 평가는 아래 순서로 진행된다.

```pseudocode
1. 함수 실행 컨텍스트 생성
2. 함수 렉시컬 환경 생성
	2.1. 함수 환경 레코드 생성
	2.2. 외부 렉시컬 환경에 대한 참조(Outer Lexical Environment Reference) 할당
	2.3. this 바인딩
```

이때 함수 렉시컬 환경의 구성 요소인 Outer Lexical Environment Reference에는 함수 객체의 내부 슬롯 [[Environment]]에 저장된 렉시컬 환경의 참조가 할당된다.

&nbsp;  

## 3. 클로저와 렉시컬 환경

* 이론적으로 자바스크립트의 모든 함수는 클로저이다. 함수의 내부 슬롯 [[Environment]]에는 상위 스코프(running execution context의 렉시컬 환경 - 자신이 정의된 스코프)에 대한 참조가 있기 때문이다.
* 단, 아래 두 가지 조건을 만족하는 함수를 일반적으로 클로저라고 한다.
  * 자신을 포함하고 있는 외부 함수보다 생명 주기가 더 길다(ex. return된 함수)
  * 외부 함수의 지역 변수에 접근할 수 있다.
* 외부 함수의 호출이 종료되면 외부 함수 실행 컨텍스트가 소멸되는 것이지, 외부 함수의 렉시컬 환경까지 소멸되는 것은 아니다(클로저가 자신의 [[Environment]] 내부 슬롯의 값으로 외부 함수의 렉시컬 환경에 대한 참조를 저장하고 있기 때문이다).
* 클로저에 의해 참조되는 상위 스코프의 변수를 자유 변수라 부른다. 클로저(closure)란 "자유 변수와 묶여있는 함수"라고 할 수 있다.
* 대부분의 모던 브라우저는 최적화를 통해 상위 스코프의 식별자 중 클로저가 참조하고 있는 식별자만을 기억한다. 

&nbsp;  

아래 예제를 살펴보자.

```javascript
const x = 1;

function outer() {
  const x = 10;
  const inner = function () { console.log(x) };
  return inner;
}

// 함수 outer를 호출하면 중첩 함수 inner가 반환된다.
// 그리고 함수 outer의 실행 컨텍스트는 콜 스택에서 pop된다.
const innerFunc = outer();
innerFunc(); // 10
```

위 코드의 실행 결과는 함수 `outer`의 지역 변수 `x`의 값인 10이다.

함수 `outer`를 호출하면 함수 `outer`는 중첩 함수 `inner`를 반환하고 생명 주기(life cycle)를 마감한다. 이때 `outer`의 지역 변수 `x`와 변수값 10을 저장하고 있던 `outer` 실행 컨텍스트가 제거되었으므로 `outer`의 지역 변수 `x`도 생명 주기를 마감한다.  하지만 이미 생명 주기가 종료되어 콜 스택에서 제거된 함수 `outer`의 지역 변수 `x`가 다시 부활이라도 한 듯 동작하고 있다.

이처럼 **자신을 포함하고 있는 외부 함수보다 중첩 함수가 더 오래 유지되는 경우, 외부 함수 밖에서 중첩 함수를 호출하더라도 외부 함수의 지역 변수에 접근할 수 있는 함수를 일반적으로 클로저(closure)라고 부른다.**

&nbsp;  

위 예제에서 `outer` 함수가 평가되어 함수 객체를 생성할 때, running execution context의 렉시컬 환경을 `outer` 함수 객체의 [[Environment]] 내부 슬롯에 상위 스코프로서 저장한다.

<img src="https://user-images.githubusercontent.com/32444914/82113402-b9696b80-9790-11ea-83e8-918a89f72f10.png" width="80%" />

`outer` 함수를 호출하면 `outer` 함수의 렉시컬 환경이 생성되고, `outer` 함수 객체의 [[Environment]] 내부 슬롯에 저장된 전역 렉시컬 환경을 `outer` 함수 렉시컬 환경의 Outer Lexical Environemnt Reference에 할당한다.

그리고 중첩 함수 `inner`가 평가된다(함수 표현식은 런타임에 평가된다). 이때 중첩 함수 `inner`는 자신의 [[Environment]] 내부 슬롯에 running execution context의 렉시컬 환경을 상위 스코프로서 저장한다.

<img src="https://user-images.githubusercontent.com/32444914/82113474-5b895380-9791-11ea-90f7-4257151fd7d2.png" width="80%" />

`outer` 함수의 실행이 종료하면 `inner` 함수를 반환하면서 `outer` 함수 실행 컨텍스트가 콜 스택에서 pop된다. 이때 **outer 함수의 렉시컬 환경까지 소멸하는 것은 아니다.** `outer` 함수의 렉시컬 환경은 `inner` 함수의 [[Environment]] 내부 슬롯에 의해 참조되고 있고, `inner` 함수는 전역 변수 `innerFunc`에 의해 참조되고 있으므로 `outer` 함수의 렉시컬 환경은 메모리에서 해제되지 않는다.

<img src="https://user-images.githubusercontent.com/32444914/82113559-d5b9d800-9791-11ea-8ac9-27ea3b649c4c.png" width="80%" />

`outer` 함수가 반환한 `inner` 함수를 호출하면(`innerFunc()`) `inner` 함수의 실행 컨텍스트가 생성되고 콜 스택에 push된다. 그리고 `innerFunc`의 렉시컬 환경의 Outer Lexical Environment Reference에는 `inner` 함수 객체의 [[Environment]] 내부 슬롯에 저장되어 있는 참조 값이 할당된다.

<img src="https://user-images.githubusercontent.com/32444914/82113613-64c6f000-9792-11ea-8236-b79c8a3819d5.png" width="80%" />

중첩 함수 `inner`는 외부 함수 `outer`보다 더 오래 생존하였다. 이때 함수는 외부 함수의 생존 여부(실행 컨텍스트의 생존 여부)와 상관 없이 자신이 정의된 위치에 의해 결정된 상위 스코프를 기억한다. 따라서 중첩 함수 `inner`의 내부에서는 상위 스코프를 참조할 수 있으므로 상위 스코프의 식별자를 참조할 수 있고 식별자의 값을 변경할 수도 있다.

&nbsp;  

이론적으로 자바스크립트의 모든 함수는 클로저이다. 함수의 내부 슬롯 [[Environment]]에는 상위 스코프(running execution context의 렉시컬 환경 - 자신이 정의된 스코프)에 대한 참조가 있기 때문이다. 단, 일반적으로는 모든 함수를 클로저라 하지 않는다.

&nbsp;  

**클로저가 되기 위한 조건**

1. 중첩 함수가 외부 함수보다 생존 주기가 길다.
2. 1을 만족하며 외부 함수의 지역 변수, 함수(식별자)를 참조한다.

&nbsp;  

대부분의 모던 브라우저는 최적화를 통해 아래와 같이 상위 스코프의 식별자 중 클로저가 참조하고 있는 식별자만을 기억한다. 클로저에 의해 참조되는 상위 스코프의 변수를 <strong>자유 변수(free variable)</strong>라 부른다. 클로저(closure)란 "자유 변수와 묶여있는 함수"라고 할 수 있다.

&nbsp;  

## 4. 클로저의 활용

**클로저는 상태(state)를 안전하게 변경하고 유지하기 위해 사용한다.** 다시 말해, 상태가 의도치 않게 변경되지 않도록 **안전하게 은닉(information hiding)하고 특정 함수에게만 상태 변경을 허용한다.**

&nbsp;  

### 카운터 예제 1

```javascript
// 카운트 상태 변경 함수
const increase = (function () {
  // 카운트 상태를 유지하기 위한 변수(자유 변수)
  let num = 0;
  
  // 클로저
  return function () {
    return ++num;
  };
}());

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

1. 소스 코드가 실행되면 즉시 실행 함수가 호출된다.
2. 즉시 실행 함수가 반환한 함수가 변수 `increase`에 할당된다.
3. `increase`에 할당된 함수는 자신이 정의된 위치(즉시 실행 함수의 렉시컬 환경)를 [[Environment]] 내부 슬롯에 상위 스코프로서 기억한다.
4. 따라서 즉시 실행 함수가 반환한 클로저(`increase`)는 카운트 상태를 유지하기 위한 자유 변수 `num`을 언제든지 참조하고 변경할 수 있다.

&nbsp;  

**이처럼 클로저는 상태가 의도치 않게 변경되지 않도록 안전하게 은닉(information hiding)하고 특정 함수에게만 상태 변경을 허용하여 상태(state)를 안전하게 변경하고 유지하기 위해 사용한다.**

&nbsp;  

현재 `increase` 함수만을 대응하는 위 예제를 `decrease` 함수에도 대응할 수 있도록 좀 더 발전시켜보자.

```javascript
const counter = (function () {
  // 카운트 상태를 유지하기 위한 변수(자유 변수)
  let num = 0;
  
  // 클로저인 메소드를 가지는 객체를 반환한다.
  return {
    // num: 0, // 프로퍼티는 public이므로 정보 은닉이 되지 않는다.
    increase() {
      return ++num;
    },
    decrease() {
      return num > 0 ? --num : 0;
    }
  };
}());

console.log(counter.increase()); // 1
console.log(counter.increase()); // 2
console.log(counter.decrease()); // 1
console.log(counter.decrease()); // 0
```

위 예제에서 즉시 실행 함수가 반환하는 객체 리터럴은 즉시 실행 함수의 실행 단계에서 평가되어 객체가 된다. 이때 **객체의 메소드인 함수도 함수 객체로 생성되므로, 메소드 `increase`와 `decrease`는 자신이 정의된 위치(즉시 실행 함수의 렉시컬 환경)를 [[Environment]] 내부 슬롯에 자신의 상위 스코프로서 기억한다.** 따라서 `increase`와 `decrease` 함수는 즉시 실행 함수 스코프의 식별자를 참조할 수 있다.

&nbsp;  

### 카운터 예제 2(생성자 함수 ver.)

```javascript
const Counter = (function () {
  let num = 0;
  
  function Counter() {
    // this.num = 0; // 인스턴스의 프로퍼티는 pulbic하므로 정보 은닉이 되지 않는다.
  }
  
  Counter.prototype.increase = function () {
    return ++num;
  };
  
  Counter.prototype.decrease = function () {
    return num > 0 ? --num : 0;
  };
  
  return Counter;
}());

const counter = new Counter();

console.log(counter.increase()); // 1
console.log(counter.increase()); // 2

console.log(counter.decrease()); // 1
console.log(counter.decrease()); // 0
```

위 예제의 `num`은 생성자 함수 `Counter`가 생성할 인스턴스의 프로퍼티가 아니라, 즉시 실행 함수 내에서 선언된 변수다. 만약 `num`이 생성자 함수 `Counter`가 생성할 인스턴스의 프로퍼티라면 인스턴스를 통해 외부에서 접근이 가능한 public 프로퍼티가 된다. 하지만 즉시 실행 함수 내에서 선언된 변수 `num`은 인스턴스를 통해 접근할 수 없으며 즉시 실행 함수 외부에서도 접근할 수 없는 은닉된 변수이다.

이러한 클로저의 특징을 사용해 클래스 기반 언어의 `private` 키워드를 흉내낼 수 있다. 상태 변경이나 가변(mutable) 데이터를 피하고 불변성(immutability)을 지향하는 함수형 프로그래밍에서 부수 효과(side effect)를 최대한 언제하여 오류를 피하고, 프로그램의 안정성을 높이기 위해 클로저는 적극적으로 사용된다.

&nbsp;  

## 5. 캡슐화

**캡슐화(encapsulation)는 정보의 일부를 외부에 감추어 은닉(information hiding)하는 것을 말한다.** 즉, 구현의 일부를 외부에 공개되지 않도록 감추어 적절치 못한 접근으로부터 벙보를 보호하며, 객체간의 상호 의존성을 낮추는 효과를 얻는다.

자바스크립트는 자바의 public, private, protected와 같은 접근 제한자를 제공하지 않는다. 따라서 **자바스크립트 객체의 모든 프로퍼티와 메소드는 기본적으로 외부에 공개되어 있다**. 즉 public하다.

클로저를 활용하여 캡슐화를 구현할 수 있을 것 같지만, 그렇지 않다. 아래 예제를 살펴보자.

```javascript
const Person = (function () {
	let _age = 0; // private
  
  // 생성자 함수 (클로저)
  function Person(name, age) {
    this.name = name;
    _age = age;
  }
  
  // 프로토타입 메소드 (클로저)
  Person.prototype.sayHi = function () {
    console.log(`Hi! My name is ${this.name}. I am ${_age}.`);
  };
  
  // 생성자 함수 반환
  return Person;
}());

const me = new Person('Kim', 20);
me.sayHi(); // Hi! My name is Kim. I am 20.
console.log(me.name); // Kim
console.log(me._age); // undefined

const you = new Person('Park', 30);
you.sayHi(); // Hi! My name is Park. I am 30.
console.log(you.name); // Park
console.log(you._age); // undefined
```

위 패턴을 사용하면 접근 제한자를 제공하지 않는 자바스크립트에서도 캡슐화가 가능한 것처럼 보인다. `Person` 생성자 함수와 `Person.prototype.sayHi` 메소드는 즉시 실행 함수의 지역 변수 `_age`을 참조할 수 있는 클로저이다.

하지만 위 코드의 문제는 `Person` 생성자 함수가 여러 개의 인스턴스를 생성할 경우, `_age` 변수의 상태를 유지하지 못한다는 것이다.

```javascript
const me = new Person('Kim', 20);
me.sayHi(); // Hi! My name is Kim. I am 20.

const you = new Person('Park', 30);
you.sayHi(); // Hi! My name is Park. I am 30.

// _age의 상태가 변경된다.
me.sayHi(); // Hi! My name is Kim. I am 20.
```

이는 `Person.prototype.sayHi` 메소드가 단 한번만 생성되는 클로저이기 때문에 발생하는 현상이다. `Person` 생성자 함수의 모든 인스턴스가 상속을 통해 호출할 수 있는 `Person.prototype.sayHi` 메소드의 상위 스코프는 어떤 인스턴스로 호출하더라도 하나의 동일한 상위 스코프를 사용하게 된다.

&nbsp;  

이처럼 자바스크립트는 캡슐화를 완전하게 지원하지 않는다. 인스턴스 메소드를 사용한다면 자유 변수를 통해 private을 흉내낼 수는 있지만, 프로토타입 메소드를 사용하면 이마저도 불가능하다.

다행히도 2020년 5월 TC39 프로세스의 stage 3(candidate)에는 클래스에 private 필드를 정의할 수 있는 새로운 표준 사양이 제안되어 있다. 표준 사양으로 승급이 확실시 되는 이 제안은 현재 최신 브라우저와 Node.js에 이미 구현되어 있다.

&nbsp;  

&nbsp;  

## 6. 자주 발생하는 실수

아래는 클로저를 사용할 때 자주 발생할 수 있는 실수에 관련한 예제이다.

```javascript
var funcs = [];

for (var i = 0; i < 3; i++) {
  funcs[i] = function () {
    return i;
  };
}

for (var j = 0; j < funcs.length; j++) {
  console.log(funcs[j]()); // 3 3 3
}
```

for 문의 초기화 문에서 `var` 키워드로 선언한 변수 `i`는 블록 레벨 스코프가 아닌 함수 레벨 스코프를 갖기 때문에 전역 변수가 되며, 변수 `i`에는 0, 1, 2가 순차적으로 할당된다. 따라서 배열 `funcs`에 요소로 추가된 함수를 호출하면 전역 변수 `i`를 참조하여 `i`의 값 3이 출력된다.

&nbsp;  

클로저를 사용해 위 예제를 바르게 동작하는 코드로 만들어보자.

```javascript
var funcs = [];

for (var i = 0; i < 3; i++) {
  funcs[i] = (function iife(id) { // ①
    return function inner() {
      return i;
    };
  }(i));
}

for (var j = 0; j < funcs.length; j++) {
  console.log(funcs[j]());
}
```

①에서 즉시 실행 함수(`iife`)는 전역 변수 `i`의 현재 값을 인수로 전달 받아 새로운 매개 변수 `id`에 할당한 후 중첩 함수(`inner`)를 반환하고 종료된다. 이때 `iife`의 매개 변수 `id`는 `inner`의 상위 스코프에 존재하며 `inner`에 의해 참조되므로 자유 변수가 되어 `inner`에 의해 그 값이 유지된다.

&nbsp;  

이러한 방법은 자바스크립트의 함수 레벨 스코프 특성으로 인해 for 문의 초기화 문에서 `var` 키워드로 선언한 변수가 전역 변수가 되기 때문에 사용한다. ES6의 `let` 키워드를 사용하면 이와 같은 번거로움이 깔끔하게 해결된다.

```javascript
const funcs = [];

for (let i = 0; i < 3; i++) {
  funcs[i] = function () {
    return i;
  };
}

for (let i = 0; i < 3; i++) {
  console.log(funcs[i]()); // 0 1 2
}
```

&nbsp;  

이전 실행 컨텍스트에서 살펴보았듯, **초기화 문에서 `let` 키워드로 선언한 변수를 사용하면 for 문이 반복될 때마다 for 문 코드 블록의 새로운 렉시컬 환경이 생성된다.** 만약 for 문 안에 정의된 함수가 있다면, 이 함수의 상위 스코프는 for 문이 반복될 때마다 독립적으로 생성된 for 문 코드 블록의 새로운 렉시컬 환경이다.

<img src="https://user-images.githubusercontent.com/32444914/82119209-a322d600-97b7-11ea-8b15-38cd94c30dc3.png" width="80%" />

이처럼 `var` 키워드로 사용하지 않은 ES6의 반복문(for...in 문, for...of 문, while 문 등)은 반복할 때마다 새로운 렉시컬 환경을 생성하여 반복할 당시의 상태를 마치 스냅샷처럼 저장한다. 이는 반복문 내부에서 함수 정의가 존재할 때 의미가 있다.

&nbsp;  

## 출처

* [poiemaweb.com - 클로저](https://poiemaweb.com/fastcampus/closure)

