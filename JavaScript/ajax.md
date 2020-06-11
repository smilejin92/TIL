# Ajax

## 1. Ajax란?

* Ajax는 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹 페이지를 동적으로 갱신하는 프로그래밍 방식이다.
* Ajax는 Web API인 XMLHttpRequest 객체를 기반으로 동작한다.
* Ajax 이전의 웹 페이지는 html 태그로 시작하여 html 태그로 끝나는 완전한 HTML 문서를 서버로부터 전송 받아 웹 페이지 전체를 처음부터 다시 렌더링하는 방식으로 동작했다.
* Ajax 이전의 클라이언트 <-> 서버 통신의 단점은 아래와 같다.
  * 변경이 필요 없는 영역까지 포함된 완전한 HTML 문서를 다시 요청하기 때문에 불필요한 데이터 통신이 발생한다.
  * 변경이 필요 없는 부분까지 다시 렌더링한다.
  * 클라이언트 <-> 서버 통신이 동기적으로 수행되기 때문에 응답을 받기 전까지 다음 태스크는 블로킹된다.
* Ajax는 위 세 개의 단점을 모두 보완한다.

&nbsp;  

Ajax(Asynchronous JavaScript and XML)란 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹 페이지를 동적으로 갱신하는 프로그래밍 방식을 말한다. Ajax는 Web API인 XMLHttpRequest 객체를 기반으로 동작한다. XMLHttpRequest는 HTTP 비동기 통신을 위한 메소드와 프로퍼티를 제공한다.

&nbsp;  

> 1999년 마이크로소프트가 개발한 XMLHttpRequest는 그다지 큰 주목을 받지 못하다가 2005년 구글이 발표한 구글 맵스를 통해 웹 애플리케이션 개발 프로그래밍 언어로서 자바스크립트의 가능성을 확인하는 계기를 마련했다. 웹 브라우저에서 자바스크립트와 Ajax를 기반으로 동작하는 구글 맵스가 데스트톱 애플리케이션과 비교해 손색이 없을 정도의 퍼포먼스와 부드러운 화면 전환 효과를 보여준 것이다.

&nbsp;  

이전의 웹 페이지는 html 태그로 시작해서 html 태그로 끝나는 완전한 HTML을 서버로부터 전송 받아 웹페이지 전체를 처음부터 다시 렌더링하는 방식으로 동작했다. 따라서 화면이 전환되면 서버로부터 새로운 HTML을 전송 받아 웹페이지 전체를 처음부터 다시 렌더링하였다.

<img src="https://user-images.githubusercontent.com/32444914/84358726-8638c180-ac02-11ea-80d8-14c7455da6d7.png" width="50%" />

이러한 전통적인 방식은 아래와 같은 단점이 있다.

1. 변경이 필요 없는 부분까지 포함된 완전한 HTML을 서버로부터 매번 다시 전송 받기 때문에 불필요한 데이터 통신이 발생한다.
2. 변경이 필요 없는 부분까지 처음부터 다시 렌더링한다. 이로 인해 화면 전환이 일어나면 화면이 순간적으로 깜박이는 현상이 발생한다.
3. 클라이언트와 서버와의 통신이 동기적으로 수행되기 때문에 서버로부터 응답이 있을 때까지 다음 처리는 블로킹된다.

&nbsp;  

Ajax의 등장은 이전의 전통적인 패러다임을 획기적으로 전환했다. 즉, 서버로부터 웹페이지의 변경에 필요한 데이터만을 비동기 방식으로 전송 받아 웹페이지의 변경이 필요 없는 부분은 다시 렌더링하지 않고, 변경이 필요한 부분만 한정적으로 렌더링하는 방식이 가능해진 것이다. 이를 통해 브라우저에서도 테스크톱 애플리케이션과 유사한 빠른 퍼포먼스와 부드러운 화면 전환이 가능하게 되었다.

<img src="https://user-images.githubusercontent.com/32444914/84359666-ed0aaa80-ac03-11ea-8362-49bd4e3b98d3.png" width="50%" />

Ajax는 전통적인 웹 페이지 방식과 비교했을 때 아래와 같은 장점이 있다.

