# Object

### 객체란? 

원시 타입은 단 하나의 값만을 나타내지만, **객체 타입 (object / reference type)**은 다양한 타입의 값(primitive or another object)을 **하나의 단위**로 구성한 **자료 구조 (Data Structure)**이다. 원시 값은 변경 불가능한 값이지만 (immutable) **객체는 변경 가능한(mutable value) 값이다.**

``` javascript
var person = {
    name: 'Lee', // property
    gender: 'male' // property
};
```

자바스크립트의 객체는 **key**와 **value**로 구성된 **property의 집합**이다. 위의 코드를 살펴보면, `person`이라는 객체는 `name`과 `gender`라는 key를 가지고, 각 key는 `Lee`와 `male`이라는 value를 가지고 있다. 이처럼 key와 value가 **한쌍이되어 property**가 된다.



```javascript
var counter = {
    num: 0, // property
    increase: function() { // method
        this.num++;
    }
};
```

또한, 자바스크립트에서 사용할 수 있는 모든 값은 property 값이 될 수 있다. 따라서, **자바스크립드의 함수 역시 한 객체의 property 값으로 취급할 수 있다.** property 값이 함수일 경우, 일반 함수와 구분하기 위해 **method**라고 부른다.

* property : 객체의 상태 (state)를 나타내는 값 (data)
* method: property를 참조하고 조작할 수 있는 동작 (behavior) - 상태를 변경한다

---

### 객체 리터럴에 의한 객체 생성

C++과 Java 같은 **class** 기반 객체지향 언어는 class를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자 (constructor)를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.

```java
Car a = new Car();
```



하지만 자바스크립트는 **프로토타입** 기반 객체지향 언어로서, 클래스 기반 객체지향 언어와는 다른 다양한 객체 생성 방법이 존재한다.

* **객체 리터럴**
* Object 생성자 함수
* 생성자 함수
* Object.create method
* 클래스 (ES6)

위 방법 중 가장 일반적이고 간단한 방법은 **객체 리터럴**을 사용하는 방법이다. 객체 리터럴은 중괄호 내에 **0개 이상**의 프로퍼티를 정의한다. 객체 리터럴은 **변수에 할당이 이루어지는 시점에 해석되고 생성된다.**

```javascript
var empty = {}; // 빈 객체
console.log(typeof empty); // object

// 할당이 이루어지는 시점에 객체 리터럴이 해석되고 그 결과 객체가 생성된다 (not hoisted?)
var person = {
    name: 'Lee',
    sayHello: function() {
        console.log('Hello! My name is ${this.name}.');
    }
}; // 객체 리터럴의 중괄호는 코드 블록을 의미하지 않으므로 semicolon을 붙여준다 (표현식).

console.log(typeof person); // object
console.log(person); // {name: "Lee", sayHello: f}
```

객체 리터럴에 프로퍼티를 포함시켜 객체의 생성과 동시에 프로퍼티를 만들 수도 있고, **객체를 생성한 이후에 프로퍼티를 동적으로 추가할 수도 있다.**

---

### 프로퍼티 (Property)

프로퍼티 키와 프로퍼티 값으로 사용할 수 있는 값은 아래와 같다.

* property key: **빈 문자열을 포함하는 (??)** 모든 문자열 또는 symbol 값
* property value: 자바스크립트에서 사용할 수 있는 모든 값

프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로, 식별자 역할을 하지만 반드시 식별자 네이밍 규칙을 따라야하는 것은 아니다. 하지만, 식별자 네이밍 규칙을 따르지 않은 프로퍼티 키는 **반드시 따옴표를 사용해야한다.**

```javascript
var person = {
    first_name: 'Jinhyun', // 식별자 네이밍 규칙을 따른 property key
    'last-name': 'Kim' // 식별자 네이밍 규칠을 따르지 않은 property key
};
```



#### 프로퍼티 키 동적 생성

문자열 또는 문자열로 변환 가능한 값을 반환하는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 이 경우, 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야한다. 이를 Computed Property name (계산된 프로퍼티 이름)이라 한다.

``` javascript
var obj = {};
var key = 'first_name';

obj[key] = 'Jinhyun';

console.log(obj); // {first_name: 'Jinhyun'}
```



#### 프로퍼티 키 생성 시 주의사항

빈 문자열을 프로퍼티 키로 사용해도 에러가 발생하진 않지만, 키로서 의미를 갖지 못하므로 권장하지 않는다.

```javascript
var foo = {
    '' = ''
};

console.log(foo); // {'': ''}
```



프로퍼티 키에 문자열이나 symbol 값 이외의 값을 사용하면 **암묵적 타입 변환을 통해 문자열이 된다.**

```javascript
var foo = {
    0: 1,
    1: 2,
    2: 3
};

console.log(foo); // {0: 1, 1: 2, 2: 3}
```



자바스크립트의 예약어를 프로퍼티 키로 사용해도 에러가 발생하지 않지만, 권장하지 않는다.

