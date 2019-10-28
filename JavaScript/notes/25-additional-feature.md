# ES6 함수의 추가 기능

## 1. 함수의 구분

ES6 이전의 함수는 동일한 함수라도 다양한 형태로 호출할 수 있다.

```javascript
var foo = function () {
  return 1;
};

// 일반 함수로서 호출
foo(); // 1

// 생성자 함수로서 호출
new foo(); // foo {}

// 메소드로서 호출
var obj = { a: foo };
obj.a(); // 1
```

이는 언뜻 보면 편리한 것 같지만, 실수를 유발시킬 수 있으며 성능면에서도 손해이다. ES6 이전까지 함수는 사용 목적에 따라 명확히 구분되지 않는다. **ES6 이전의 모든 함수는 callable이며 constructor이다.** 따라서 우리가 흔히 메소드라고 부르는 객체에 바인딩된 함수도 callable이며 constructor이다. 객체에 바인딩된 함수를 생성자 함수로 호출하는 경우가 흔치는 않겠지만 문법상 가능하다는 것은 성능면에서도 문제가 있다.

```javascript
// obj의 프로퍼티 f에 할당된 것은 일반 함수이다.
var obj = {
  x: 10,
  f: function () {
    return this.x;
  }
};

// 하지만 ES6 이전의 모든 함수는 callable이며 constructor이다.
var foo = new obj.f();
console.log(foo); // f {}

// 메소드로서 호출
console.log(obj.f()); // 10

// 일반 함수로서 호출
var bar = obj.f;
bar(); // undefined
```

객체에 바인딩된 함수가 constructor라는 것은 prototype 프로퍼티에 바인딩된 프로토타입 객체를 생성한다는 것을 의미한다. 심지어 고차 함수의 인수로 전달된 콜백 함수도 constructor이기 때문에 불필요한 프로토타입 객체를 생성한다.

```javascript
[1, 2, 3].map(function (item) {
  return item * 2;
}); // [2, 4, 6]
```



ES6 이전의 모든 함수의 문제점은 아래와 같다. 

1. 사용 목적에 따라 명확한 구분이 없으므로 호출 방식에 제약이 없다.
2. 생성자 함수로 호출되지 않아도 프로토타입 객체를 생성한다.

이러한 문제를 해결하기 위해 ES6에서는 사용 목적에 따라 함수를 **세 가지 종류로 명확히 구분하였다.**

| ES6 함수의 구분    | constructor | prototype | super | arguments |
| ------------------ | ----------- | --------- | ----- | --------- |
| 일반 함수(Normal)  | O           | O         | X     | O         |
| 메소드(Method)     | X           | X         | O     | O         |
| 화살표 함수(Arrow) | X           | X         | X     | X         |

일반 함수: 함수 선언문 혹은 함수 표현식으로 정의한 함수 (Consturctor)

메소드: 메소드 축약형으로 정의한 함수 (Non- constructor)

화살표 함수: 화살표 함수 문법을 사용하여 정의한 함수 (Non-constructor)



## 2. 메소드

일반적으로 메소드는 객체에 바인딩된 함수를 일컫는 의미로 사용되었다. 하지만 ES6 사양에서는 **메소드 축약 표현으로 정의한 함수 만을 의미한다.**

```javascript
const obj = {
  x: 1,
  // foo는 메소드이다.
  foo() {
    return this.x;
  },
  // bar에 바인딩된 함수는 메소드가 아닌 일반 함수이다.
  bar: function () {
    return this.x;
  }
};
```



**ES6의 메소드는 non-constructor이다.** 따라서 ES6의 메소드는 생성자 함수로서 호출할 수 없다. 또한 non-constructor이므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.

```javascript
new obj.foo(); // TypeError: obj.foo is not a constructor
new obj.bar(); // bar {}

Object.prototype.hasOwnProperty.call(obj.foo, 'prototype'); // false
Object.prototype,hasOwnProperty.call(obj.bar, 'prototype'); // true
```



**ES6 메소드는** 자신이 바인딩된 객체를 가리키는 **내부 슬롯 [[HomeObject]]를 갖는다.** super 참조는 내부 슬롯 [[HomeObject]]를 사용하여 수퍼 클래스의 메소드를 참조하므로 ES6 메소드만이 super 키워드를 사용할 수 있다.

