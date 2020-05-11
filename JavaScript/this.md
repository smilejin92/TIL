# this

## 1. this 키워드

객체지향 프로그래밍에서 살펴보았듯 **객체는 상태(state)를 나타내는 프로퍼티와 동작(behavior)을 나타내는 메소드를 하나의 논리적인 단위로 묶은 복학접인 자료구조**이다.

메소드는 자신이 속한 객체의 프로퍼티(상태)를 참조하고 변경할 수 있어야 한다. 이때 메소드가 자신이 속한 객체의 프로퍼티를 참조하려면 먼저 **자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.**

객체 리터럴 방식으로 생성한 객체의 경우, 메소드 내부에서 메소드 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조할 수 있다.

```javascript
const circle = {
  radius: 5,
  getDiameter() {
    // 자신이 속한 객체 circle을 참조할 수 있어야 한다.
    return 2 * circle.radius;
  }
};

console.log(circle.getDiameter()); // 10
```

`getDiameter` 메소드가 호출되는 시점에는 이미 객체 리터럴의 평가가 완료되어 생성된 객체가 `circle` 식별자에 바인딩되어 있다. 따라서 메소드 내부에서 식별자 `circle`을 참조할 수 있다.

> **바인딩(Binding)**
>
> 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 예를 들어 변수는 할당에 의해 값이 바인딩된다.



하지만 생성자 함수로 인스턴스를 생성하려면 먼저 생성자 함수가 존재해야 한다. 따라서 **생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하기 이전이므로 생성자 함수가 생성할 인스턴스를 가리키는 식별자를 알 수 없다.**

```javascript
function Circle(radius) {
  // 이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
  ???.radius = radius;
}

Circle.prototype.getDiameter = function () {
  // 이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
  return 2 * ???.radius;
}

// 생성자 함수로 인스턴스를 생성하려면 먼저 생성자 함수를 정의해야 한다.
const circle = new Circle(5);
```

이러한 문제를 해결할 수 있게 자바스크립트는 `this`라는 특수한 식별자를 제공한다. **this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(Self-referencing variable)이다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메소드를 참조할 수 있다.**

`this`는 자바스크립트 엔진에 의해 암묵적으로 생성되며 코드 어디에서든지 참조할 수 있다. 함수 내부에서 `arguments` 객체를 지역 변수처럼 사용할 수 있는 것처럼, `this`도 지역 변수처럼 사용할 수 있다. **단, this가 가리키는 값(this binding)은 함수 호출 방식에 의해 동적으로 결정된다.**

&nbsp;  

## 2. 함수 호출 방식과 this 바인딩

**this 바인딩(this에 연결되는 값)은 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.**

> **렉시컬 스코프와 this 바인딩은 결정 시기가 다르다.**
>
> 함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프(Lexical scope)는 함수 정의가 평가되어 함수 객체가 생성되는 시점에 상위 스코프를 결정한다. 반면, this에 바인딩될 객체는 함수 호출 시점에 결정된다.

함수를 호출하는 방식은 아래와 같이 다양하다.

1. 일반 함수 호출
2. 메소드 호출
3. 생성자 함수 호출
4. Function.prototype.apply / call / bind 메소드에 의한 간접 호출

주의할 것은 **동일한 함수도 다양한 방식으로 호출할 수 있다는 것이다.**

```javascript
// this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.
const foo = function () {
  console.dir(this);
};

// 1. 일반 함수 호출
foo(); // window

// 2. 메소드 호출
const obj = { foo };
obj.foo(); // obj

// 3. 생성자 함수 호출
new foo(); // foo {}

// 4. Function.prototype.apply / call / bind 메소드에 의한 간접 호출
const bar = { name: 'bar' };
foo.call(bar); // bar
foo.apply(bar); // bar
foo.bind(bar); // bar
```

다양한 함수의 호출 방식에 따라 this 바인딩이 어떻게 결정되는지 알아보자.

&nbsp;  

### 2.1. 일반 함수 호출

**기본적으로 this에는 전역 객체(global object)가 바인딩된다.**

```javascript
function foo() {
  console.log(`foo's this: ${this}`); // window
  
  function bar() {
    console.log(`bar's this: ${this}`); // window
  }
  bar();
}
foo();
```

위 예제처럼 전역 함수는 물론, 중첩 함수를 **일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩된다.** 다만, this는 객체의 프로퍼티나 메소드를 참조하기 위한 자기 참조 변수이므로 **객체를 생성하지 않는 일반 함수에서 this는 의미가 없다.** 따라서 엄격 모드(strict mode)가 적용된 일반 함수 내부의 this에는 undefined가 바인딩된다.

```javascript
function foo() {
  console.log(`foo's this: ${this}`); // undefined
  
  function bar() {
    console.log(`bar's this: ${this}`); // undefined
  }
  bar();
}
foo();
```

&nbsp;  

메소드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는 전역 객체가 바인딩된다.

```javascript
const obj = {
  value: 100,
  foo() {
    console.log(`foo's this: ${this}`); // { value: 100, foo: function }
    
    // 메소드 내에서 정의한 중첩 함수
    function bar() {
      console.log(`bar's this: ${this}`); // window
    }
    // 메소드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는 전역 객체가 바인딩된다.
    bar();
  }
};

obj.foo();
```

&nbsp;  

콜백 함수가 일반 함수로 호출된다면 콜백 함수 내부의 this에도 전역 객체가 바인딩된다.

```javascript
const obj = {
  value: 100,
  foo() {
    console.log(`foo's this: ${this}`); // { value: 100, foo: function }
    
    // 콜백 함수 내부의 this에는 전역 객체가 바인딩된다.
    setTimeout(function () {
      console.log(`callback's this: ${this}`); // window
    }, 100);
  }
};

obj.foo();
```

**이처럼 일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 포함) 내부의 this에는 전역 객체가 바인딩된다.**

하지만 메소드 내에서 정의한 중첩 함수 또는 메소드에게 전달한 콜백 함수(보조 함수) 내부의 this가 전역 객체를 바인딩하는 것은 문제가 있다. **외부 함수인 메소드와 중첩 함수 혹은 콜백 함수의 this가 일치하지 않으면, 중첩 함수 혹은 콜백 함수를 헬퍼 함수로 사용하기 어렵기 때문이다.**

&nbsp;  

### 2.2. 메소드 호출

### 2.3. 생성자 함수 호출

### 2.4. Function.prototype.apply / call / bind 메소드에 의한 간접 호출

