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



#### `String.prototype.charAt(index)`

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



#### `String.prototype.concat(string)`

인수로 전달한 1개 이상의 문자열과 연결하여 새로운 문자열을 반환한다.

`concat` 메소드를 사용하는 것보다는 `+`, `+=` 할당 연산자를 사용하는 것이 성능상 유리하다.

```javascript
// str.concat(str1)
const firstName = 'Jin';
const lastName = 'Kim';

console.log(firstName.concat(lastName)); // JinKim
```



#### `String.prototype.indexOf(string, fromIndex=0)`

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



#### `String.prototype.lastIndexOf(string, fromIndex=this.length - 1)`

인수로 전달한 문자 또는 문자열을 대상 문자열에서 검색하여 **마지막으로 발견된 곳의 index를 반환한다.** 발견하지 못한 경우 -1을 반환한다.

2번째 인수(fromIndex)가 전달되면 **검색 시작 위치를 fromIndex으로 이동하여 역방향으로 검색을 시작한다.** 이때 검색 범위는 fromIndex ~ 0이며 반환값은 indexOf 메소드와 동일하게 발견된 곳의 index이다.

```javascript
const str = 'Hello World';

console.log(str.lastIndexOf('World')); // 6
console.log(str.lastIndexOf('l')); // 9

// 5 ~ 0 인덱스를 탐색
console.log(str.lastIndexOf('o', 5)); // 4
// 8 ~ 0 인덱스를 탐색
console.log(str.lastIndexOf('o', 8)); // 7
```



#### `String.prototype.replace(searchValue, replacer)`

첫번째 인수로 전달한 문자열 또는 정규표현식을,

대상 문자열에서 검색하여,

두번째 인수로 전달한 문자열로 대체한다.

**검색된 문자열이 여럿 존재할 경우 첫번째로 검색된 문자열만 대체된다 (searchValue가 string일 경우).**

```javascript
// str.replace(searchValue, replacer)
const str = 'Hello world';

// 첫번째로 검색된 문자열만 대체하여 새로운 문자열을 반환
console.log(str.replace('world', 'Kim')); // 'Hello Kim'

// 특수한 교체 패턴을 사용할 수 있다. ($& = 검색된 문자열)
console.log(str.replace('world', '<strong>$&</strong>')); // Hello <strong>world</strong>

// 정규 표현식
console.log(str.replace(/hello/gi, 'Kim')); // Kim world

```

첫번째 인자에는 문자열 또는 정규표현식이 전달된다. 문자열의 경우 첫번째 검색 결과만이 대체되지만, 정규표현식을 사용하면 다양한 방식으로 검색할 수 있다.



#### `String.prototype.split(separator, limit)`

첫번째 인수로 전달한 문자열 또는 정규표현식을,

대상 문자열에서 검색하여,

문자열을 구분한 후

분리된 각 문자열로 이루어진 **배열을 반환한다** (원본 문자열은 변경되지 않는다).

```javascript
// str.split(separator, limit)
const str = 'How are you doing?';

// 공백으로 구분(단어로 구분)하여 배열로 반환한다.
console.log(str.split(' ')); // [ 'How', 'are', 'you', 'doing?' ]

// 인수가 없는 경우, 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.
console.log(str.split()); // [ 'How are you doing?' ]

// 각 문자를 모두 분리한다
console.log(str.split(''));
// [ 'H', 'o', 'w', ' ', 'a', 'r', 'e', ' ', 'y', 'o', 'u', ' ', 'd', 'o', 'i', 'n', 'g', '?' ]

// 공백으로 구분하여 배열로 반환한다. 단, 요소 수는 3개까지만 허용한다.
console.log(str.split(' ', 3)); // [ 'How', 'are', 'you' ]

// 'o'로 구분하여 배열로 반환한다.
console.log(str.split('o')); // [ 'H', 'w are y', 'u d', 'ing?' ]

```



#### `String.prototype.substring(start_index, end_index)`

첫번째 인수로 전달한 start 인덱스에 해당하는 문자부터 두번째 인자에 전달된 end 인덱스에 해당하는 문자의 **바로 이전 문자까지**를 모두 반환한다. 이때 첫번때 인수 < 두번째 인수의 관계가 성립된다.

* start index > end index: 두 인수는 교환된다
* end index가 생략된 경우: start index부터 해당 문자열의 끝까지 반환된다.
* index < 0 또는 NaN인 경우: index는 0으로 취급된다.
* index > str.length: index는 str.length로 취급된다.

```javascript
const str = 'Hello World'; // str.length === 11

console.log(str.substring(1, 4)); // ell

// start index > end index : 두 인수는 교환된다.
console.log(str.substring(4, 1)); // ell

// end index가 생략된 경우 : start index에서 해당 문자열의 끝까지를 반환
console.log(str.substring(4)); // o World

// index < 0 또는 NaN인 경우 : index는 0으로 취급된다.
console.log(str.substring(-2)); // Hello World

// index > str.length : index는 str.length로 취급된다.
console.log(str.substring(1, 12)); // ello World
console.log(str.substring(11)); // ''

```



#### `String.prototype.slice(start_index, end_index)`

`String.prototype.substring`과 동일하다. 단, `String.prototype.slice`는 **음수의 인수를 전달할 수 있다.**

```javascript
const str = 'hello world';

// index가 음수일 경우, index 이동 방향을 반대로 카운트한다
console.log(str.slice(-5)); // 'world'

// 2번째부터 마지막 문자까지 잘라내어 반환
console.log(str.slice(2)); // llo world

// 0번째부터 5번째 이전 문자까지 잘라내어 반환
console.log(str.slice(0, 5)); // hello

```



#### `String.prototype.toLowerCase()`

대상 문자열의 모든 문자를 소문자로 변경한다.

```javascript
console.log('Hello World!'.toLowerCase()); // hello world!
```



#### `String.prototype.toUpperCase()`

대상 문자열의 모든 문자를 대문자로 변경한다.

```javascript
console.log('Hello World!'.toUpperCase()); // HELLO WORLD!
```



#### `String.prototype.trim()`

대상 문자열 양쪽 끝에 있는 공백 문자를 제거한 문자열을 반환한다.

```javascript
const str = '   foo   ';

console.log(str.trim()); // 'foo'
console.log(str.trimStart()); // 'foo  '
console.log(str.trimEnd()); // '   foo'

```



#### `String.prototype.repeat(count)`

인수로 전달한 숫자만큼 반복해 연결한 새로운 문자열을 반환한다. count가 0이면 빈 문자열을 반환하고, 음수이면 `RangeError`를 발생시킨다.

```javascript
console.log('abc'.repeat(0)); // ''
console.log('abc'.repeat(1)); // 'abc'
console.log('abc'.repeat(2)); // 'abcabc'
console.log('abc'.repeat(-1)); // RangeError
```



#### `String.prototype.includes(searchString, index)`

인수로 전달한 문자열이 포함되어 있는지를 검사하고 결과를 불리언 값으로 반환한다. 두번째 인수는 옵션으로 검색할 위치를 나타내는 정수이다.

```javascript
const str = 'hello world';

console.log(str.includes('hello')); // true
console.log(str.includes(' ')); // true
console.log(str.includes('wo')); // true
console.log(str.includes('wow')); // false
console.log(str.includes('')); // true ?????????????????????????????????????????????
console.log(str.includes()); // false ??????????????????????????????????????????????

// String.prototype.indexOf 메소드로 대체할 수 있다.
console.log(str.indexOf('hello')); // 0 (-1이 아니면 존재한다는 뜻이다)
```