```javascript
const parent = {
  name: 'Kim',
  sayHi() {
    return `Hi! ${this.name}.`;
  }
};

const child {
  __proto__: parent,
  sayHi() {
    return `${super.sayHi()} How are you doing?`;
  }
};

console.log(child.sayHi()); // Hi! Kim. How are you doing?

const child2 = {
  __proto__: parent,
  // 이 곳의 sayHi는 일반 함수이다. 따라서 [[HomeObject]]를 갖지 않는다.
  sayHi: function () {
    // SyntaxError: 'super' keyword unexpected here
    return `${super.sayHi()}`
  }
};
```





## 3. 화살표 함수

화살표 함수(Arrow function)는 **익명 함수 표현식의 단축 표현이다.** `function` 키워드 대신 `=>`를 사용하여 보다 간략함 방법으로 함수를 정의할 수 있다. 하지만 기존의 함수와 다르게 동작하므로 모든 상황에 화살표 함수를 사용할 수 있는 것은 아니다.



### 3.1 화살표 함수 정의

##### 1. 매개 변수 선언

```javascript
// 매개 변수가 여러 개인 경우, 소괄호 안에 매개 변수를 선언한다.
(x, y) => {...}

// 매개 변수가 한 개인 경우, 소괄호를 생략할 수 있다.
x => {...}

// 매개 변수가 없는 경우 소괄호를 생략할 수 없다.
() => {...}
```



##### 2. 함수 몸체 정의

**함수 몸체가 한 줄의 문으로 구성된다면** 함수 몸체를 감싸는 중괄호 {}를 생략할 수 있다. 이때 문은 암묵적으로 반환된다.

```javascript
x => x * x; // x => { return x * x; }

const now = () => Date.now(); // () => { return Date.now(); }

const id = value => value; // value => { return value; }

const sum = (a, b) => a + b; // (a, b) => { return a + b };
```



**함수 몸체가 여러 줄의 문으로 구성된다면** 함수 몸체를 감싸는 중괄호 {}를 생략할 수 없다.

```javascript
const sum = (a, b) => {
  const result = a + b; // 생략 가능한 문이나, 예제를 위해 작성했다.
  return result;
};
```



**객체 리터를을 반환하는 경우,** 객체 리터럴을 소괄호 ()로 감싸 주어야 한다.

```javascript
() => ({}) // () => { return {}; }

const create = (id, content) -> ({ id, content });
```



화살표 함수도 즉시 실행 함수(IIFE)로 사용할 수 있다.

```javascript
const person = (name => {
  sayHi() {
    return `Hi! My name is ${name}`;
  }
}('Kim'));

console.log(person.sayHi()); // Hi! My name is Kim
```



화살표 함수도 일급 객체이므로 고차 함수에 인수로 전달될 수 있다.

```javascript
// ES5
[1, 2, 3].map(function (v) {
  return v * 2;
});

// ES6
[1, 2, 3].map(v => v * 2); // [2, 4, 6]
```

화살표 함수는 콜백 함수로서 정의할 때 유용하다. 표현도 간략하며, `this`를 사용하는 것도 편리하게 설계되었다. 이에 대해선 아래 자세히 설명하겠다.



### 3.2 화살표 함수와 일반 함수의 차이

##### 1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor이다.

```javascript
const Foo = () => ({});
new Foo(); // TypeRoor: Foo is not a constructor
```

화살표 함수는 non-constructor이기 때문에 prototype 프로퍼티를 가지지 않고, 프로토타입도 생성하지 않는다.

```javascript
Object.prototype.hasOwnProperty.call(Foo, 'prototype'); // false
```



##### 2. 중복된 매개 변수 이름을 선언할 수 없다.

```javascript
const arrow = (a, a) => a + a;
// SyntaxError: Duplicate parameter name not allowed in this context
```



##### 3. 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않는다.

따라서 화살표 함수 내부에서 this, arguments, super, new.target을 참조하면 스코프 체인을 통해 **상위 컨텍스트의 this, arguments, super, new.target을 참조한다.** 화살표 함수가 다른 화살표 함수의 중첩 함수인 경우, 상위 스코프에 존재하는 가장 가까운 함수 중에서 **화살표 함수가 아닌 부모 함수의 this, arguments, super, new.target을 참조한다.**



### 3.3 this

화살표 함수의 this는 일반 함수의 this와 다르게 동작한다. 이는 **중첩 함수 내부의 this가 외부 함수의 this와 다르기 때문에 발생하는 문제를 해결하기 위해 의도적으로 설계된 것이다.**