1. 변경이 필요한 부분만을 갱신하기 위한 데이터 만을 전송 받기 때문에 불필요한 데이터 통신이 발생하지 않는다.
2. 변경이 필요 없는 부분은 다시 렌더링하지 않는다. 따라서 화면이 순간적으로 깜박이는 현상이 발생하지 않는다.
3. 클라이언트와 서버와의 통신이 비동기 방식으로 동작하기 때문에 서버에게 요청을 보낸 이후 블로킹이 발생하지 않는다.

&nbsp;  

## 2. JSON

* JSON은 클라이언트와 서버간의 HTTP 통신을 위한 **텍스트 데이터 포맷**이다.
* JSON은 자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트다.
* JSON의 키는 반드시 큰따옴표로 묶어야 한다. 값은 객체 리터럴과 같은 표기법을 그대로 사용할 수 있지만, 문자열은 반드시 큰따옴표로 묶어야 한다.
* `JSON.stringify` 메소드는 객체를 JSON 포맷의 문자열로 변환(직렬화)한다.
* `JSON.parse` 메소드는 JSON 포맷의 문자열을 객체로 변환(역직렬화)한다.
* 배열의 요소가 객체여도 직렬화 / 역직렬화 할 수 있다. 단, 값이 함수이거나 메소드 축약 표현으로 정의한 프로퍼티는 직렬화할 수 없다.

&nbsp;  

JSON(JavaScript Object Notation)은 클라이언트와 서버간의 HTTP 통신을 위한 **텍스트 데이터 포맷**이다. 자바스크립트에 종속되지 않는 언어 독립형 데이터 포맷으로 대부분의 프로그래밍 언어에서 사용할 수 있다.

&nbsp;

### 2.1. JSON 표기 방식

JSON은 자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 **순수한 텍스트다.**

```json
{
  "name": "Kim",
  "age": 20,
  "alive": true,
  "hobby": ["traveling", "tennis"]
}
```

JSON의 키는 반드시 큰따옴표로 묶어야 한다. 값은 객체 리터럴과 같은 표기법을 그대로 사용할 수 있다. 하지만 문자열은 반드시 큰따옴표로 묶어야 한다.

&nbsp;  

### 2.2. JSON.stringify

`JSON.stringify` 메소드는 객체를 JSON 포맷의 문자열로 변환한다. 클라이언트가 서버로 객체를 전송하려면 객체를 문자열로 변환해야하는데 이를 직렬화(serializing)이라 한다.

```javascript
const obj = {
  name: 'Kim',
  age: 20,
  alive: true,
  hobby: ['traveling', 'tennis']
};

// 1. 객체 -> JSON
const json = JSON.stringify(obj);
console.log(typeof json); // string
console.log(json);
// {"name":"Kim","age":20,"alive":true,"hobby":["traveling","tennis"]}

// 2. 객체 -> JSON + prettify
const prettyJson = JSON.stringify(obj, null, 2);
console.log(prettyJson);
/*
{
  "name": "Lee",
  "age": 20,
  "alive": true,
  "hobby": [
    "traveling",
    "tennis"
  ]
}
*/

// 3. 객체 -> JSON + replacer + prettify
const prettyJsonWithoutNumber = JSON.stringify(obj, filter, 2);
console.log(prettyJsonWithoutNumber);
/*
{
  "name": "Lee",
  "alive": true,
  "hobby": [
    "traveling",
    "tennis"
  ]
}
*/

// replacer
// 값의 타입이 Number이면 필터링되어 반환되지 않는다.
function filter(key, value) {
  // undefined: 반환되지 않음
  return typeof value === 'number' ? undefined : value;
}
```

&nbsp;  

`JSON.stringify` 메소드는 객체 뿐만이 아니라 배열도 JSON 포맷의 문자열로 변환한다.

```javascript
const todos = [
  { id: 1, content: 'HTML', completed: false },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'JavaScript', completed: false }
];

// 배열 -> JSON + prettify
const json = JSON.stringify(todos, null, 2);
console.log(json);
/*
[
  {
    "id": 1,
    "content": "HTML",
    "completed": false
  },
  {
    "id": 2,
    "content": "CSS",
    "completed": true
  },
  {
    "id": 3,
    "content": "Javascript",
    "completed": false
  }
]
*/
```



&nbsp;  

### 2.3. JSON.parse

`JSON.parse` 메소드는 **JSON 포맷의 문자열을 객체로 변환**한다. 서버로부터 클라이언트에게 전송된 JSON 데이터는 문자열이다. 이 문자열을 객체로서 사용하려면 JSON 포맷의 문자열을 객체화해야 한다. 이를 역직렬화(deserializing)이라 한다.

