# 클래스

## 1. 클래스는 프로토타입의 문법적 설탕인가?

* 클래스는 새로운 객체 생성 메커니즘이다.
* 클래스는 생성자 함수보다 엄격하며, 생성자 함수에서 제공하지 않는 기능을 제공한다.
  * `super`, `extends` 키워드 제공
  * 호이스팅이 발생하지 않는 것 처럼 동작 (선언문 이전에 참조하면 TDZ)
  * `new` 연산자와 함께 호출하지 않으면 에러 발생
  * 클래스 내의 모든 코드에는 암묵적으로 엄격 모드가 적용되며, 해지할 수 없다.
  * 클래스의 constructor, 프로토타입 메소드, 정적 메소드는 열거되지 않는다.

&nbsp;  

자바스크립트는 프로토타입 기반(prototype-based) 객체지향 언어다. 프로토타입 기반 객체지향 언어는 클래스가 필요 없은(class-free) 객체지향 프로그래밍 언어이다. ES5에서는 클래스 없이도 아래와 같이 생성자 함수와 프로토타입 체인, 클로저를 사용하여 객체 지향 언어의 상속, 캡슐화 등의 개념을 구현할 수 있었다.

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

* 메소드 내부에서 인스턴스 프로퍼티를 참조해야 할 필요가 있다면 this를 사용해야 한다. 이러한 경우, 프로토타입 메소드로 정의해야 한다
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

* `function` 키워드를 생략한 메소드 축약 표현을 사용한다.
* 객체 리터럴과는 다르게 클래스에 메소드를 정의할 때는 쉼표(`,`)가 필요 없다.
* 암묵적으로 strict 모드가 실행된다.
* for...in 문 혹은 Object.keys 메소드 등으로 클래스의 메소드를 열거할 수 없다([[Enumerable]] 내부 슬롯의 값이 false이다.)
* 내부 메소드 [[Construct]]를 갖지 않는 non-constructor이다. 따라서 `new` 연산자와 함께 호출할 수 없다.

&nbsp;  

## 6. 클래스의 인스턴스 생성 과정

`new` 연산자와 함께 클래스를 호출하면 생성자 함수와 마찬가지로 클래스의 내부 메소드 [[Construct]]가 호출된다. 클래스는 `new` 연산자 없이 호출할 수 없다.

### 1. 인스턴스 생성과 this 바인딩

1. `new` 연산자와 함께 클래스를 호출하면 constructor 내부 코드가 실행되기 전, 암묵적으로 빈 객체(인스턴스) 생성된다.
2. 인스턴스의 프로토타입 결정 (`클래스.prototype`)
3. 인스턴스를 this에 바인딩한다. 따라서 constructor 내부의 this는 클래스가 생성한 인스턴스를 가리킨다.

&nbsp;  

### 2. 인스턴스 초기화

constructor의 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티 값을 초기화한다. 만약 constructor가 생략되었다면 이 과정도 생략된다.

&nbsp;  

### 3. 프로토타입 / 정적 메소드 추가

클래스 몸체에 정의한 프로토타입 메소드가 존재하면 `클래스.prototype`에 추가한다. 클래스 몸체에 정의한 정적 메소드가 존재하면 클래스에 추가한다.

&nbsp;  

### 4. 인스턴스 반환

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
    
    // 4. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
  }
  
  // 3. 프로토타입 메소드는 클래스의 prototype에 메소드로 추가된다.
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
  
  // 3. 정적 메소드는 클래스에 메소드로 추가된다.
  static sayHello() {
    console.log('Hello!');
  }
}
```

&nbsp;  

## 7. 프로퍼티

### 7.1. 인스턴스 프로퍼티

인스턴스 프로퍼티는 constructor 내부에서 정의해야 한다.

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

constructor 내부에서 this에 추가한 프로퍼티는 언제나 클래스가 생성한 인스턴스의 프로퍼티가 된다. ES6의 클래스는 다른 객체지향 언어처럼 private, public, protected 키워드와 같은 접근 제한자(access modifier)를 지원하지 않는다. 따라서 인스턴스 프로퍼티는 언제나 public하다.

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

* 클래스 필드 정의 제안으로 인해 인스턴스 프로퍼티를 정의하는 방식은 2가지가 되었다.
* 인스턴스를 생성할 때 외부 초기값으로 클래스 필드를 초기화할 필요가 있다면 constructor에서 인스턴스 프로퍼티를 정의하는 방식을 사용한다.
* 인스턴스를 생성할 때 외부 초기값으로 클래스 필드를 초기화할 필요가 없다면 2가지 방법 모두 사용할 수 있다.

&nbsp;  

**클래스 필드는** 클래스 기반 객체지향 언어에서 클래스가 생성할 **인스턴스의 프로퍼티를 가리키는 용어**이다. 자바스크립트의 경우, 인스턴스 프로퍼티를 선언하고 초기화하려면 반드시 생성자 함수 몸체 또는 클래스의 constructor 내부에서 this에 프로퍼티를 추가해야 한다. 하지만 클래스 필드 정의 제안 문법을 사용하면 클래스 몸체에서도 클래스 필드(인스턴스의 프로퍼티)를 정의할 수 있다.

```javascript
class Person {
  // 클래스 필드 정의
  name = 'Kim';
}

const me = new Person(); // Person { name: 'Kim' }
```

자바스크립트의 경우, 클래스 몸체에 메소드 만을 선언할 수 있다. 따라서 위 예제를 실행하면 문법 에러(SyntaxError)가 발생해야한다. 하지만 클래스 필드 정의 제안은 현재 TC39 프로세스의 stage 3(candidate)에 제안되어 있고, 최신 브라우저와 최신 Node.js는 ECMAScript 표준 사양으로 승급이 확실시되는 이 제안을 미리 구현해 놓았다. 따라서 최신 브라우저와 최신 Node.js에서는 위 예제와 같이 클래스 필드를 클래스 몸체에 정의할 수 있다.

클래스 몸체에서 클래스 필드를 정의하는 경우 this에 클래스 필드를 바인딩해서는 안된다. this는 클래스의 constructor와 메소드 내에서만 유효하다.

```javascript
class Person {
  // this에 클래스 필드를 바인딩해서는 안된다.
  this.name = ''; // SyntaxError: Unexpected token '.'
}
```

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

클래스 필드에 초기값을 할당하지 않으면 undefined를 갖는다.

```javascript
class Person {
  // 클래스 필드를 초기화하지 않으면 undefined를 갖는다.
  name;
}

const me = new Person();
console.log(me); // Person { name: undefined }
```

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



### 7.5. static 필드 정의 제안

## 8. 상속에 의한 클래스 확장

### 8.1. 클래스 상속과 생성자 함수 상속

### 8.2. extends 키워드

### 8.3. 동적 상속

### 8.4. 서브 클래스의 constructor

### 8.5. super 키워드

### 8.6. 상속 클래스의 인스턴스 생성 과정

### 8.7. 표준 빌트인 생성자 함수 확장

