# 클래스

## 1. 클래스는 프로토타입의 문법적 설탕인가?

* 클래스는 새로운 객체 생성 메커니즘이다.
* 클래스는 생성자 함수보다 엄격하며, 생성자 함수에서 제공하지 않는 기능을 제공한다.
  * `super`, `extends` 키워드 제공
  * 호이스팅이 발생하지 않는 것 처럼 동작 (선언문 이전에 참조할 수 없다)
  * `new` 연산자와 함께 호출하지 않으면 에러 발생
  * 클래스 내의 모든 코드에는 암묵적으로 엄격 모드가 적용되며, 해지할 수 없다.
  * 클래스의 constructor, 프로토타입 메소드, 정적 메소드는 열거되지 않는다.

&nbsp;  

자바스크립트는 프로토타입 기반(prototype-based) 객체지향 언어다. 프로토타입 기반 객체지향 언어는 클래스가 필요 없은(class-free) 객체지향 프로그래밍 언어이다. ES5에서는 클래스 없이도 아래와 같이 생성자 함수와 프로토타입 체인, 클로저를 사용하여 객체 지향 언어의 상속의 개념을 구현할 수 있고,  캡슐화도 한정적으로 구현할 수 있었다.

```javascript
// ES5 생성자 함수
var Person = (function () {
  var _name = '';
  
  // 생성자 함수(클로저)
  function Person(name) {
    _name = name;
  }
  
  // 프로토타입 메소드(클로저)
  Person.prototype.sayHi = function () {
    console.log('Hi! My name is ' + _name);
  };
  
  // 생성자 함수 반환
  return Person;
}());

// 인스턴스 생성
var me = new Person('Kim');

// _name은 지역 변수이므로 외부에서 접근하여 변경할 수 없다(private하다).
// me 객체에는 _name 프로퍼티가 존재하지 않기 때문에 me._name 프로퍼티를 동적 추가할 뿐이다.
me._name = 'Kim';
me.sayHi(); // Hi! My name is Kim
```

ES6에서 새롭게 도입된 클래스는 Java나 C#과 같은 클래스 기반 객체지향 프로그래밍에 익숙한 프로그래머가 보다 빠르게 학습할 수 있도록 클래스 기반 객체지향 프로그래밍 언어와 매우 흡사한 **새로운 객체 생성 메커니즘**을 제시하고 있다.

단, 클래스와 생성자 함수는 모두 프로토타입 기반의 인스턴스를 생성하지만 정확히 동일하게 동작하지는 않는다. **클래스는 생성자 함수보다 엄격하며 생성자 함수에서는 제공하지 않는 기능도 제공한다.**

1. 클래스는 `new` 연산자를 사용하지 않고 호출하면 에러가 발생한다.
2. 클래스는 상속을 지원하는 `extends`와 `super` 키워드를 제공한다.
3. 클래스는 호이스팅이 발생하지 않는 것 처럼 동작한다(TDZ).
4. 클래스 내의 모든 코드에는 암묵적으로 strict 모드가 적용되며, 해지할 수 없다.
5. 클래스의 constructor, 프로토타입 메소드, 정적 메소드는 열거되지 않는다([[Enumerable]]의 값이 false이다).

&nbsp;  

## 2. 클래스 정의

* 클래스는 `class` 키워드를 사용하여 정의한다.
* 클래스는 **함수**이다. 따라서 클래스는 **일급 객체**이다.
* 클래스 몸체에는 0개 이상의 메소드만을 정의할 수 있다.
  * constructor
  * 프로토타입 메소드
  * 정적 메소드

&nbsp;  

클래스는 `class` 키워드를 사용하여 정의한다. 클래스 이름은 생성자 함수와 마찬가지로 파스칼 케이스를 사용하는 것이 일반적이다.

```javascript
// 클래서 선언문
class Person {}
```

&nbsp;  

일반적이지는 않지만, 함수와 마찬가지로 표현식으로 클래스를 정의할 수 있다. 이때 클래스는 함수와 마찬가지로 이름일 가질 수 있고, 그렇지 않을 수도 있다.

```javascript
// 익명 클래스 표현식
const Person = class {};

// 기명 클래스 표현식
const Person = class MyClass {};
```

클래스를 표현식으로 정의할 수 있다는 것은 클래스가 **값**으로 사용할 수 있는 **일급 객체**라는 것을 의미한다. 즉, 클래스는 일급 객체로서 아래와 같은 특징을 가진다.

* 무명의 리터럴로 생성할 수 있다(런타임에 생성이 가능하다).
* 변수나 자료 구조에 저장할 수 있다.
* 함수의 매개 변수에게 전달할 수 있다.
* 함수의 반환값으로 사용할 수 있다.

**좀 더 자세히 말하자면 클래스는 함수이다. 따라서 클래스는 값처럼 사용할 수 있는 일급 객체이다.**

&nbsp;  

클래스 몸체에는 0개 이상의 **메소드만을 정의할 수 있다.** 클래스 몸체에서 정의할 수 있는 메소드는 아래와 같다.

1. constructor (생성자 함수)
2. 프로토타입 메소드
3. 정적 메소드

```javascript
// 클래스 선언문
class Person {
  // 1. 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name; // name 프로퍼티는 public하다.
  }
  
  // 2. 프로토타입 메소드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
  
  // 3. 정적 메소드
  static sayHello() {
    console.log('Hello!');
  }
}

// 인스턴스 생성
const me = new Person('Kim');

// 인스턴스의 프로퍼티 참조
console.log(me.name); // Kim

// 프로토타입 메소드 호출
me.sayHi(); // Hi! My name is Kim

// 정적 메소드 호출
Person.sayHello(); // Hello!
```

클래스와 생성자 함수의 정의 방식을 비교해 보면 아래와 같다.

<img src="https://user-images.githubusercontent.com/32444914/82151338-0a16bc80-9896-11ea-8f79-acac41eb3769.png" width="80%" />

이처럼 클래스와 생성자 함수의 정의 방식은 형태적인 면에서 매우 유사하다.

&nbsp;  

## 3. 클래스 호이스팅

클래스는 클래스 정의 이전에 참조할 수 없다(TDZ).

```javascript
console.log(Person);
// ReferenceError: Cannot access 'Person' before initialization

// 클래스 선언문
class Person {}
```

&nbsp;  

클래스 선언문은 마치 호이스팅이 발생하지 않는 것처럼 보이지만 그렇지 않다.

```javascript
const Person = '';

{
  // 호이스팅이 발생하지 않는다면 ''이 출력되어야 한다.
  console.log(Person);
  // ReferenceError: Cannot access 'Person' before initialization
  
  // 클래스 선언문
  class Person {}
}
```

**모든 선언문은 런타임 이전에 먼저 실행된다.** 따라서 클래스 선언문도 변수 선언, 함수 선언문으로 정의한 함수와 마찬가지로 호이스팅이 발생한다. 단, 클래스는 `let`, `const` 키워드로 선언한 변수처럼 호이스팅된다. 즉, 클래스 선언문 이전에 일시적 사각지대(TDZ)에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다.

&nbsp;  

## 4. 인스턴스 생성

**클래스는 함수로 평가된다.**

```javascript
class Person {}

console.log(typeof Person); // function
```

즉, **클래스는 생성자 함수이며 `new` 연산자와 함께 호출되어 인스턴스를 생성한다.**

```javascript
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); // Person {}
```