```javascript
const obj = {
  name: 'Kim',
  age: 20,
  alive: true,
  hobby: ['traveling', 'tennis']
};

// 객체 -> JSON
const json = JSON.stringify(obj);

// JSON -> 객체
const parsed = JSON.parse(json);
console.log(typeof parsed); // object
console.log(parsed);
// {name: "Kim", age: 20, alive: true, hobby: ["traveling", "tennis"]}
```

&nbsp;  

배열이 JSON 포맷의 문자열로 변환되어 있는 경우 `JSON.parse`는 문자열을 배열 객체로 변환한다. 배열의 요소가 객체인 경우 배열의 요소까지 객체로 변환한다.

```javascript
const todos = [
	{ id: 1, content: 'HTML', completed: false },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'JavaScript', completed: false }
];

// 배열 -> JSON
const json = JSON.stringify(todos);

// JSON -> 배열
const parsed = JSON.parse(json);
console.log(parsed);
/*
[
  { id: 1, content: 'HTML', completed: false },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'Javascript', completed: false }
]
*/
```

&nbsp;  

## 3. XMLHttpRequest

* 브라우저는 주소창이나 HTML의 `form` 태그 또는 `a` 태그를 통해 HTTP 요청 전송 기능을 기본 제공한다.
* 자바스크립트를 사용하여 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용한다.
* Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 HTTP 응답 수신을 위한 다양한 메소드와 프로퍼티를 제공한다.
* HTTP 요청을 생성하여 서버에 전송하고 응답을 수신하는 순서는 아래와 같다.
  * XMLHttpRequest 객체 생성
  * 요청 초기화 (`XMLHttpRequest.prototype.open`)
  * 요청 헤더 설정 (`XMLHttpRequest.prototype.setRequestHeader`)
  * 요청 전송 (`XMLHttpRequest.prototype.send`)
  * 응답 수신 (`XMLHttpRequest.prototype.onload / onreadystatechange`)
* HTTP 요청 메소드는 클라이언트가 <strong>서버에게 요청의 종류와 목적(리소스에 대한 행위)</strong>을 알리는 방법이다. 주로 5가지 메소드(GET, POST, PUT, PATCH, DELETE 등)를 사용하여 CRUD를 구현한다.
* GET 요청 메소드의 경우, 데이터를 URL의 일부분인 쿼리 문자열(query string)로 서버에 전송한다.
* POST 요청 메소드의 경우, 데이터(페이로드)를 요청 몸체(request body)에 담아 전송한다.

&nbsp;  

브라우저는 주소창이나 HTML의 `form` 태그 또는 `a` 태그를 통해 HTTP 요청 전송 기능을 기본 제공한다. 자바스크립트를 사용하여 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용한다. Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 HTTP 응답 수신을 위한 다양한 메소드와 프로퍼티를 제공한다.

&nbsp;  

### 3.1. XMLHttpRequest 객체 생성

XMLHttpRequest 객체는 `XMLHttpRequest` 생성자 함수를 호출하여 생성한다.

```javascript
// XMLHttpRequest 객체의 생성
const xhr = new XMLHttpRequest();
```

&nbsp;  

XMLHttpRequest 객체는 다양한 프로퍼티와 메소드를 제공한다. 대표적인 프로퍼티와 메소드는 아래와 같다.

| 프로토타입 프로퍼티 | 설명                                                         |
| ------------------- | ------------------------------------------------------------ |
| **readyState**      | * 요청의 현재 상태를 나타내는 정수<br />* 0: UNSENT<br />* 1: OPENED<br />* 2: HEADERS_RECEIVED<br />* 3: LOADING<br />* 4: DONE |
| **status**          | 요청에 대한 응답 상태(HTTP 상태 코드)를 나타내는 정수 (ex. 200) |
| **statusText**      | 요청에 대한 응답 메시지를 나타내는 문자열 (ex. "OK")         |
| **responseType**    | 응답 타입 (ex. document, json, text, blob, arraybuffer)      |
| **response**        | * 요청에 대한 응답 몸체(response body)<br />* responseType에 따라 타입이 다르다. |
| responseText        | 서버가 전송한 요청에 대한 응답 문자열                        |

&nbsp;  