`this` 바인딩은 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다. 함수를 정의할 때 `this`에 바인딩할 객체가 결정되는 것이 아니다. 때문에 **중첩 함수가 일반 함수로 호출되면, 중첩 함수 내에 `this`는 늘 전역 객체를 가리킨다.** 외부 함수의 `this`와 중첩 함수의 `this`가 불일치한다는건 코드의 문맥 상 맞지 않는다.

```javascript
var obj = {
  foo() {
    console.log(this); // 인스턴스
      
    // 중첩 함수 정의 후 일반 함수로 호출
    function bar() {
      console.log(this); // window (전역 객체)
    }
    bar();
  }
}

obj.foo();
```

이때 발생하는 문제가 바로 "중첩 함수 내부의 this 문제"이다. 즉, 중첩 함수의 this와 외부 함수의 this가 서로 다른 객체를 가리키고 있다. 이는, 고차 함수의 인수로 전달되는 콜백 함수에도 적용된다. ES6 이전에는 이러한 문제를 해결하기 위해 아래와 같이 두 가지 방법을 사용했다.

##### 1. 메소드를 호출한 인스턴스를 가리키는 this의 참조 값을 새로운 변수에 저장 후, 중첩 함수 (혹은 콜백 함수) 내부에서 사용한다.

```javascript
var obj = {
  foo() {
    console.log(this); // obj
    // 인스턴스를 가리키는 참조 값을 that에 저장
    const that = this;
      
    // 중첩 함수 정의 후 일반 함수로 호출
    function bar() {
      console.log(that); // obj
    }
    bar();
  }
}

obj.foo();

```



##### 2. Function.prototype.apply / call / bind

```javascript
var obj = {
  foo() {
    console.log(this); // obj
      
    // 중첩 함수 정의 후 Function.prototype.apply / call / bind로
    // bar 함수 내부의 this를 외부의 this로 갈아끼운다.
    function bar() {
      console.log(this); // obj
    }
    bar.apply(this);
    // bar.call(this);
    // bar.bind(this)();
  }
}

obj.foo();

```



##### 3. 인수로 this를 전달할 수 있는 고차 함수를 사용한다.

```javascript
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  prefixArray(arr) {
    // 인수로 전달된 배열 arr을 순회하며 배열의 모든 요소에 prefix를 추가한다.
    return arr.map(function (item) {
    // prefixer.prefix = 'Hi'
      return this.prefix + ' ' + item;
    }, this); // 여기서 주입한 this는 아래 prefixer 객체이다.
  }
}

const prefixer = new Prefixer('Hi');
console.log(prefixer.prefixArray(['Lee', 'Kim'])); // ['Hi Lee', 'Hi Kim']

```



ES6에서는 화살표 함수를 사용하여 "중첩 함수 내부의 this 문제"를 해결할 수 있다.

```javascript
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }
  
  prefixArray(arr) {
    // 앞서 말했듯, 화살표 함수 내부에는 this 바인딩이 없다.
    // 따라서, 화살표 함수 내부에서 this를 참조하면
    // 상위 컨텍스트의 this를 그대로 참조한다.
    // 이 곳에서 this는 prefixArray를 호출한 인스턴스를 가리킨다.
    return arr.map(item => `${this.prefix} ${item}`);
  }
}
```

화살표 함수는 함수 자체의 this 바인딩이 없기 때문에, 상위 컨텍스트의 this를 그대로 참조한다. 이를 Lexical this라 한다. 마치 렉시컬 스코프와 같이 **화살표 함수의 this는 함수가 정의된 위치에 의해 결정된다는 것을 의미한다.**

```javascript
// 화살표 함수는 함수 자체의 this 바인딩이 없다.
// 전역 함수 foo의 상위 컨텍스트는 전역이다.
// 화살표 함수 foo의 this는 전역 객체를 가리킨다.
const foo = () => console.log(this);
foo(); // window

// 중첩 함수 foo의 상위 컨텍스트는 즉시 실행 함수이다.
// 화살표 함수 foo의 this는 즉시 실행 함수의 this를 가리킨다.
(function () {
  const foo = () => console.log(this);
  foo();
}).call({ a: 1 }); // { a: 1 }

// increase 프로퍼티에 할당한 화살표 함수의 상위 컨텍스트는 전역이다.
// increase 프로퍼티에 할당한 화살표 함수의 this는 전역 객체이다.
const counter = {
  num: 1,
  increase: () => ++this.num
};

console.log(counter.increase()); // NaN
```

따라서, 화살표 함수를 Function.prototype.apply / call / bind로 특정 객체를 인수로 전달하여 호출하여도 화살표 함수의 this는 변하지 않는다.