함수는 `new` 연산자의 사용 여부에 따라 일반 함수로 호출되거나 생성자 함수로 호출되지만, **클래스는 인스턴스를 생성하는 것이 유일한 존재 이유이므로 반드시 `new` 연산자와 함께 호출하여야 한다.**

&nbsp;  

클래스 표현식으로 정의된 클래스의 경우, 클래스를 가리키는 식별자를 사용해 인스턴스를 생성해야한다.

```javascript
const Person = class MyClass {};

const me = new Person();
const you = new MyClass(); // ReferenceError: MyClass is not defined
```

이는 기명 함수 표현식과 마찬가지로 클래스 표현식에서 사용한 클래스 이름은 클래스 몸체 외부에서 접근 불가능하기 때문이다.

&nbsp;  

## 5. 메소드

클래스 몸체에는 0개 이상의 메소드 만을 선언할 수 있다. 클래스 몸체에서 정의할 수 있는 메소드는 아래 3가지 뿐이다.

1. constructor(생성자)
2. 프로토타입 메소드
3. 정적 메소드

&nbsp;  

### 5.1. constructor

* constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메소드이다.
* constructor는 이름을 변경할 수 없다.
* constructor 내부의 this는 클래스가 생성한 인스턴스를 가리킨다.
* constructor는 메소드로 해석되는 것이 아니라, 클래스가 평가되어 생성한 함수 객체 코드의 일부분이 된다. 다시 말해, **클래스 정의가 평가되면 constructor의 기술된 동작을 하는 함수 객체가 생성된다.**
* constructor 메소드는 클래스 내 최대 한개만 존재할 수 있다.
* constructor 메소드는 생략할 수 있다(암묵적으로 디폴트 constructor 메소드가 정의된다).
* constructor 메소드를 생략한 클래스는 디폴트 constructor 메소드에 의해 빈 객체를 생성한다.
* 인스턴스를 생성할 때, 클래스 외부에서 인스턴스 프로퍼티의 초기값을 전달하려면 constructor 메소드에 매개변수를 선언하고 인스턴스를 생성할 때 초기값을 전달한다. 이때 초기값은 constructor 메소드의 매개변수에 전달된다.
* constructor 메소드는 별도의 반환문을 갖지 않는다. 암묵적으로 this, 즉 인스턴스를 반환하기 때문이다.

&nbsp;  

constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메소드이다. constructor는 이름을 변경할 수 없다.

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }
}
```

&nbsp;  

앞에서 살펴본 바와 같이 클래스는 인스턴스를 생성하기 위한 생성자 함수이다. 아래를 크롬 브라우저의 개발자 도구에서 실행해보자.

```javascript
// 클래스는 함수이다.
console.log(typeof Person); // function
console.dir(Person);
```

<img src="https://user-images.githubusercontent.com/32444914/82153345-d5a8fd80-98a1-11ea-9875-539bc8f3b6fd.png" width="80%" />

이처럼 클래스는 평가되어 함수 객체가 된다. 클래스도 함수 객체 고유의 프로퍼티를 모두 갖고 있다. 함수와 동일하게 프로토타입과 연결되어 있으며 자신의 스코프 체인을 구성한다.

모든 함수 객체가 가지고 있는 `prototype` 프로퍼티가 가리키는 객체(프로토타입 객체)의 `constructor` 프로퍼티는 클래스 자신을 가리키고 있다. 이는 클래스가 인스턴스를 생성하는 생성자 함수라는 것을 의미한다.

```javascript
// 인스턴스 생성
const me = new Person('Kim');
console.log(me);
```

위 예제를 실행하면 `Person` 클래스의 constructor 메소드 내부에서 `this`에 추가한 `name` 프로퍼티가 `me` 인스턴스의 프로퍼티로 추가된 것을 확인할 수 있다. 즉, 생성자 함수와 마찬가지로 constructor 메소드 내부에서 `this`에 추가한 프로퍼티는 인스턴스 프로퍼티가 된다. constructor 메소드 내부의 `this`는 생성자 함수와 마찬가지로 클래스가 생성한 인스턴스를 가리킨다.

```javascript
// 클래스
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }
}

// 생성자 함수
function Person(name) {
  // 인스턴스 생성 및 초기화
  this.name = name;
}
```

그런데 흥미로운 것은 클래스가 평가되어 생성된 함수 객체나 클래스가 생성한 인스턴스 어디에도 constructor 메소드가 보이지 않는다는 것이다. constructor는 메소드로 해석되는 것이 아니라, 클래스가 평가되어 생성한 함수 객체 코드의 일부가 된다. 다시 말해, **클래스 정의가 평가되면 constructor의 기술된 동작을 하는 함수 객체가 생성된다.**

&nbsp;  

#### 클래스 constructor 메소드 vs. 생성자 함수

* constructor 메소드는 클래스 내 최대 한개만 존재할 수 있다.
* constructor 메소드는 생략할 수 있다(암묵적으로 디폴트 constructor 메소드가 정의된다).
* constructor 메소드를 생략한 클래스는 디폴트 constructor 메소드에 의해 빈 객체를 생성한다.
* 인스턴스를 생성할 때, 클래스 외부에서 인스턴스 프로퍼티의 초기값을 전달하려면 constructor 메소드에 매개변수를 선언하고 인스턴스를 생성할 때 초기값을 전달한다. 이때 초기값은 constructor 메소드의 매개변수에 전달된다.
* constructor 메소드는 별도의 반환문을 갖지 않는다. 암묵적으로 this, 즉 인스턴스를 반환하기 때문이다.

&nbsp;  

### 5.2. 프로토타입 메소드

* 클래스 몸체에서 정의한 메소드는 프로토타입 메소드가 된다.
* 클래스가 생성한 인스턴스는 프로토타입 체인의 일원이 된다.

&nbsp;  

클래스 몸체에서 정의한 메소드는 `클래스.prototype` 프로퍼티에 메소드를 추가하지 않아도 기본적으로 프로토타입 메소드가 된다.

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }
  
  // 프로토타입 메소드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
}

const me = new Person('Kim');
me.sayHi(); // Hi! My name is Kim
```

&nbsp;  

생성자 함수와 마찬가지로 클래스가 생성한 인스턴스는 프로토타입 체인의 일원이 된다.

```javascript
// me 객체의 프로토타입은 Person.prototype이다.
me.__proto__ === Person.prototype; // true
me instanceof Person; // true

// Person.prototype의 프로토타입은 Object.prototype이다.
Person.prototype.__proto__ === Object.prototype; // true
me instanceof Object; // true

// me 객체의 constructor는 Person 클래스이다.
me.constructor === Person; // true
```

위 예제의 Person 클래스는 아래와 같이 프로토타입 체인을 생성한다.

<img src="https://user-images.githubusercontent.com/32444914/82154120-c9736f00-98a6-11ea-8c90-6781fd93fe0c.png" width="80%" />

이처럼 클래스 몸체에서 정의한 메소드는 인스턴스의 프로토타입에 존재하는 프로토타입 메소드가 된다. 인스턴스는 프로토타입 메소드를 상속받아 사용할 수 있다.

프로토타입 체인은 기존의 모든 객체 생성 방식(객체 리터럴, 생성자 함수, Object.create 메소드 등) 뿐만 아니라 클래스에 의해 생성된 인스턴스에도 동일하게 적용된다. 생성자 함수의 역할을 클래스가 할 뿐이다. 따라서 클래스는 생성자 함수와 마찬가지로 프로토타입 기반의 객체 생성 매커니즘이다.

