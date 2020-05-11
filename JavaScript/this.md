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

| 함수 호출 방식                                               | this 바인딩                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 일반 함수 호출                                               | 전역 객체                                                    |
| 메소드 호출                                                  | 메소드를 호출한 객체                                         |
| 생성자 함수 호출                                             | 생성자 함수가 (미래에) 생성할 인스턴스                       |
| Function.prototype.apply / call / bind 메소드에 의한 간접 호출 | Function.prototype.apply / call / bind 메소드에 첫번째 인수로 전달한 객체 |



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

메소드 내부의 this에는 메소드를 호출한 객체(메소드 이름 앞의 마침표 연산자 앞에 위치한 객체)가 바인딩된다. 주의할 것은 **메소드 내부의 this는 메소드를 소유한 객체가 아닌, 메소드를 호출한 객체에 바인딩된다는 것**이다.

```javascript
const person = {
  name: 'Kim',
  getName() {
    // 메소드의 this는 메소드를 호출한 객체에 바인딩된다.
    return this.name;
  }
};

// 메소드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Kim
```

위 예제의 `getName` 메소드는 프로퍼티에 바인딩된 함수이다. 즉, `person` 객체와 `getName` 프로퍼티가 가리키는 함수 객체는 별도의 객체이다.

<img src="https://user-images.githubusercontent.com/32444914/81574129-5cf8fb80-93e0-11ea-9560-739e8bb1ac20.png" width="80%" />

따라서 `getName` 프로퍼티가 가리키는 함수 객체는 다른 객체의 프로퍼티에 할당는 것으로 다른 객체의 메소드가 될 수도 있고, 일반 변수에 할당하여 일반 함수로 호출될 수도 있다.

```javascript
const anotherPerson = {
  name: 'Kim'
};

// 메소드 getName을 anotherPerson 객체의 메소드로 할당
anotherPerson.getName = person.getName;

// 메소드 getName을 호출한 객체는 anotherPerson이다.
console.log(anotherPerson.getName()); // Kim

// 메소드 getName을 변수에 할당
const getName = person.getName;

// 메소드 getName을 일반 함수로 호출
console.log(getName()); // '' (window.name)
```

따라서 **메소드 내부의 `this`는 프로퍼티로 메소드를 가리키고 있는 객체와는 관계가 없고, 메소드를 호출한 객체에 바인딩된다.**

<img src="https://user-images.githubusercontent.com/32444914/81574794-38e9ea00-93e1-11ea-8857-0c246af7abf4.png" width="80%" />

&nbsp;  

### 2.3. 생성자 함수 호출

생성자 함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.

```javascript
// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
// 반지름이 5인 Circle 객체를 생성
const circle1 = new Circle(5);
// 반지름이 10인 Circle 객체를 생성
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

생성자 함수는 이름 그대로 객체(인스턴스)를 생성하는 함수이다. 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 **new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다**. 만약 new 연산자와 함께 생성자 함수를 호출하지 않으면 생성자 함수가 아니라 일반 함수로 동작한다.

```javascript
// new 연산자와 함께 호출하지 않으면 일반 함수로 호출된다.
const circle3 = Circle(15);

// 일반 함수 Circle은 반환문이 없으므로 암묵적으로 undefined를 반환한다.
console.log(circle3); // undefined

// 일반 함수 Circle내의 this는 전역 객체를 가리킨다.
console.log(radius); // 15 (window.radius)
```

&nbsp;  

### 2.4. Function.prototype.apply / call / bind 메소드에 의한 간접 호출

`Function.prototype.apply`, `Function.prototype.call` 메소드는 인수로 this와 인수 리스트를 전달받아 함수를 호출한다. appy와 call 메소드는 `Funtion.prototype`의 메소드이므로, Function 생성자 함수를 constructor 프로퍼티로 가리키는 모든 함수가 상속받아 사용할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/81584369-a00d9b80-93ed-11ea-8712-88a8125e234e.png" width="80%" />

&nbsp;  

#### 2.4.1. apply, call

```javascript
/* 
apply
* 함수 내부에서 사용할 this와 인수 리스트 배열을 사용하여 함수를 호출한다.
* @param thisArg - this로 사용될 객체
* @param argsArray - 함수에게 전달할 인수 리스트의 배열 또는 유사 배열 객체
* @returns 호출된 함수의 반환값
*/
Function.prototype.apply(thisArg[, argsArray]);

/*
call
* 함수 내부에서 사용할 this와 ,로 구분된 인수 리스트를 사용하여 함수를 호출한다.
* @param thisArg - this로 사용될 객체
* @param arg1, arg2, ... - 함수에게 전달할 인수 리스트
* @returns 호출된 함수의 반환값
*/
Function.prototype.call(thisArg[, arg1[, arg2[, ...]]])
```

아래 예제를 살펴보자.

```javascript
function getThisBinding() {
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };
console.log(getThisBinding()); // window

// getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩한다.
console.log(getThisBinding.apply(thisArg)); // { a: 1 }
console.log(getThisBinding.call(thisArg)); // { a: 1 }
```

**apply와 call 메소드의 본질적인 기능은 함수를 호출하는 것이다.** apply와 call 메소드는 함수를 호출하면서 첫번째 인수로 전달한 특정 객체를 호출함 함수의 this에 바인딩한다.

apply와 call 메소드는 호출할 함수에 인수를 전달하는 방식만 다를 뿐, this로 사용할 객체를 전달하면서 함수를 호출하는 것은 동일하다.

```javascript
function getThisBinding() {
  console.log(arguments);
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩한다.
// apply 메소드는 호출할 함수의 인수를 배열로 묶어 전달한다.
console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
// Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
// { a: 1 }

// call 메소드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다.
console.log(getThisBinding.call(thisArg, 1, 2, 3));
// Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
// { a: 1 }
```

&nbsp;  

#### 2.4.2. bind

`Function.prototype.bind` 메소드는 apply와 call 메소드와는 달리 **함수를 호출하지 않고 this로 사용할 객체만을 전달한다.**

```javascript
function getThisBinding() {
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// bind 메소드는 함수에 this로 사용할 객체를 전달한다.
// bind 메소드는 함수를 호출하지는 않는다.
console.log(getThisBinding.bind(thisArg)); // this 바인딩

// bind 메소드는 함수를 호출하지는 않으므로 명시적으로 호출해야 한다.
console.log(getThisBinding.bind(thisArg)()); // { a: 1 }
```

bind 메소드는, 객체의 메소드 내부에 정의된 중첩 함수 혹은 객체의 메소드에 전달된 콜백 함수가 일반 함수로 호출되어 this가 일치하지 않는 경우에 유용하게 사용된다.

```javascript
const person = {
  name: 'Kim',
  foo(callback) {
    // bind 메소드로 callback 함수 내부의 this 바인딩을 전달
    setTimeout(callback.bind(this), 100); // 여기서 this는 person을 가리킨다.
  }
};

person.foo(function () {
  console.log(`Hi! My name is ${this.name}`); // Hi! My name is Kim.
});
```