```javascript
window.x = 1;

const normal = function () { return this.x; }
const arrow = () => this.x;

console.log(normal.call({ x: 10 })); // 10
console.log(arrow.call({ x: 10 })); // 1
```



화살표 함수의 this는 언제나 상위 컨텍스트의 this를 가리킨다고 했다. 그렇다면 클래스 필드 정의 제안을 사용하여 클래스 필드에 화살표 함수를 할당했을때 상위 컨텍스트는 무엇일까?

```javascript
class Person {
  // 클래스 필드 정의 제안
  name = 'Kim';
  sayHi = () => console.log(`Hi! ${this.name}`); // this는 무엇을 가리키는가?
}

const me = new Person();
me.sayHi(); // ??
```

**이전에 클래스 필드는 모두 인스턴스 프로퍼티가 된다고 했다.** 따라서 위의 예제는 아래와 동일하게 동작한다.

```javascript
class Person {
  constructor() {
    this.name = 'Kim';
    this.sayHi = () => console.log(`Hi! ${this.name}`);
  }
}
```

따라서 `sayHi` 클래스 필드에 할당한 화살표 함수의 상위 컨텍스트는 constructor이며, 화살표 함수의 `this`는 constructor의 `this`와 같다. 클래스 필드를 사용한 위 예제는 화살표 함수는 상위 컨텍스트의 this를 그대로 참조한다는 것을 보여주기 위함이다. 저런 식으로 인스턴스 프로퍼티를 생성하는 것은 좋은 방법이 아니다.

### 3.4 super

화살표 함수는 함수 자체의 super 바인딩이 없다. 따라서 화살표 함수 내부에서 super를 참조하면 상위 컨텍스트의 super를 참조한다.

```javascript
class Parent {
  constructor(name) {
    this.name = name;
  }
    
  sayHi() {
    return `Hi! ${this.name}.`;
  }
}

class Child extends Parent {
  // super 키워드는 ES6 메소드 내에서만 사용 가능하다.
  // 화살표 함수는 함수 자체의 super 바인딩이 없다.
  // 클래스 필드 sayHi의 상위 컨텍스트는 constructor이다.
  // 클래스 필드 sayHi의 super는 constructor의 super를 가리킨다.
  sayHi = () => `${super.sayHi()} How are you doing?`;
}

const child = new Child('Kim');

// child.sayHi()는 인스턴스 메소드이다.
console.log(child.sayHi()); // Hi! Kim. How are you doing?
```

super는 내부 슬롯 [[HomeObject]]를 갖는 ES6 메소드만이 사용할 수 있는 키워드이다. 위 예제의 `sayHi` 클래스 필드에 할당한 화살표 함수는 ES6 메소드가 아니지만, 상위 컨텍스트의 super를 그대로 참조하기 때문에 super 참조가 가능하다.



### 3.5 arguments

화살표 함수는 함수 자체의 arguments 바인딩이 없다. 따라서 화살표 함수 내부에서 arguments를 참조하면 상위 컨텍스트의 arguments를 참조한다.

```javascript
(function () {
  // 화살표 함수는 함수 자체의 arguments 바인딩이 없다.
  // 중첩 함수 foo의 상위 컨텍스트는 즉시 실행 함수이다.
  // 화살표 함수 foo의 arguments는 실행 함수의 arguments를 가리킨다.
  const foo = () => console.log(arguments); // {'0': 1, '1': 2}
  foo(3, 4); // 여기서 인수를 전달해도 arguments에 바인딩이 안된다.
}(1, 2));

// 전역 함수 foo의 상위 컨텍스트는 전역이다.
// 전역에는 arguments 객체가 없다. arguments 객체는 함수 내부에서만 유효하다.
const foo = () => console.log(arguments);
foo(1, 2); // ReferenceError: argument is not defined
```

이처럼 화살표 함수는 arguments 바인딩이 없다. 따라서 **화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 rest 파라미터를 사용해야한다.**



## 4. Rest 파라미터

### 4.1 기본 문법

Rest 파라마터(Rest Parameter, 나머지 매개변수)는 매개변수 이름 앞에 세 개의 `...`을 붙여서 정의한 매개변수를 의미한다. Rest 파라미터는 **함수에 전달된 인수들의 목록을 배열로 전달받는다.**

```javascript
function foo(...rest) {
  // 매개변수 rest는 인수들의 목록을 배열로 전달받는 Rest 파라미터이다.
  console.log(rest); // [1, 2, 3, 4, 5]
  
  // 매개변수 rest에는 배열이 할당된다.
  console.log(Array.isArray(rest)); // true
}

foo(1, 2, 3, 4, 5);
```