&nbsp;  

### 5.3. 정적 메소드

클래스에서는 메소드에 `static` 키워드를 붙이면 정적 메소드(클래스 메소드)가 된다.

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }
  
  // 정적 메소드
  static sayHi() {
    console.log('Hi!');
  }
}
```

위 예제의 `Person` 클래스는 아래와 같이 프로토타입 체인을 생성한다.

<img src="https://user-images.githubusercontent.com/32444914/82154435-e14bf280-98a8-11ea-95ba-fa2863c654bc.png" width="80%" />

이처럼 정적 메소드는 클래스 자신의 메소드가 된다. 클래스는 함수 객체로 평가되므로 자신의 프로퍼티 / 메소드를 소유할 수 있다.

&nbsp;  

### 5.4. 정적 메소드와 프로토타입 메소드의 차이

* 메소드 내부에서 인스턴스 프로퍼티를 참조해야 할 필요가 있다면 this를 사용해야 한다. 이러한 경우, 프로토타입 메소드로 정의해야 한다.
* 메소드 내부에서 인스턴스 프로퍼티를 참조해야 할 필요가 없다면 정적 메소드로 정의하는 것이 좋다.
* 클래스 또는 생성자 함수를 하나의 **네임 스페이스**로 사용하여 정적 메소드를 모아 놓으면 이름 충돌 가능성을 줄여 주고, 관련 있는 함수들을 구조화 할 수 있는 효과가 있다.
* 정적 메소드와 프로토타입 메소드의 차이는 아래와 같다.
  * 정적 메소드와 프로토타입 메소드는 자신이 속해 있는 **프로토타입 체인이 다르다.**
  * 정적 메소드는 클래스로 호출하고, 프로토타입 메소드는 인스턴스로 호출한다.
  * 정적 메소드는 인스턴스 프로퍼티를 참조할 수 없지만, 프로토타입 메소드는 인스턴스 프로퍼티를 참조할 수 있다.

&nbsp;  

아래 예제를 살펴보자.

```javascript
class Square {
  // 정적 메소드
  static area(width, height) {
    return width * height;
  }
}

console.log(Square.area(10, 10)); // 100
```

이때 정적 메소드 `area`는 인스턴스 프로퍼티를 참조하지 않는다. **만약 인스턴스 프로퍼티를 참조해야 한다면 정적 메소드 대신 프로토타입 메소드를 사용해야 한다.**

```javascript
class Square {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  
  // 프로토타입 메소드
  area() {
    return this.width * this.height;
  }
}

const square = new Square(10, 10);
console.log(square.area()); // 100
```

메소드 내부의 this는 메소드를 소유한 객체가 아니라 메소드를 호출한 객체, 즉 메소드 이름 앞의 마침표(`.`) 연산자 앞에 기술한 객체에 바인딩된다.

프로토타입 메소드는 인스턴스로 호출해야 하므로 프로토타입 메소드 내부의 this는 프로토타입 메소드를 호출한 인스턴스를 가리킨다.

정적 메소드는 클래스로 호출해야 하므로 정적 메소드 내부의 this는 인스턴스가 아닌 클래스를 가리킨다. 즉, 프로토타입 메소드와 정적 메소드 내부의 this 바인딩이 다르다.

**따라서 메소드 내부에서 인스턴스 프로퍼티를 참조해야 할 필요가 있다면 this를 사용해야 한다. 이러한 경우, 프로토타입 메소드로 정의해야 한다. 하지만 메소드 내부에서 인스턴스 프로퍼티를 참조해야 할 필요가 없다면 정적 메소드로 정의하는 것이 좋다.**

&nbsp;  

표준 빌트인 객체인 `Math`, `Number`, `JSON`, `Object`, `Reflect` 등은 다양한 정적 메소드를 가지고 있다.

```javascript
Math.max(1, 2, 3);
Number.isNaN(NaN);
JSON.stringify({ a: 1 });
Object.create(null);
Reflect.has({ a: 1 }, 'a');
```

이처럼 클래스 또는 생성자 함수를 하나의 **네임 스페이스**로 사용하여 정적 메소드를 모아 놓으면 이름 충돌 가능성을 줄여 주고, 관련 있는 함수들을 구조화 할 수 있는 효과가 있다.

&nbsp;  

### 5.5. 클래스에서 정의한 메소드의 특징

* `function` 키워드를 생략한 **메소드 축약 표현**을 사용한다.
* 객체 리터럴과는 다르게 클래스에 메소드를 정의할 때는 쉼표(`,`)가 필요 없다.
* 암묵적으로 strict 모드가 실행된다.
* for...in 문 혹은 Object.keys 메소드 등으로 클래스의 메소드를 열거할 수 없다.([[Enumerable]] 내부 슬롯의 값이 false이다.)
* 내부 메소드 [[Construct]]를 갖지 않는 **non-constructor**이다. 따라서 `new` 연산자와 함께 호출할 수 없다.

&nbsp;  

## 6. 클래스의 인스턴스 생성 과정

자바스크립트 엔진은 **클래스 선언문**을 런타임 이전 함수 객체로 평가한 후 생성한 함수 객체를 클래스 이름과 동일한 식별자에 바인딩한다. (함수 호이스팅과 동일)

또한 생성된 함수 객체의 prototype 프로퍼티가 가리키는 객체, 즉 프로토타입 객체를 생성하고 프로토타입 객체의 constructor 프로퍼티에 생성자 함수의 참조를 할당한다. (normal 함수 객체 생성 과정과 동일)

이때, **클래스 몸체에 정의된 정적 메소드와 프로토타입 메소드도 생성자 함수와 프로토타입 객체에 각각 추가된다.** 함수 선언문으로 정의한 생성자 함수를 사용하면, 정적 메소드와 프로토타입 메소드를 런타임에 동적으로 추가해야한다. 하지만 클래스의 정적 메소드와 프로토타입 메소드는 클래스가 평가되는 시점에 함수 객체와 프로토타입 객체가 추가된다.

&nbsp;  

`new` 연산자와 함께 클래스를 호출하면 생성자 함수와 마찬가지로 클래스의 내부 메소드 [[Construct]]가 호출된다. 클래스는 `new` 연산자 없이 호출할 수 없다.

**1. 인스턴스 생성과 this 바인딩**

1. `new` 연산자와 함께 클래스를 호출하면 constructor 내부 코드가 실행되기 전, 암묵적으로 빈 객체(인스턴스) 생성된다.
2. 인스턴스의 프로토타입 결정 (`클래스.prototype`)
3. 인스턴스를 this에 바인딩한다. 따라서 constructor 내부의 this는 클래스가 생성한 인스턴스를 가리킨다.

&nbsp;  

**2. 인스턴스 초기화**

constructor의 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티 값을 초기화한다. 만약 constructor가 생략되었다면 이 과정도 생략된다.

&nbsp;  

**3. 인스턴스 반환**

클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
    console.log(this); // Person {}
    console.log(this.__proto__ === Person.prototype); // true
    
    // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
    this.name = name;
    
    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
  }
  
  // 프로토타입 메소드는 클래스의 prototype에 메소드로 이미 추가되어있다.
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
  
  // 정적 메소드는 클래스에 메소드로 이미 추가되어있다.
  static sayHello() {
    console.log('Hello!');
  }
}
```

&nbsp;  

## 7. 프로퍼티

### 7.1. 인스턴스 프로퍼티

