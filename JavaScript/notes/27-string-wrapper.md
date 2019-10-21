# String 레퍼 객체

String 객체는 원시타입인 문자열을 다룰 때 유용한 프로퍼티와 메소드를 제공하는 레퍼(wrapper) 객체이다. 변수 또는 객체 프로퍼티가 **문자열을 값으로 가지고 있다면**, String 객체의 별도 생성없이 **String 객체의 프로퍼티와 메소드를 사용할 수 있다.**

원시 타입이 wrapper 객체의 메소드를 사용할 수 있는 **이유**는 원시 타입으로 프로퍼티나 메소드를 호출할 때 **원시 타입과 연관된 wrapper 객체로 일시적으로 변환되어 프로토타입 객체를 공유하게 되기 때문이다.**

```javascript
const str = 'Hello world!';
console.log(str.toUpperCase()); // 'HELLO WORLD!'
```



## 1. String Constructor

String 객체는 String 생성자 함수를 통해 생성할 수 있다. 이때 전달된 인자는 모두 문자열로 변환된다.

```javascript
// new String(value);
let strObj = new String('Lee');
console.log(strObj); // [String: 'Lee']

strObj = new String(1);
console.log(strObj); // [String: '1']

strObj = new String(undefined);
console.log(strObj); // [String: 'undefined']
```



`new` 연산자를 사용하지 않고 String 생성자 함수를 호출하면 **String 객체가 아닌 문자열 리터럴로 반환한다.**

```javascript
var name = String('Jin');

console.log(typeof x, x); // string Jin
```



일반적으로 문자열을 사용할 때는 원시 타입 문자열을 사용한다.

```javascript
const str = 'Jin';
const strObj = new String('Jin');

console.log(str == strObj); // true
console.log(str === strObj); // false

console.log(typeof str); // string
console.log(typeof strObj); // object
```



## 2. String Property

문자열 내의 문자 갯수를 반환한다. String 객체는 length 프로퍼티를 소유하고 있으므로 유사 배열 객체이다.

**`String.length`** 

```javascript
const str1 = 'Hello';
console.log(str1.length); // 5

const str2 = '안녕하세요';
console.log(str2.length); // 5
```



## 3. String Method

String 객체의 모든 메소드는 **언제나 새로운 문자열을 반환한다.** 문자열은 변경 불가능(immutable)한 원시 값이기 때문이다.



**`String.prototype.charAt(index)`**

인수로 전달한 index를 사용하여 index에 해당하는 위치의 문자를 반환한다. index는 0 ~ (문자열 길이 - 1) 사이의 정수이다. 지정한 index가 문자열의 범위를 벗어난 경우 **빈문자열을 반환한다.**

```javascript
const str = 'Hello';

for (let i = 0; i < str.length; i++) {
  console.log(str.charAt(i)); // H e l l o
}

// 지정한 index가 범위를 벗어난 경우 빈문자열을 반환
console.log(str.charAt(5)); // ''
console.log(str.charAt(-1)); // ''
```



**`String.prototype.concat(str)`**

인수로 전달한 1개 이상의 문자열과 연결하여 새로운 문자열을 반환한다.

`concat` 메소드를 사용하는 것보다는 `+`, `+=` 할당 연산자를 사용하는 것이 성능상 유리하다.

```javascript
// str.concat(str1)
const firstName = 'Jin';
const lastName = 'Kim';

console.log(firstName.concat(lastName)); // JinKim
```



**`String.prototype.indexOf(string, fromIndex=0)`**

인수로 전달한 문자 또는 문자열을 대상 문자열에서 검색하여 **처음 발견된 곳의 index를 반환한다.** 발견하지 못한 경우 -1를 반환한다.

```javascript
const str = 'Hello World';

console.log(str.indexOf('l')); // 2
console.log(str.indexOf('or')); // 7

// 문자열 'or'을 8번 index에서부터 탐색
console.log(str.indexOf('or', 8)); // -1

// 문자열 'Hello'가 str 안에 포함되어 있다면,
if (str.indexOf('Hello') !== -1) {
  // do something
}
```



**`String.prototype.lastIndexOf(string, fromIndex=this.length - 1)`**

인수로 전달한 문자 또는 문자열을 대상 문자열에서 검색하여 **마지막으로 발견된 곳의 index를 반환한다.** 발견하지 못한 경우 -1을 반환한다.





**`String.prototype.replace`**



**`String.prototype.split`**



**`String.prototype.substring`**



**`String.prototype.slice`**



**`String.prototype.toLowerCase`**



**`String.prototype.toUpperCase`**



**`String.prototype.trim`**



**`String.prototype.repeat`**



**`String.prototype.include`**