함수에 전달된 인수들은 **순차적으로 파라미터와 Rest 파라미터에 할당된다.**

```javascript
function foo(param, ...rest) {
  console.log(param); // 1
  console.log(rest); // [2, 3, 4, 5]
}

foo(1, 2, 3, 4, 5);

function bar(param1, param1, ...rest) {
  console.log(param1); // 1
  console.log(param2); // 2
  console.log(rest); // [3, 4, 5]
}

bar(1, 2, 3, 4, 5);
```



Rest 파라미터는 이름 그대로 먼저 선언된 파라미터에 할당된 인수를 제외한 **나머지 인수들이 모두 배열에 담겨 할당된다.** 따라서 Rest 파라미터는 반드시 **마지막 파라미터이어야 한다.**

```javascript
function foo(...rest, param1, parm2) {}

foo(1, 2, 3, 4, 5);
// SyntaxError: Rest parameter must be last formal parameter
```



Rest 파라미터는 단 하나만 선언할 수 있다.

```javascript
function foo(...rest1, ...rest2) {}

foo(1, 2, 3, 4, 5);
// SyntaxError: Rest parameter must be last formal parameter
```



Rest 파라미터는 함수 정의 시 선언한 매개변수 개수를 나타내는 **함수 객체의 `length` 프로퍼티에 영향을 주지 않는다.**

```javascript
function foo(...rest) {}
console.log(foo.length); // 0

function bar(x, y, ...rest) {}
console.log(bar.length); // 2
```



### 4.2 Rest 파라미터와 arguments 객체

인자의 개수를 사전에 알 수 없는 가변 인자 함수는, arguments 객체를 통해 인수를 확인한다. **arguments 객체**는 함수 호출 시 전달된 인수(arguments)들의 정보를 담고 있는 **순회 가능한(iterable) 유사 배열 객체(array-like object)이며** 함수 내부에서 지역 변수처럼 사용할 수 있다.

```javascript
// 매개변수의 개수를 사전에 알 수 없는 가변 인자 함수
function sum() {
  // 가변 인자 함수는 arguments 객체를 통해 인수를 전달 받는다.
  console.log(arguments);
}

sum(1, 2); // { length: 2, '0': 1, '1': 2 }
```



arguments 객체는 유사 배열 객체이므로 배열 메소드를 사용하려면 Function.prototype.call 메소드를 통해 this를 변경하여 배열 메소드를 호출해야 하는 번거로움이 있다.

```javascript
function sum() {
  // 유사 배열 객체인 arguments 객체를 배열로 변환한다.
  var arr = Array.prototype.slice.call(arguments);
  
  return array.reduce(function (pre, cur) {
    return pre + cur;
  });
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```



ES6에서는 rest 파라미터를 사용하여 가변 인자의 목록을 배열로 직접 전달받을 수 있다. 이를 통해 유사 배열인 arguments 객체를 배열로 변환하는 번거로움을 피할 수 있다.

```javascript
function sum(...args) {
  // Rest 파라미터 args에는 배열 [1, 2, 3, 4, 5]이 할당된다.
  return args.reduce((pre, cur) => pre + cur);
}
console.log(sum(1, 2, 3, 4, 5)); // 15
```



일반 함수와 메소드는 Rest 파라미터와 arguments 객체를 모두 사용할 수 있다. 하지만 **화살표 함수는 함수 자체의 arguments 객체를 갖지 않는다.** 따라서 화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 rest 파라미터를 사용해야 한다.

```javascript
var normal = function () {};
console.log(normal.hasOwnProperty('arguments')); // true

const arrow = () => {};
console.log(arrow.hasOwnProperty('arguments')); // false
```



## 5. 매개변수 기본값

ES6에서는 매개변수 기본값을 사용하여 함수 내에서 수행하던 인수 체크 및 초기화를 간소화할 수 있다. 매개변수 기본값은 매개변수에 인수를 전달하지 않았을 경우에만 유효하다.

```javascript
function sum(x = 0, y = 0) {
  return x + y;
}
// sum.length = 0; 질문

console.log(sum(1)); // 1
console.log(sum(1, 2)); // 3
```



매개변수 기본값은 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티와 arguments 객체에 영향을 주지 않는다.

```javascript
fuction foo(x, y = 0) {
  console.log(arguments);
}

console.log(foo.length); // 1

sum(1); // Arguments { '0': 1 }
sum(1, 2); // Arguments { '0': 1, '1': 2 }
```