**인스턴스 프로퍼티는 constructor 내부에서 정의해야 한다.**

```javascript
class Person {
  constructor(name) {
    // 인스턴스 프로퍼티
    this.name = name;
  }
}

const me = new Person('Kim');
console.log(me); // Person { name: 'Kim' }
```

constructor 내부 코드가 실행되기 이전에 이미 인스턴스는 this에 바인딩되어 있다. 생성자 함수에서 생성자 함수가 생설할 인스턴스의 프로퍼티를 정의하는 것과 마찬가지로 constructor 내부에서 this에 인스턴스 프로퍼티를 추가한다. 이로써 클래스가 암묵적으로 생성한 빈 객체, 즉 인스턴스에 프로퍼티가 추가되어 인스턴스가 초기화된다.

```javascript
class Person {
  constructor(name) {
    // 인스턴스 프로퍼티
    this.name = name; // name 프로퍼티는 public하다.
  }
}

const met = new Person('Kim');

// name은 public하다.
console.log(me.name); // Kim
```

constructor 내부에서 this에 추가한 프로퍼티는 언제나 클래스가 생성한 인스턴스의 프로퍼티가 된다. ES6의 클래스는 다른 객체지향 언어처럼 private, public, protected 키워드와 같은 접근 제한자(access modifier)를 지원하지 않는다. 따라서 **인스턴스 프로퍼티는 언제나 public하다.**

&nbsp;  

### 7.2. 접근자 프로퍼티

접근자 프로퍼티(accessor property)는 자체적으로는 값([[Value]] 내부 슬롯)을 갖지 않고, 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(accessor function)로 구성된 프로퍼티이다.

접근자 프로퍼티는 클래스에서도 사용할 수 있다.

```javascript
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  
  // fullName은 접근자 함수로 구성된 접근자 프로퍼티이다.
  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  
  // setter 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
}

const me = new Person('Jin', 'Kim');

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조
console.log(`${me.firstName} ${me.lastName}`);

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 할당하면 setter 함수가 호출된다.
me.fullName = 'Joon Park';

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(me.fullName); // Joon Park
```

**getter는 인스턴스 프로퍼티에 접근할 때마다** 프로퍼티 값을 조작하는 행위가 필요할 때 사용한다. getter는 메소드 이름 앞에 `get` 키워드를 사용해 정의한다. **setter는 인스턴스 프로퍼티에 값을 할당할 때마다** 프로퍼티 값을 조작하는 행위가 필요할 때 사용한다. setter는 메소드 이름 앞에 `set` 키워드를 사용해 정의한다.

이때 **getter와 setter는 호출하는 것이 아니라 프로퍼티처럼 참조하는 형식으로 사용**한다. getter를 참조하면 내부적으로 getter 함수가 호출된다. setter에 값을 할당하면 내부적으로 setter가 호출된다.

getter는 이름 그대로 무언가를 취득할 때 사용하므로 반드시 무언가를 반환해야 하고, setter는 무언가를 프로퍼티에 할당해야 할 때 사용하므로 반드시 매개 변수가 있어야 한다. 단, **setter는 단 하나의 값만을 할당 받기 때문에 단 하나의 매개 변수만을 선언할 수 있다.**

클래스의 메소드는 기본적으로 프로토타입 메소드가 된다. 따라서 **클래스의 접근자 프로퍼티 또한 인스턴스 프로퍼티가 아닌 프로토타입의 프로퍼티가 된다.**

&nbsp;  

### 7.3. 클래스 필드 정의 제안

* 클래스 필드 정의 제안으로 인해 **인스턴스 프로퍼티를 정의하는 방식은 2가지가 되었다.**
* 인스턴스를 생성할 때 외부 초기값으로 클래스 필드를 초기화할 필요가 있다면 constructor에서 인스턴스 프로퍼티를 정의하는 방식을 사용한다.
* 인스턴스를 생성할 때 외부 초기값으로 클래스 필드를 초기화할 필요가 없다면 2가지 방법 모두 사용할 수 있다.
* 클래스 필드는 클래스 몸체에서 정의한다.
* 클래스 필드를 정의할 때 this에 클래스 필드를 바인딩해서는 안된다. this는 클래스의 constructor와 메소드 내에서만 유효하다.
* 클래스의 constructor와 메소드 내에서 클래스 필드를 참조하려면 this 키워드를 사용해야 한다.
* 클래스 필드에 초기값을 할당하지 않으면 undefined를 갖는다.
* 함수는 일급 객체이므로 함수를 클래스 필드에 할당할 수 있다. 이때 할당된 함수는 인스턴스의 메소드로 추가된다.

&nbsp;  

**클래스 필드는** 클래스 기반 객체지향 언어에서 클래스가 생성할 **인스턴스의 프로퍼티를 가리키는 용어**이다. 자바스크립트의 경우, 인스턴스 프로퍼티를 선언하고 초기화하려면 반드시 생성자 함수 몸체 또는 클래스의 constructor 내부에서 this에 프로퍼티를 추가해야 한다. 하지만 클래스 필드 정의 제안 문법을 사용하면 클래스 몸체에서도 클래스 필드(인스턴스의 프로퍼티)를 정의할 수 있다.

```javascript
class Person {
  // 클래스 필드 정의
  name = 'Kim';
}

const me = new Person(); // Person { name: 'Kim' }
```

&nbsp;  

자바스크립트의 경우, 클래스 몸체에 메소드 만을 선언할 수 있다. 따라서 위 예제를 실행하면 문법 에러(SyntaxError)가 발생해야한다. 하지만 클래스 필드 정의 제안은 현재 TC39 프로세스의 stage 3(candidate)에 제안되어 있고, 최신 브라우저와 최신 Node.js는 ECMAScript 표준 사양으로 승급이 확실시되는 이 제안을 미리 구현해 놓았다. 따라서 최신 브라우저와 최신 Node.js에서는 위 예제와 같이 클래스 필드를 클래스 몸체에 정의할 수 있다.

클래스 몸체에서 클래스 필드를 정의하는 경우 this에 클래스 필드를 바인딩해서는 안된다. this는 클래스의 constructor와 메소드 내에서만 유효하다.

```javascript
class Person {
  // this에 클래스 필드를 바인딩해서는 안된다.
  this.name = ''; // SyntaxError: Unexpected token '.'
}
```

&nbsp;  

클래스 필드를 참조하는 경우, 자바스크립트에서는 this를 반드시 사용해야 한다.

```javascript
class Person {
  // 클래스 필드
  name = 'Kim';
  
  constructor() {
    console.log(name); // ReferenceError: name is not defined
  }
}

new Person();
```

&nbsp;  

클래스 필드에 초기값을 할당하지 않으면 undefined를 갖는다.

```javascript
class Person {
  // 클래스 필드를 초기화하지 않으면 undefined를 갖는다.
  name;
}

const me = new Person();
console.log(me); // Person { name: undefined }
```

&nbsp;  

인스턴스를 생성할 때, 외부의 초기값으로 클래스 필드를 초기화해야 할 필요가 있다면 constructor에서 클래스 필드를 초기화해야 한다.

```javascript
class Person {
  name;
  
  constructor(name) {
    // 클래스 필드 초기화
    this.name = name;
  }
}

const me = new Person('Kim');
console.log(me); // Person { name: 'Kim' }
```

