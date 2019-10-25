# 클래스 (Class)

```javascript
function Person() {
  this.name = 'Kim';
}
// 프로토타입 메소드
Person.prototype.sayHi = function () {
  console.log(`Hi ${this.name}`);
};
// static method (정적 메소드)
Person.foo = function () {
  console.log("foo");
};

const person1 = new Person();

// ---------------------------------------------------

// 클래스 내부에서 프로토타입 메소드를 정의할때는 메소드 단축표기법만 쓸 수 있다.
class Person {
  // field (ECMAScript 검토중인 기능)
  // name = 'Lee';
  // 인스턴스 메소드
  // hi = function () {
  //   do something;
  // };
  // hi = () => console.log('hi');
    
  // 생성자 함수 역할 constructor
  constructor() {
    // 암묵적으로 객체를 생성하여 this에 바인딩
    this.name = 'Kim';
    
    // 인스턴스 메소드
    this.hi = function () {
      // do something
    }
    // return this;
  }
  // 프로토타입 메소드
  sayHi() {
    console.log(`Hi ${this.name}`);
  }
  // static 메소드
  static foo() {
    console.log("foo");
  }
}

const person2 = new Person();
```

클래스는 무조건 객체를 만드는 용도로 밖에 쓰이지 않는다.

클래스는 내부적으로 생성자 함수처럼 작동하고, 프로토타입을 생성하며 인스턴스를 찍어낸다. 

새로운 객체 생성 메커니즘으로 생각하면된다. 생성자 함수 방식보다 훨씬 엄격하다.

`new` 키워드 없이는 호출할 수 없다. 무조건 [[Construct]]이다.

`extends`와 `super` 키워드를 제공한다.

`super`는 super 클래스의 메소드를 부를때 사용



## 2. 클래스 정의