| 이벤트 핸들러 프로퍼티 | 설명                                               |
| ---------------------- | -------------------------------------------------- |
| **onreadystatechange** | readyState 프로퍼티 값이 변경된 경우               |
| onloadstart            | 요청에 대한 응답을 받기 시작한 경우                |
| onprogress             | 요청에 대한 응답을 받는 동안 주기적으로 발생       |
| onabort                | abort 메소드에 의해 요청이 중단되었을 경우         |
| **onerror**            | 요청에 에러가 발생한 경우                          |
| **onload**             | 요청이 성공적으로 완료한 경우                      |
| ontimeout              | 요청 시간이 초과한 경우                            |
| onloadend              | 요청이 완료한 경우. 요청이 성공 또는 실패하면 발생 |

&nbsp;  

| 메소드               | 설명                                       |
| -------------------- | ------------------------------------------ |
| **open**             | HTTP 요청 초기화                           |
| **send**             | HTTP 요청 전송                             |
| **abort**            | 이미 전송된 HTTP 요청 중단                 |
| **setRequestHeader** | HTTP 요청 헤더의 값을 설정                 |
| getResponseHeader    | 지정한 HTTP 요청 헤더의 값을 문자열로 반환 |

&nbsp;  

| 정적 프로퍼티    | 값   | 설명                                  |
| ---------------- | ---- | ------------------------------------- |
| UNSENT           | 0    | open 메소드 호출 이전                 |
| OPENED           | 1    | open 메소드 호출 이후                 |
| HEADERS_RECEIVED | 2    | send 메소드 호출 이후                 |
| LOADING          | 3    | 서버 응답 중(응답 데이터 미완성 상태) |
| **DONE**         | 4    | 서버 응답 완료                        |

&nbsp;  

### 3.2. HTTP 요청 전송

HTTP 요청을 전송하는 경우, 아래의 순서를 따른다.

1. `XMLHttpRequest.prototype.open` 메소드로 HTTP 요청 초기화
2. 필요에 따라 `XMLHttpReqeust.prototype.setRequestHeader` 메소드로 HTTP 요청의 레더 값 설정
3. `XMLHttpRequest.prototype.send` 메소드로 HTTP 요청 전송

&nbsp;  

```javascript
// 0. XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// 1. HTTP 요청 초기화
xhr.open('GET', '/users');

// 2. HTTP 요청 헤더 설정
// 클라이언트가 서버로 전송할 데이터의 MIME-type 지정: JSON으로 보내겠다.
xhr.setRequestHeader('Content-Type', 'application/json');
// 서버가 응답할 데이터의 MIME-type을 지정: JSON으로 받겠다.
xhr.setRequestHeader('Accept', 'application/json');

// 3. HTTP 요청 전송
xhr.send();
```

&nbsp;  

#### 3.2.1. XMLHttpRequest.prototype.open

`open` 메소드는 **서버에 전송할 HTTP 요청을 초기화**한다.

```javascript
xhr.open(method, url[, async])
```

| 매개변수 | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| method   | **HTTP 요청 메소드** (ex. "GET", "POST", "PUT", "PATCH", "DELETE" 등) |
| url      | HTTP 요청을 전송할 URL                                       |
| async    | (옵션) 비동기 요청 여부. 기본값은 true이며 비동기 방식으로 동작한다. |

&nbsp;  

HTTP 요청 메소드는 클라이언트가 <strong>서버에게 요청의 종류와 목적(리소스에 대한 행위)</strong>을 알리는 방법이다. 주로 5가지 메소드(GET, POST, PUT, PATCH, DELETE 등)를 사용하여 CRUD를 구현한다.

| HTTP 요청 메소드 | 종류           | 목적                  | 페이로드 |
| ---------------- | -------------- | --------------------- | -------- |
| GET              | index/retrieve | 모든/특정 리소스 취득 | X        |
| POST             | create         | 리소스 생성           | O        |
| PUT              | replace        | 리소스의 전체 교체    | O        |
| PATCH            | modify         | 리소스의 일부 수정    | O        |
| DELETE           | delete         | 모든/특정 리소스 삭제 | X        |

&nbsp;  

#### 3.2.2. XMLHttpRequest.prototype.send

`send` 메소드는 `open` 메소드로 초기화된 **HTTP 요청을 서버에 전송**한다. 기본적으로 서버에 전송하는 데이터는 GET, POST 요청 메소드에 따라 그 전송 방식에 차이가 있다.