이처럼 인스턴스를 생성할 때, 클래스 필드를 초기화할 필요가 없다면 constructor 밖에서 클래스 필드를 정의할 필요가 없다. 클래스 필드를 초기화할 필요가 있다면 어차피 constructor 내부에서 클래스 필드를 참조하여 초기값을 할당해야 한다. 이때 this, 즉 클래스가 생성한 인스턴스에 클래스 필드에 해당하는 프로퍼티가 없다면 자동 추가되기 때문이다.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

const me = new Person('Kim');
console.log(me); // Person { name: 'Kim' }
```

&nbsp;  

함수는 일급 객체이므로 함수를 클래스 필드에 할당할 수 있다. 이때 할당된 함수는 인스턴스의 메소드로 추가된다.

```javascript
class Person {
  // 클래스 필드에 문자열을 할당
  name = 'Kim';
	
	// 클래스 필드에 함수를 할당
	getName = function () {
    return this.name;
  }
	// 화살표 함수로 정의할 수도 있다.
	// getName = () => this.name;
}

const me = new Person();
console.log(me); // Person { name: 'Kim', getName: f }
console.log(me.getName()); // Kim
```

&nbsp;  

### 7.4. private 필드 정의 제안

* private 필드의 선두에는 `#`을 붙여준다. private 필드를 참조할 때도 `#`을 붙어주어야 한다.
* private 필드는 클래스 몸체에 정의한다.
* private 필드는 private 필드를 소유한 클래스 내에서만 접근할 수 있다. 다만, 접근자 프로퍼티를 통해 간접적으로 접근하는 방법은 유효하다.

&nbsp;  

constructor 내부에서 this를 통해 정의한 인스턴스 프로퍼티는 인스턴스를 통해 클래스 외부에서 언제나 참조할 수 있다. 즉, 언제나 public이다.

생성자 함수에서는 클로저를 사용하여 private한 프로퍼티를 흉내낼 수 있었다. 단, private한 프로퍼티를 흉내낸 자유 변수와 같은 이름의 프로퍼티에 접근하면 에러가 발생하지 않고 undefined를 반환하는 아쉬움이 있다. 또한, 여러 개의 인스턴스를 생성하면 프로토타입 메소드 내부에서 참조하는 자유변수의 값이 변경된다는 치명적 약점이 있다.

```javascript
// ES5
var Person = (function () {
  var _name = '';
  
  // 생성자 함수
  function Person(name) {
    _name = name;
  }
  
  // 프로토타입 메소드
  Person.prototype.sayHi = function () {
    console.log('Hi ' + _name);
  }
  
  return Person;
}());

// 인스턴스 생성
var me = new Person('Kim');
console.log(me._name); // undefined
me.sayHi(); // Hi Kim

var you = new Person('Park');
you.sayHi(); // Hi Park
me.sayHi(); // Hi Park
```

&nbsp;  

클래스 필드 정의 제안을 사용하더라도 클래스 필드는 인스턴스의 프로퍼티이기 때문에 마찬가지로 pulbic하다.

```javascript
class Person {
  // 클래스 필드는 인스턴스의 프로퍼티이므로 public하다
  name = 'Kim';
}

const me = new Person();
console.log(me.name); // Kim
```

&nbsp;  

2020년 5월 현재, TC39 프로세스의 stage 3(candidate)에는 **private 필드를 정의할 수 있는 새로운 표준 사양이 제안되어 있다.** 표준 사양으로 승급이 확실시 되는 이 제안도 최신 브라우저와 최신 Node.js에 이미 구현되어 있다.

private 필드의 선두에는 `#`을 붙여준다. private 필드를 참조할 때도 `#`을 붙어주어야 한다.

```javascript
class Person {
  // public 필드 정의
  name = '';
  // private 필드 정의
  #age;
  
  constructor(name, age) {
    // public 필드 참조
    this.name = name;
    // private 필드 참조
    this.#age = age;
  }
}

const me = new Person('Kim', 100);
console.log(me.name); // Kim
console.log(me.#age); // private 필드 #name은 클래스 외부에서 참조할 수 없다.
// SyntaxError: Private field '#name' must be declared in an enclosing class
```

&nbsp;  

public 필드는 어디서든지 참조할 수 있지만, private 필드는 클래스 내부에서만 참조할 수 있다.

| 접근 가능성                 | public | private |
| --------------------------- | ------ | ------- |
| 클래스 내부                 | O      | O       |
| 자식 클래스 내부            | O      | X       |
| 클래스 인스턴스를 통한 접근 | O      | X       |

즉, 부모 클래스를 포함한 클래스 외부에서 private 필드에 직접 접근할 수 있는 방법은 없다. 다만, 접근자 프로퍼티를 통해 간접적으로 접근하는 방법은 유효하다.

```javascript
class Person {
  // private 필드 정의
  #age;
  
  constructor(age) {
    this.#age = age;
  }

	get age() {
    return this.#age;
  }

	set age(age) {
    this.#age = age;
  }
}

const me = new Person(10);
// console.log(me.#name); // 접근 불가
console.log(me.age); // 10 (getter 접근자 프로퍼티 참조)
me.age = 100; // setter 프로퍼티 값 할당
console.log(me.age); // 100 (getter 접근자 프로퍼티 참조)
```

&nbsp;  

private 필드는 반드시 클래스 몸체에 정의해야 한다. private 필드를 직접 constructor에 정의하면 에러가 발생한다.

```javascript
class Person {
  constructor(name) {
    // private 필드는 클래스 몸체에서 정의해야 한다.
    this.#name = name;
    // SyntaxError: Private field '#name' must be declared in an enclosing class
  }
}
```

&nbsp; 

### 7.5. static 필드 정의 제안

* static 필드와 static private 필드는 2020년 5월 현재 최신 브라우저와 최신 Node.js에 구현되어 있다.

&nbsp;  

클래스에는 `static` 키워드를 사용하여 정적 메소드를 정의할 수 있다. 하지만 `static` 키워드를 사용하여 정적 필드를 정의할 수는 없었다. 하지만 static public 필드, static private 필드, static private 메소드를 정의할 수 있는 새로운 표준 사양인 "Static class features"가 2020년 5월 현재, TC39 프로세스의 stage 3(candidate)에 제안되어 있다. 이 제안 중 static public / private 필드는 최신 브라우저와 최신 Node.js에 이미 구현되어 있다.

```javascript
class MyMath {
  // static public 필드 정의
  static PI = 22 / 7;

	// static private 필드 정의
  static #num = 10;
  
  // static 메소드
  static increment() {
    return ++MyMath.#num;
  }
}

console.log(MyMath.PI); // 3.14.....
console.log(MyMath.increment()); // 11
console.log(MyMath.#num); // SyntaxError
```

&nbsp;  

## 8. 상속에 의한 클래스 확장

### 8.1. 클래스 상속과 생성자 함수 상속

* 상속에 의한 클래스 확장은 기존의 클래스를 상속받아 새로운 클래스를 확장(extends)하여 정의하는 것이다.
* 상속에 의한 클래스 확장은 코드의 재사용 관점에서 매우 유용하다.
* 생성자 함수는 클래스와 같이 상속을 통해 다른 생성자 함수를 확장할 수 있는 문법이 제공되지 않는다.

&nbsp;  

프로토타입 기반 상속은 프로토타입 체인에 의해 다른 객체의 자산을 상속 받는 개념이지만, **상속에 의한 클래스 확장은 기존의 클래스를 상속받아 새로운 클래스를 확장(extends)하여 정의**하는 것이다.

