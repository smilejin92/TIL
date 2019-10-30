# 디스트럭처링 할당

디스트럭처링 할당(구조 분해 할당, Destructuring assignment)은 구조화된 배열 또는 객체를 Destructuring(비구조화, 구조파괴)하여 1개 이상의 변수에 개별적으로 할당하는 것을 말한다. 배열  또는 객체 리터럴에서 필요한 값만을 추출하여 변수에 할당할 때 유용하다.

## 1. 배열 디스트럭처링 할당

ES5에서 구조화된 배열을 디스트럭처링하여 1개 이상의 변수에 할당하기 위한 방법은 아래와 같다.

```javascript
// ES5
var arr = [1, 2, 3];

var a = arr[0];
var b = arr[1];
var c = arr[2];

console.log(a, b, c); // 1 2 3
```



ES6의 배열 디스트럭처링 할당은 배열의 각 요소를 배열로부터 추출하여 1개 이상의 변수에 할당한다. 이때 **할당 기준은 배열의 인덱스이다(순서대로 할당된다).** 

```javascript
const arr = [1, 2, 3];

// ES6 배열 디스트럭처링 할당
// 변수 a b, c를 선언하고 배열 arr을 디스트럭처링 하여 할당한다.
// 이때 할당 기준은 배열의 인덱스이다.
const [a, b, c] = arr;

console.log(a, b, c); // 1 2 3
```



배열 디스트럭처링 할당을 위해서는 할당 연산자 `=` 왼쪽에 **값을 할당 받을 변수를 선언해야 한다.** 이때 **여러 개의 변수를 배열 리터럴 형태로 선언**한다.

```javascript
let x, y;
[x, y] = [1, 2];

// 위의 문과 아래의 문은 동치이다.
const [x, y] = [1, 2];

// 할당 연산자 = 왼쪽에 변수를 배열 형태로 선선하면 반드시 우변에 배열을 할당해야 한다.
const [x, y];
// SyntaxError: Missing initializer in destructuring declaration
```



배열 디스트럭처링 할당의 기준은 배열의 인덱스이다(순서대로 할당된다). 이때 **변수의 개수와 배열 요소의 개수가 반드시 일치할 필요는 없다.**

```javascript
let x, y, z;

[x, y] = [1, 2]; // x = 1, y = 2
[x, y] = [1]; // x = 1, y = undefined
[x, y] = [1, 2, 3]; // x = 1, y = 2
[x, , z] = [1, 2, 3]; // x = 1, z = 3
```



배열 디스트럭처링 할당을 위한 **변수에 기본값을 설정할 수 있다.**

```javascript
let x, y, z;

// z에 기본 값을 설정
[x, y, z = 3] = [1, 2]; // x = 1, y = 2, z = 3

// 기본값보다 할당된 값이 우선한다.
[x, y = 10, z = 3] = [1, 2]; // x = 1, y = 2, z = 3
```



배열 디스트럭처링 할당은 배열에서 필요한 요소만 추출하여 변수에 할당하고 싶을 때 유용하다. 아래 예제는 Date에서 년, 월, 일을 추출하는 예제이다.

```javascript
const today = new Date(); // 2019-10-30T06:50:12.165Z
let formattedDate = today.toISOString().substring(0, 10); // "2019-10-30"

// 문자열을 분리하여 배열로 변환
formattedDate = formattedDate.split('-'); // ['2019', '10', '30']

// 배열 디스트럭처링 할당
const [year, month, day] = formattedDate;
console.log(year, month, day); // 2019 10 30
```



배열 디스트럭처링 할당을 위한 변수에 Rest 파라미터와 유사하게 Rest 요소(Rest element) `...`을 사용할 수 있다. Rest 요소는 Rest 파라미터와 마찬가지로 반드시 마지막에 위치해야 한다.

```javascript
// Rest 요소
const [x, ...y] = [1, 2, 3]; // x = 1, y = [1, 2]
```