```javascript
var foo = {
  var: '',
  function: ''
};

console.log(foo); // {var: '', function: ''}
```



이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 적용된다.

```javascript
var foo = {
    name: 'Lee',
    name: 'Kim'
};

console.log(foo); // {name: "Kim"}
```

---

### 메소드 (Method)

프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해 메소드 (method)라 부른다. 따라서, **메소드는 객체에 제한되어 있는 함수를 의미한다.**

```javascript
var point = {
  x: 1,
  y: 2,
  getCoordinate: function() {
    return `[ ${this.x}, ${this.y} ]`;
  }
};

console.log(point.getCoordinate()); // [ 1, 2 ]
```

---

### 프로퍼티 접근

프로퍼티 값에 접근하는 방법은 두 가지 있다.

* dot notation (마침표 표기법)
* bracket notation (대괄호 표기법)

프로퍼티 키가 식별자 네이밍 규칙을 따르는 이름이라면 위의 두 가지 방법을 모두 사용할 수 있다.

``` javascript
var person = {
    name: 'Lee'
};

// using dot notation
console.log(person.name); // Lee

// using bracket notation
console.log(person.['name']);
```

대괄호 표기법을 사용하는 경우, **대괄호 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다 (프로퍼티 키가 숫자로 이루어진 문자열인 경우만 제외).**  자바스크립트 엔진은 대괄호 내의 따옴표로 감싸지 않은 이름을 식별자로 취급하기 때문이다.

``` javascript
console.log(person[name]); // ReferenceError: name is not defined
```



반면, 프로퍼티 키가 식별자 네이밍 규칙을 **준수하지 않을 경우,** 반드시 대괄호 표기법을 사용해야한다. 단, 프로퍼티 키가 **숫자로 이루어진 문자열인 경우, 따옴표를 생략 가능하다.**

```javascript
var person = {
    'last-name': 'Lee',
    1: 10
};

console.log(person.'last-name');  // SyntaxError: Unexpected string
console.log(person.last-name);    // ReferenceError: name is not defined
console.log(person[last-name]);   // ReferenceError: last is not defined
console.log(person['last-name']); // Lee

// 프로퍼티 키가 숫자로 이루어진 문자열인 경우, 따옴표를 생략 가능하다.
console.log(person.1);     // SyntaxError: missing ) after argument list
console.log(person.'1');   // SyntaxError: Unexpected string
console.log(person[1]);    // 10 : person[1] -> person['1']
console.log(person['1']);  // 10
```



객체에 존재하지 않는 프로퍼티에 접근하면 `undefined`를 반환한다. 이때 `ReferenceError`가 발생하지 않는 것에 주의해야한다.

```javascript
var person = {
    name: 'Lee'
};
console.log(person.age); // undefined
```

---

### 프포퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

``` javascript
var person = {
    name: 'Lee'
};
// overwrite
person.name = 'Kim';

console.log(person); // {name: "Kim"}
```

---

### 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

``` javascript
var person = {
    name: 'Lee'
};

// person 객체에는 address 프로퍼티가 존재하지 않는다.
// 따라서 person 객체에 address 프로퍼티가 동적으로 생성되고 값이 할당된다.
person.address = 'Seoul';

console.log(person); // {name: "Lee", address: "Seoul"}
```



---

### 프로퍼티 삭제

`delete` 연산자는 객체의 프로퍼티를 삭제한다. 이때 `delete` 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다. 만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러없이 무시된다. 

``` javascript
var person = {
  name: 'Lee'
};

// 프로퍼티 동적 추가
person.address = 'Seoul';

// person 객체에 address 프로퍼티가 존재한다.
// 따라서 delete 연산자로 address 프로퍼티를 삭제할 수 있다.
delete person.address;

// person 객체에 age 프로퍼티가 존재하지 않는다.
// 따라서 delete 연산자로 age 프로퍼티를 삭제할 수 없다. 이때 에러가 발생하지 않는다.
delete person.age;

console.log(person); // {name: "Lee"}
```

---

### ES6에서 추가된 객체 리터럴의 확장 기능

#### 1. 프로퍼티 축약 표현

프로퍼티 값으로 들어오는 변수의 이름이, 프로퍼티 키의 이름과 동일할때 **프로퍼티 키를 생략할 수 있다. 이때 프로퍼티 키는 변수 이름으로 자동생성된다.**

```javascript
// ES5
var x = 1, y = 2;

var obj = {
  x: x,
  y: y
};

console.log(obj); // {x: 1, y: 2}


// ES6
let x = 1, y = 2;

// 프로퍼티 축약 표현
const obj = {x, y};
console.log(obj); // {x: 1, y: 2};
```



#### 2. 프로퍼티 키 동적 생성

...



#### 3. 메소드 축약 표현

```javascript
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee

// ES6
const obj = {
  name: 'Lee',
  // 메소드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```