<img src="https://user-images.githubusercontent.com/32444914/82306071-8a096780-99f9-11ea-9a42-88b971e2ab5a.png" width="80%" />

클래스와 생성자 함수는 인스턴스를 생성할 수 있는 함수라는 점에서 매우 유사하다. 하지만 클래스는 상속을 통해 기존의 클래스를 확장할 수 있는 문법이 기본적으로 제공되지만, 생성자 함수는 그렇지 않다.

예를 들어 동물을 추상화한 Animal 클래스와 새와 사자를 추상화한 Bird, Lion 클래스를 정의한다고 생각해보자. 새와 사자는 동물에 속하므로 동물의 속성을 가진다. 하지만 새와 사자는 자신만의 고유한 속성도 가진다. 이때 Animal 클래스는 동물의 속성을 표현하고, Bird, Lion 클래스는 상속을 통해 동물 클래스의 속성을 그대로 사용하고 자신만의 고유한 속성을 추가하여 확장할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/82306680-524eef80-99fa-11ea-8dad-23a7201c0bd7.png" width="60%" />

&nbsp;  

이처럼 **상속에 의한 클래스 확장은 코드 재사용 관점에서 매우 유용하다.** 상속을 통해 Animal 클래스를 확장한 Bird 클래스를 구현해 보자.

```javascript
class Animal {
  constructor(age, weight) {
    this.age = age;
    this.weight = weight;
  }
  
  eat() { return 'eat'; }
  
  move() { return 'move'; }
}

class Bird extends Animal {
  fly() { return 'fly'; }
}

const bird = new Bird(1, 5);

console.log(bird); // Bird {age: 1, weight: 5}
console.log(bird instanceof Bird); // true
console.log(bird instanceof Animal); // true

console.log(bird.eat()); // eat
console.log(bird.move()); // move
console.log(bird.fly()); // fly
```

상속에 의해 확장된 클래스 `Bird`가 생성한 인스턴스의 프로토타입 체인은 아래와 같다.

<img src="https://user-images.githubusercontent.com/32444914/82307249-0cdef200-99fb-11ea-9395-7fd111d63357.png" width="60%" />

클래스는 상속을 통해 다른 클래스를 확장할 수 있는 문법인 **extends 키워드**가 기본적으로 제공된다. `extends` 키워드를 사용한 클래스 확장은 간편하고 직관적이다. 하지만 **생성자 함수는 클래스와 같이 상속을 통해 다른 생성자 함수를 확장할 수 있는 문법이 제공되지 않는다.**

&nbsp;  

### 8.2. extends 키워드

* 상속을 통해 클래스를 확장하려면 `extends` 키워드를 사용하여 상속받을 클래스를 정의한다.
* `extends` 키워드의 역할은 수퍼 클래스와 서브 클래스 간의 상속 관계를 설정하는 것이다.
* 클래스도 프로토타입을 통해 상속 관계를 구현한다.
* 수퍼 클래스와 서브 클래스는 인스턴스의 프로토타입 체인 뿐만 아니라, 클래스 간은 프로토타입 체인도 생성한다.

&nbsp;  

상속을 통해 클래스를 확장하려면 `extends` 키워드를 사용하여 상속받을 클래스를 정의한다.

```javascript
// 수퍼(베이스/부모) 클래스
class Base {}

// 서브(파생/자식) 클래스
class Derived extends Base {}
```

상속을 통해 확장된 클래스를 서브 클래스(sub class), 파생 클래스(derived class), 혹은 자식 클래스(child class)라 부르고, 서브 클래스에게 상속된 클래스를 수퍼 클래스(super class), 베이스 클래스(base class), 혹은 부모 클래스(parent class)라 부른다.

`extends` 키워드의 역할은 **수퍼 클래스와 서브 클래스 간의 상속 관계를 설정하는 것이다.** 클래스도 프로토타입을 통해 상속 관계를 구현한다.

<img src="https://user-images.githubusercontent.com/32444914/82309213-d35bb600-99fd-11ea-8a8a-972a2906cb0e.png" width="60%" />

수퍼 클래스와 서브 클래스는 인스턴스의 프로토타입 체인 뿐만 아니라, 클래스 간의 프로토타입 체인도 생성한다. 이를 통해 프로토타입 메소드, 정적 메소드 모두 상속이 가능하다.

&nbsp;  

### 8.3. 동적 상속

`extends` 키워드는 생성자 함수를 상속받아 클래스를 확장할 수도 있다. 단, `extends` 키워드 앞에는 반드시 클래스가 와야 한다.

```javascript
// 생성자 함수
function Base(a) {
  this.a = a;
}

// 생성자 함수를 상속받는 서브 클래스
class Derived extends Base {}

const derived = new Derived(1);
console.log(derived); // Derived {a: 1}
```

&nbsp;  

`extends` 키워드 다음에는 클래스 뿐만 아니라 [[Construct]] 내부 메소드를 갖는 함수 객체를 반환하는 모든 표현식을 사용할 수 있다. 이를 통해 **동적으로 상속받을 대상을 결정할 수 있다.**

```javascript
function Base1() {}

class Base2 {}

let condition = true;

// 조건에 따라 동적으로 상속 대상을 결정하는 서브 클래스
class Derived extends (condition ? Base1 : Base2) {}

const derived = new Derived();
console.log(derived); // Derived {}

console.log(derived instanceof Base1); // true
console.log(derived instanceof Base2); // false
```

&nbsp;  

### 8.4. 서브 클래스의 constructor

클래스에 constructor를 생략하면 클래스에 아래와 같이 디폴트 constructor가 암묵적으로 정의된다.

```javascript
constructor() {}
```

&nbsp;  

수퍼 클래스를 상속 받는 서브 클래스의 constructor를 생략하면 아래와 같이 디폴트 constructor가 암묵적으로 정의된다. `args`는 `new` 연산자와 함께 클래스를 호출할 때 전달한 인수의 리스트이다.

`super()`는 수퍼 클래스의 constructor(super-constructor)를 호출하여 인스턴스를 생성한다.

```javascript
constructor(...args) { super(...args); }
```

&nbsp;  

아래 예제에서 수퍼 클래스와 서브 클래스 모두 constructor를 생략하였다.

```javascript
// 수퍼 클래스
class Base {}

// 서브 클래스
class Derived extends Base {}
```

위 예제는 아래와 같이 암묵적으로 디폴트 constructor가 정의된다.

```javascript
// 수퍼 클래스
class Base {
  constructor() {}
}

// 서브 클래스
class Derived extends Base {
  constructor() { super(); }
}

const derived = new Derived();
console.log(derived); // Derived {}
```

위 예제와 같이 수퍼 클래스와 서브 클래스 모두 constructor를 생략하면 빈 객체가 생성된다. 프로퍼티를 소유하는 인스턴스를 생성하려면 constructor 내부에서 인스턴스에 프로퍼티를 추가해야 한다.

&nbsp;  

### 8.5. super 키워드

super 키워드는 함수처럼 호출할 수도 있고, this와 같이 식별자처럼 참조할 수 있는 특수한 키워드이다. super는 아래와 같이 동작한다.

* super를 호출하면 수퍼 클래스의 constructor(super-constructor)를 호출한다.
* super를 참조하면 수퍼 클래스의 메소드를 호출할 수 있다.

&nbsp;  

#### &ast;&ast;super 호출&ast;&ast;

super를 호출하면 수퍼 클래스의 constructor(super-constructor)를 호출한다.