## 2. 객체 디스트럭처링 할당

ES5에서 객체의 각 프로퍼티를 디스트럭처링하여 변수에 할당하기 위해서는 프로퍼티 키를 사용해야 한다.

```javascript
// ES5
var user = { firstName: 'Jin', lastName: 'Kim' };

var firstName = user.firstName;
var lastName = user.lastName;

console.log(firstName, lastName); // Jin Kim
```



ES6의 객체 디스트럭처링 할당은 객체의 각 프로퍼티를 객체로부터 추출하여 1개 이상의 변수에 할당한다. 배열 디스트럭처링 할당과 마찬가지로 객체 디스트럭처링 할당을 위해서는 할당 연산자 `=` 왼쪽에 값을 할당 받을 변수를 선언해야 한다.

이를 위해 **여러 개의 변수를 객체 리터럴 형태로 선언한다.** 이때 **할당 기준은 프로퍼티 키이다. 순서는 의미가 없으며 변수 이름과 프로퍼티 키가 일치하면 할당된다.** 

```javascript
const user = { firstName: 'Jin', lastName: 'Kim' };

// ES6 객체 디스트럭처링 할당
// 변수 lastName, firstName을 선언하고 객체 user를 디스트럭처링하여 할당한다.
// 이때 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다. 순서는 의미가 없다.
const { lastName, firstName } = user;
// lastName = user.lastName
// firstName = user.firstName

console.log(firstName, lastName); 
```

위 예제에서 객체 리터럴 형태로 선언한 변수는 `lastName`, `firstName`이다. 이는 프로퍼티 축약 표현을 통해 선언한 것이다.

```javascript
const { lastName, firstName } = user;
// 위와 아래는 동치이다.
const { lastName: lastName, fistName: firstName } = user;
```

따라서 **객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당 받으려면** 아래와 같이 변수를 선언한다.

```javascript
const user = { firstName: 'Jin', lastName: 'Kim' };

const { lastName: ln, firstName: fn } = user;
// ln = user.lastName
// fn = user.firstName

console.log(fn, ln); // Jin Kim
```



객체 디스트럭처링 할당을 위한 변수에 **기본값을 설정할 수 있다.**

```javascript
const { firstName = 'Jin', lastName } = { lastName: 'Kim' };
console.log(firstName, lastName); // Jin Kim

const { firstName: fn = 'Jin', lastName: ln } = { lastName: 'Kim' };
console.log(fn, ln); // Jin Kim
```



객체 디스트럭처링 할당은 프로퍼티 키로 객체에서 **필요한 프로퍼티 값만을 추출할 수 있다.**

```javascript
const todo = { id: 1, content: 'HTML', completed: true };

// todo 객체로부터 id 프로퍼티만을 추출한다.
const { id } = todo;
console.log(id); // 1
```



**배열의 요소가 객체인 경우, 배열 디스트럭처링 할당과 객체 디스트럭처링 할당을 혼용할 수 있다.**

```javascript
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: false },
  { id: 3, content: 'JS', completed: false }
];

// todos 배열의 두번째 요소인 객체로부터 id 프로퍼티만을 추출한다.
const [, { id }] = todos;
console.log(id); // 2
```



중첩 객체의 경우는 아래와 같이 사용한다.

```javascript
const user = {
  name: 'Kim',
  address: {
    zipCode: '98105',
    city: 'Seattle'
  }
};

const { address: { city } } = user;
console.log(city); // 'Seattle'
```



객체 디스트럭처링 할당을 위한 변수에 Rest 파라미터와 유사하게 Rest 프로퍼티 `...`을 사용할 수 있다 **(TC39 stage 4)**. Rest 프로퍼티는 Rest 파라미터와 마찬가지로 반드시 마지막에 위치해야 한다.

```javascript
// Rest 프로퍼티
const { x, ...rest } = { x: 1, y: 2, z: 3};
// x = 1
// rest = { y: 2, z: 3}
```

