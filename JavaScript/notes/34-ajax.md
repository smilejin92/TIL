# 비동기식 처리 모델과 Ajax

## 1. Ajax (Asynchronous JavaScript and XML)

Ajax는 자바스크립트를 이용해서 **비동기적(Asynchronous)**으로 서버와 브라우저가 데이터를 교환할 수 있는 통신 방식을 의미한다.

서버로부터 웹페이지가 반환되면 화면 전체를 갱신해야 하는데 페이지 일부만을 갱신하고도 동일한 효과를 볼 수 있도록 하는 것이 Ajax이다.



## 2. JSON (JavaScirpt Object Notation)

JSON (JavaScript Object Notation)은 클라이언트와 서버 간 데이터 교환을 위한 데이터 포맷을 말한다.

자바스크립트의 객체 리터럴과 매우 흡사하다. 하지만 **JSON은 순수한 텍스트로 구성된 규칙이 있는 데이터 구조이다.**

```javascript
{
    "name": "Kim",
    "gender": "male",
    "age": 20,
    "alive": true
}
```

**키는 반드시 큰따옴표로 둘러싸야한다.**



### 2.1. JSON.stringify

객체를 JSON 형식의 문자열로 변환한다.

```javascript
const obj = { name: 'Kim', gender: 'male', age: 20 };

// 객체 -> JSON 형식의 문자열
const strObj = JSON.stringify(obj);
console.log(typeof strObj, strObj);
// string {"name":"Kim","gender":"male","age":20}

// 객체 -> JSON 형식의 문자열 + prettify
const strPrettyObj = JSON.strignify(obj, null, 2);
console.log(typeof strPrettyObj, strPrettyObj);
/*
string {
	"name": "Kim",
	"gender": "male",
	"age": 20
}
*/

// replacer
// 값의 타입이 Number이면 필터링되어 반환되지 않는다.
function filter(key, value) {
    // undefined: 반환하지 않음
    return typeof value === 'number' ? undefined : value;
}

// 객체 -> JSON 형식의 문자열 + replacer + prettify
const strFilteredObj = JSON.stringify(obj, filter, 2);
console.log(typeof strFilteredObj, strFilteredObj);
/*
string {
	"name": "Lee",
	"gender": "male"
}
*/
```



### 2.2. JSON.parse

JSON.parse 메소드는 JSON 데이터를 가진 문자열을 객체로 변환한다.

>  서버로부터 브라우저로 전송된 JSON 데이터는 문자열이다. 이 문자열을 객체로서 사용하려면 객체화하여야 하는데 이를 역직렬화(Deserializing)이라 한다. 역직렬화를 위해 내장 객체 JSON의 static 메소드인 `JSON.parse`를 사용한다.

```javascript
const obj = { name: 'Kim', gender: 'male', age: 20 };

// 객체 -> JSON 형식의 문자열
const strObj = JSON.stringify(obj);
console.log(typeof strObj, strObj);
// string {"name":"Kim","gender":"male","age":20}

// JSON 형식의 문자열 -> 객체
const parseObj = JSON.parse(strObj);
console.log(typeof parseObj, parseObj); // object { name: 'Kim', gender: 'male' }


const arr = [1, 5, 'false'];

// 배열 객체 -> 문자열
const strArray = JSON.stringify(arr);
console.log(typeof strArray, strArray); // string [1,5,"false"]

// 문자열 -> 배열 객체
const parseArray = JSON.parse(strArray);
console.log(typeof parseArray, parseArray); // object [ 1, 5, 'false' ]

```

배열이 JSON 형식의 문자열로 변환되어 있는 경우 `JSON.parse`는 문자열을 배열 객체로 변환한다. **배열의 요소가 객체인 경우 배열의 요소까지 객체로 변환한다.**

```javascript
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'JavaScript', completed: false }
];

// 배열 -> JSON 형식의 문자열
const str = JSON.stringify(todos);
console.log(typeof str, str);

// JSON 형식의 문자열 -> 배열
const parsed = JSON.parse(str);
console.log(typeof parsed, parsed);

```



## 3. XMLHttpRequest

### 3.1. Ajax request

#### 3.1.1. XMLHttpRequest.open

#### 3.1.2. XMLHttpRequest.send

#### 3.1.3 XMLHttpRequest.setRequestHeader



### 3.2. Ajax response



## 4. Web Server

## 5. Ajax 예제

### 5.1. Load HTML

### 5.2 Load JSON

### 5.3 Load JSONP