아래 예제와 같이 수퍼 클래스의 constructor 내부에서 추가한 프로퍼티를 그대로 갖는 인스턴스를 생성한다면, 서브 클래스의 constructor를 생략할 수 있다. 이때 `new` 연산자와 함께 서브 클래스를 호출하면서 전달한 인수는 모두 서브 클래스에 암묵적으로 정의된 디폴트 constructor의 super 호출을 통해 수퍼 클래스의 constructor에게 전달된다.

```javascript
// 수퍼 클래스
class Base {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}

// 서브 클래스
class Derived extends Base {
  // constructor(...args) { super(...args); }
}

const derived = new Derived(1, 2);
console.log(derived); // Derived {a: 1, b: 2}
```

&nbsp;  

아래 예제와 같이 수퍼 클래스에서 추가한 프로퍼티와 서브 클래스에서 추가한 프로퍼티를 모두 가지는 인스턴스를 생성한다면, 서브 클래스의 constructor를 생략할 수 없다. 이때 new 연산자와 함께 서브 클래스를 호출하면서 전달한 인수 중 수퍼 클래스의 constructor에게 전달할 필요가 있는 인수는 서브 클래스의 constructor에서 호출한 super를 통해 전달된다.

```javascript
// 수퍼 클래스
class Base {
  constructor(a, b) { // 4. 인수 전달
    this.a = a;
    this.b = b;
  }
}

// 서브 클래스
class Derived extends Base {
  constructor(a, b, c) { // 2. 인수 전달
    super(a, b); // 3. Base 클래스의 constructor(super) 호출
    this.c = c;
  }
}

const derived = new Derived(1, 2, 3); // 1. Derived 클래스 호출
console.log(derived); // Derived {a: 1, b: 2, c: 3}
```

&nbsp;  

**super 호출 시 주의사항**

1. 서브 클래스에서 constructor를 생략하지 않는 경우, 서브 클래스의 constructor에서는 반드시 super를 호출해야 한다.
2. 서브 클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없다.
3. super는 반드시 서브 클래스의 constructor에서만 호출한다. 서브 클래스가 아닌 클래스 또는 함수에서 호출하면 에러가 발생한다.

&nbsp;  

#### &ast;&ast;super 참조&ast;&ast;

메소드 내에서 super를 참조하면 수퍼 클래스의 메소드를 호출할 수 있다.

**1. 서브 클래스의 프로토타입 메소드 내에서 super.prop은 수퍼 클래스의 프로토타입 메소드 prop을 가리킨다.**

```javascript
// 수퍼 클래스
class Base {
  constructor(name) {
    this.name = name;
  }
  
  sayHi() {
    return `Hi! ${this.name}`;
  }
}

// 서브 클래스
class Derived extends Base {
  sayHi() {
    // super.sayHi는 수퍼 클래스의 프로토타입 메소드를 가리킨다.
    return `${super.sayHi()}. How are you doing?`;
  }
}

const derived = new Derived('Jin');
console.log(derived.sayHi()); // Hi! Jin. How are you doing?
```

&nbsp;  

super 참조를 통해 수퍼 클래스의 메소드를 참조하려면, super가 `수퍼클래스.prototype` 객체를 참조할 수 있어야 한다. 위 예제는 아래 예제와 동일하게 동작한다.

```javascript
// 수퍼 클래스
class Base {
  constructor(name) {
    this.name = name;
  }
  
  sayHi() {
    return `Hi! ${this.name}`;
  }
}

// 서브 클래스
class Derived extends Base {
  sayHi() {
    // __super는 Derived의 sayHi가 바인딩된 객체의 프로토타입을 가리킨다.
    // sayHi는 Derived.prototype에 바인딩되었으므로 __super는 Base.prototype을 가리킨다.
    const __super = Object.getPrototypeOf(Derived.prototype);
    return `${__super.sayHi.call(this)}. How are you doing?`;
  }
}
```

**super는 자신이 바인딩되어 있는 객체의 프로토타입을 가리킨다.** 위 예제에서 `Derived` 클래스의 `sayHi`는 `Derived.prototype`에 바인딩되어 있고, super는 `Derived.prototype`의 프로토타입인 `Base.prototype`을 가리킨다.  즉,  `수퍼클래스.prototype` 객체를 가리킨다. 따라서 위 예제의 `super.sayHi` 메소드는 `Base.prototype.sayHi` 메소드를 가리킨다.

`Base.prototype.sayHi`를 호출할 때 `call` 메소드로 this를 전달하지 않으면, `Base.prototype.sayHi` 메소드 내부의 this는 `Base.prototype`을 가리킨다. `Base.prototype.sayHi` 메소드는 프로토타입 메소드이기 때문에 내부의 this는 인스턴스를 가리켜야한다. `name` 프로퍼티는 인스턴스에 존재하기 때문이다.

<strong>이처럼 super 참조가 동작하기 위해서는 메소드가 자신을 바인딩하고 있는 객체(`Derived.prototype`)의 프로토타입(`Base.prototype`)를 찾을 수 있어야한다.</strong> 이를 위해 메소드는 내부 슬롯 [[HomeObject]]을 가지며 자신을 바인딩한 객체를 가리킨다.

&nbsp;  

super 참조를 의사 코드로 표현하면 아래와 같다.

```javascript
/*
[[HomeObject]]는 메소드 자신을 바인딩한 객체를 가리킨다.
이를 통해 메소드가 자신을 바인딩하고 있는 객체의 프로토타입을 찾을 수 있다.
예를 들어, Derived 클래스의 sayHi 메소드는 Derived.prototype에 바인딩된다.
따라서 Derived 클래스의 sayHi 메소드의 [[HomeObject]]는 Derived.prototype이고
이를 통해 Derived 클래스의 sayHi 메소드 내부의 super 참조가 Base.prototype으로 결정된다.
따라서 super.sayHi는 Base.prototype.sayHi를 가리키게 된다.
*/
super = Object.getPrototypeOf([[HomeObject]])
```

super 참조는 클래스의 전유물은 아니다. **객체 리터럴에서도 super 참조를 사용할 수 있다. 단, ES6의 메소드 축약 표현으로 정의된 함수만 가능하다.**

```javascript
const base = {
  sayHi() {
    return `Hi! ${this.name}`
  }
};

const derived = {
  __proto__: base,
  name: 'Kim',
  // ES6 메소드 축약 표현으로 정의한 메소드이다. 따라서 [[HomeObject]]를 가진다.
  sayHi() {
    return `${super.sayHi()}. How are you doing?`;
  }
};

console.log(derived.sayHi()); // Hi! Kim. How are you doing?
```

&nbsp;  

**2. 서브 클래스의 정적 메소드 내에서 super.prop은 수퍼 클래스의 정적 메소드 prop을 가리킨다.**

```javascript
// 수퍼 클래스
class Base {
  static sayHi() {
    return `Hi!`;
  }
}

// 서브 클래스
class Derived extends Base {
  static sayHi() {
    // super.sayHi는 수퍼 클래스의 정적 메소드를 가리킨다.
    return `${super.sayHi()} How are you doing?`;
  }
}

console.log(Derived.sayHi()); // Hi! How are you doing?
```

&nbsp;  

### 8.6. 상속 클래스의 인스턴스 생성 과정

자바스크립트 엔진은 클래스 선언문을 런타임 이전 함수 객체로 평가한 후 생성한 함수 객체를 클래스 이름과 동일한 식별자에 바인딩한다. (함수 호이스팅과 동일)