* GET 요청 메소드의 경우, 데이터를 URL의 일부분인 쿼리 문자열(query string)로 서버에 전송한다.
* POST 요청 메소드의 경우, 데이터(페이로드)를 요청 몸체(request body)에 담아 전송한다.

<img src="https://user-images.githubusercontent.com/32444914/84373155-23055a00-ac17-11ea-9920-39b5b8f5c6f0.png" width="60%" />

`send` 메소드에는 request body에 담아 전송할 페이로드를 인수로 전달할 수 있다. **페이로드가 객체인 경우, 반드시 `JSON.stringify` 메소드를 사용하여 직렬화한 후 전댈해야 한다.**

```javascript
xhr.send(JSON.stringify({ id: 1, content:'HTML', completed: false }));
```

**만약 HTTP 요청 메소드가 GET인 경우, `send` 메소드에 페이로드로 전달한 인수는 무시되고 요청 몸체는 null로 설정된다.**

&nbsp;  

#### 3.2.3. XMLHttpRequest.prototype.setRequestHeader

`setRequestHeader` 메소드는 HTTP 요청의 헤더 값을 설정한다. `setRequestHeader` 메소드는 반드시 `open` 메소드 호출 이후에 호출해야 한다. 자주 사용하는 HTTP 요청 헤더인 Content-Type과 Accept에 대해 살펴보자.

Content-Type은 요청 몸체(request body)에 담아 전송할 데이터의 [MIME-type](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)의 정보를 표현한다. 자주 사용되는 MIME-type은 아래와 같다.

| MIME-type   | 서브타입                                           |
| ----------- | -------------------------------------------------- |
| text        | text/plain, text/html, text/css, text/javascript   |
| application | application/json, application/x-www-form-urlencode |
| multipart   | multipart/formed-data                              |

&nbsp;  

다음은 요청 몸체에 담아 서버로 전송할 페이로드의 MIME-Type을 지정하는 예이다.

```javascript
// HTTP 요청 헤더 설정
// 클라이언트가 서버로 전송할 데이터의 MIME-type 지정: JSON으로 보내겠다.
xhr.setRequestHeader('Content-Type', 'application/json');
// 서버가 응답할 데이터의 MIME-type을 지정: JSON으로 받겠다.
xhr.setRequestHeader('Accept', 'application/json');
```

만약 Accept 헤더를 설정하지 않으면, `send` 메소드가 호출될 때 Accept 헤더가 `*/*`으로 전송된다.

&nbsp;  

### 3.3. HTTP 응답 처리

서버가 전송한 응답을 처리하려면 XMLHttpRequest 객체가 발생시키는 이벤트를 캐치하여야 한다. XMLHttpRequest 객체는 이벤트 핸들러 프로퍼티를 가진다. 이 이벤트 핸들러 프로퍼티 중 `readyState` 프로퍼티 값이 변경된 경우 발생하는 `readystatechange` 이벤트를 캐치하여 아래와 같이 HTTP 응답을 처리할 수 있다.

```javascript
// 0. XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// 1. HTTP 요청 초기화
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

// 2. HTTP 요청 전송
xhr.send();

// 3. HTTP 응답 처리
// readystatechange 이벤트는 요청의 현재 상태를 나타내는 readyState 프로퍼티가
// 변경될 때마다 발생
xhr.onreadystatechange = () => {
  // XMLHttpRequest.DONE === 4 (서버 응답 완료)
  if(xhr.readyState !== XMLHttpRequest.DONE) return;
  
  // status는 response 상태 코드를 반환
  // 200 === 정상 응답
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.response));
    // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```

&nbsp;  

`readystatechange` 이벤트 대신 `load` 이벤트를 캐치해도 좋다. `load` 이벤트는 요청이 성공적으로 완료된 경우 발생한다. 따라서 `load` 이벤트를 캐치하는 경우, `readyState`가 4(`XMLHttpRequest.DONE`)인지 확인할 필요가 없다.

```javascript
// 0. XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// 1. HTTP 요청 초기화
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

// 2. HTTP 요청 전송
xhr.send();

// 3. HTTP 응답 처리
// load 이벤트는 요청이 성공적으로 완료된 경우 발생한다.
xhr.onload = () => {
  // status는 response 상태 코드를 반환
  // 200 === 정상 응답
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.response));
    // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```

&nbsp;  

## 출처

* [poiemaweb.com - Ajax](https://poiemaweb.com/fastcampus/ajax)