또한 생성된 함수 객체의 prototype 프로퍼티가 가리키는 객체, 즉 프로토타입 객체를 생성하고 프로토타입 객체의 constructor 프로퍼티에 생성자 함수의 참조를 할당한다. (함수 호이스팅과 동일)

이때, **클래스 몸체에 정의된 정적 메소드와 프로토타입 메소드도 생성자 함수와 프로토타입 객체에 각각 추가된다.** 함수 선언문으로 정의한 생성자 함수를 사용하면, 정적 메소드와 프로토타입 메소드를 런타임에 동적으로 추가해야한다. 하지만 클래스의 정적 메소드와 프로토타입 메소드는 클래스가 평가되는 시점에 함수 객체와 프로토타입 객체가 추가된다.

&nbsp;  

클래스가 단독으로 인스턴스를 생성하는 것 보다 상속 관계에 있는 두 클래스가 협력하여 인스턴스를 생성하는 과정은 좀 더 복잡하다.

직사각형을 추상화한 Rectangle 클래스와 상속을 통해 상속을 통해 클래스를 확장한 ColorRectangle 클래스를 정의해 보자.

```javascript
// 수퍼 클래스
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  
  getArea() {
    return this.width * this.height;
  }
  
  toString() {
    return `width = ${this.width}, height = ${this.height}`;
  }
}

// 서브 클래스
class ColorRectangle extends Rectange {
  constructor(width, height, color) {
    super(width, height);
    this.color = color;
  }
  
  // 메소드 오버라이딩
  toString() {
    return super.toString() + `, color = ${this.color}`;
  }
}

const colorRectangle = new ColorRectangle(2, 4, 'red');
console.log(colorRectangle); // ColorRectangle { width: 2, height: 4, color: 'red' }

// 상속을 통해 getArea 메소드를 호출
console.log(colorRectangle.getArea()); // 8
// 오버라이딩된 toString 메소드를 호출
console.log(colorRectangle.toString()); // width = 2, height = 4, color = red
```

ColorRectangle 클래스에 의해 생성된 인스턴스의 프로토타입 체인은 아래와 같다.

<img src="https://user-images.githubusercontent.com/32444914/82334298-bbe2f400-9a22-11ea-8be6-9463e5e3f72e.png" width="60%" />

서브 클래스(ColorRectangle)가 new 연산자와 함께 호출되면, 아래의 과정을 통해 인스턴스를 생성한다.

&nbsp;  

**1. 서브 클래스의 super 호출**

**클래스는 내부 슬롯 [[ConstructorKind]]을 갖는다.** [[ContructorKind]] 내부 슬롯은 클래스가 자바스크립트 엔진에 의해 평가될 때, 수퍼 클래스와 서브 클래스를 구분하기 위해 'base' 또는 'derived'를 자신의 값으로 가진다. 다른 클래스를 상속받지 않는 클래스는 그 값이 'base'이고, 다른 클래스를 상속 받는 서브 클래스는 그 값이 'derived'이다. 이를 통해 **수퍼 클래스와 서브 클래스는 new 연산자와 함께 호출되었을 때의 동작이 구분된다.**

다른 클래스를 상속받지 않는 클래스(그리고 생성자 함수)는 new 연산자와 함께 호출되었을 때 암묵적으로 빈 객체(인스턴스)를 생성하고 이를 this에 바인딩한다.

하지만 **서브 클래스는 자신이 직접 인스턴스를 생성하지 않고, 인스턴스 생성을 수퍼 클래스에게 위임한다.** 이것이 바로 서브 클래스의 constructor에서 반드시 super를 호출해야하는 이유이다.

서브 클래스(ColorRectangle)가 new 연산자와 함께 호출되면 서브 클래스 constructor 내부의 super 키워드가 함수처럼 호출된다. super를 호출하면 수퍼 클래스의 constructor(super-constructor)가 호출된다. 좀 더 정확히 말하자면 수퍼 클래스가 평가되어 생성된 함수 객체의 코드가 실행되기 시작한다.

만약 서브 클래스 constructor 내부에 super 호출이 없으면 에러가 발생한다. **실제로 인스턴스를 생성하는 주체는 수퍼 클래스이므로, 수퍼 클래스의 constructor를 호출하는 super가 호출되지 않으면 인스턴스를 생성할** 수 없기 때문이다.

&nbsp;  

**2. 수퍼 클래스의 인스턴스 생성과 this 바인딩**

수퍼 클래스의 constructor 내부의 코드가 실행되기 이전에 암묵적으로 빈 객체를 생성한다. 이 빈 객체가 바로 (아직 완성되지는 않았지만) 클래스가 생성한 인스턴스이다. 그리고 암묵적으로 생성된 빈 객체(인스턴스)는 this에 바인딩된다. 따라서 수퍼 클래스의 constructor 내부의 this는 생성된 인스턴스를 가리킨다.

```javascript
// 수퍼 클래스
class Rectangle {
  constructor(width, height) {
    // 암묵적으로 빈 객체(인스턴스) 생성 후 this에 바인딩
    console.log(this); // ColorRectangle {}
    // new 연산자와 함께 호출된 함수는 ColorRectangle이다.
    console.log(new.target); // ColorRectangle
    // ...
  }
  // ...
}
```

이때 인스턴스는 수퍼 클래스가 생성한 것이다. 하지만 new 연산자와 함께 호출된 클래스가 서브 클래스라는 것이 중요하다. 즉, new 연산자와 함께 호출된 함수를 가리키는 `new.target`은 서브 클래스를 가리킨다. 따라서 **인스턴스는 new.target이 가리키는 서브 클래스가 생성한 것으로 처리된다.**

이때 생성된 인스턴스의 프로토타입은 Rectangle.prototype이 아니라 new.target(서브 클래스)의 prototype 프로퍼티가 가리키는 객체 Color.prototype이다.

&nbsp;  

**3. 수퍼 클래스의 인스턴스 초기화**

수퍼 클래스의 constructor가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화한다.

&nbsp;  

**4. 서브 클래스 constructor로의 복귀와 this 바인딩**

super의 호출이 종료되고 컨트롤이 서브 클래스 constructor로 복귀한다. **이때 super가 반환한 인스턴스가 this에 바인딩된다. 이처럼 서브 클래스는 별도의 인스턴스를 생성하지 않고 super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용한다.**

```javascript
// 서브 클래스
class ColorRectangle extends Rectangle {
  constructor(width, height, color) {
    super(width, height);
    
    // super가 반환한 인스턴스가 this에 바인딩된다.
    console.log(this); // ColorRectangle {width: 2, height: 4}
  }
}
```

**이처럼 super가 호출되지 않으면 인스턴스가 생성되지 않으며 this 바인딩도 할 수 없다. 서브 클래스의 constructor에서 super를 호출하기 이전에 this를 참조할 수 없는 이유가 바로 이 때문이다.** 따라서 서브 클래스 constructor 내부의 인스턴스 초기화는 반드시 super 호출 이후에 처리되어야 한다.

&nbsp;  

**5. 서브 클래스의 인스턴스 초기화**

super 호출 이후, 서브 클래스의  constructor에 기술되어 있는 인스턴스 초기화가 실행된다. 즉,  this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화한다.

&nbsp;  

**6. 인스턴스 반환**

클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

&nbsp;  

## 출처

* [poiemaweb.com - 클래스](https://poiemaweb.com/fastcampus/class)

