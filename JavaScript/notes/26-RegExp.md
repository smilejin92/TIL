# RegExp - 정규표현식

## 1. 정규표현식 (Regular Expression)

정규표현식은 **문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.**

예를 들어, 회원가입 화면에서 사용자로 부터 입력 받는 전화번화가 유효한지 체크할 필요가 있다. 이때 정규 표현식을 사용하면 간단히 처리할 수 있다.

```javascript
const tel = '0101234567팔';

// 정규 표현식 리터럴
const myRegExp = /^[0-9]+$/;

console.log(myRegExp.test(tel)); // false
```

정규표현식은 **주석이나 공백을 허용하지 않으며** 여러가지 기호를 혼합하여 사용하기 때문에 **가독성이 좋지 않다.**



## 2. 정규표현식 생성 방법

<img src="./images/regExp.png" style="zoom:50%;" />

| Flag | Meaning     | Description                               |
| :--: | :---------- | ----------------------------------------- |
|  i   | Ignore Case | 대소문자를 구별하지 않고 검색한다.        |
|  g   | Global      | 문자열 내의 모든 패턴을 검색한다.         |
|  m   | Multi Line  | 문자열의 행이 바뀌더라도 검색을 계속한다. |

플래그는 옵션이므로 선택적으로 사용한다. 플래그를 사용하지 않은 경우 문자열 내 검색 매칭 대상이 **1개 이상이라도 첫 번째 매칭한 대상만을 검색하고 종료한다.**



### **리터럴 표기법으로 생성**

```javascript
const targetStr = 'This is a pen.';

// 문자열 내에 'is' 패턴이 있는지 확인하기 위한 정규표현식 생성
// i - 대소문자를 구별하지 않고,
// g - 문자열 내의 모든 패턴을 검색
const regexr = /is/ig;

console.log(regexr.exec(targetStr)); // ['is', index: 2, input: 'This is a pen.']
```



### `RegExp` 생성자 함수로 생성

```javascript
const targetStr = 'This is a pen.';

// new RegExp('pattern', 'flag')
// 문재열 내에 'is' 패턴이 있는지 확인하기 위한 정규표현식 생성
// i - 대소문자를 구별하지 않고,
// g - 문자열 내의 모든 패턴을 검색
const regexr = new RegExp('is', 'ig')

console.log(regexr.exec(targetStr)); // ['is', index: 2, input: 'This is a pen.']
```



## 3. 패턴

패턴에는 검색하고 싶은 문자열을 지정한다. 이때 문자열의 따옴표는 생략한다. **따옴표를 포함하면 따옴표까지도 검색한다.** 또한 패턴은 특별한 의미를 가지는 **메타문자**(Metacharacter) 또는 **기호**로 표현할 수 있다.

| 메타문자 / 기호 | 뜻                         | 예제           | 예제 설명                                                    |
| --------------- | -------------------------- | -------------- | ------------------------------------------------------------ |
| `.`             | 임의의 문자 한 개          | `/.../g`       | 임의의 문자 3개를 반복하여 검색                              |
| `+`             | 앞선 패턴을 최소 한번 반복 | `/A+/g`        | 'A'가 한번 이상 반복되는 문자열을 반복 검색                  |
| `|`             | 또는                       | `/A+|B+/g`     | 'A' 또는 'B'가 한번 이상 반복되는 문자열을 반복 검색         |
| `[AB]`          | A 또는 B                   | `/[AB]+/g`     | 'A' 또는 'B'가 한번 이상 반복되는 문자열을 반복 검색         |
| `[A-Z]`         | A 부터 Z 까지              | `/[A-Za-z]+/g` | 'A' ~ 'Z' 또는 'a' ~ 'z'가 한번 이상 반복되는 문자열을 반복 검색 |
| `\d`            | 모든 숫자                  | `/[\d]+/g`     | '0' ~ '9'가 한번 이상 반복되는 문자열을 반복 검색            |
| `\D`            | 숫자가 아닌                | `/[\D]+/g`     | '0' ~ '9'가 아닌 문자가 한번 이상 반복되는 문자열을 반복 검색 |
| `\w`            | 알파벳과 숫자              | `/[\w,]+/g`    | 알파벳과 숫자 또는 ','가 한번 이상 반복되는 문자열을 반복 검색 |
| `\W`            | 알파벳과 숫자가 아닌       | `/[\W]+/g`     | 알파벳과 숫자가 아닌 문자가 한번 이상 반복되는 문자열을 반복 검색 |
| `^`             | 문자열의 처음              | `/^http/`      | 'http'로 시작하는지 검사                                     |
| `$`             | 문자열의 끝                | `/html$/`      | 'html'로 끝나는지 검사                                       |
| `\s`            | 여러 가지 공백 문자        | `/^[\s]+/`     | 한개 이상의 공백으로 시작하는지 검사                         |
| `{4,10}`        | 문자열의 자리수            | `/{4,10}/`     | 문자열이 4 ~ 10자리인지 검사                                 |
| `[^]`           | 부정                       | `/[^a-z]/`     | 알파벳 소문자로 시작하지 않는 모든 문자                      |



## 4. 자주 사용하는 정규표현식

**특정 단어로 시작하는지 검사**

```javascript
const url = 'http://example.com';

// 'http'로 시작하는지 검사
// ^ : 문자열의 처음을 의미한다.
const regexr = /^http/;

console.log(regexr.test(url)); // true
```



**특정 단어로 끝나는지 검사**

```javascript
const fileName = 'index.html';

// 'html'로 끝나는지 검사
// $: 문자열의 끝을 의미한다.
const regexr = /html$/;

console.log(regexr.test(fileName)); // true
```



**숫자인지 검사**

```javascript
const targetStr = '12345';

// 모두 숫자인지 검사
const regexr = /^\d+$/; // 시작(^)과 끝($) 사이에 숫자 반복(\d+)

console.log(regexr.test(targetStr)); // true
```



**아이디로 사용 가능한지 검사 (영문자, 숫자만 허용 4~10 자리)**

```javascript
const id = 'abc123';

// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~ 10자리인지 검사
const regexr = /^[A-Za-z0-9]{4,10}$/;

console.log(regexr.test(id)); // true
```



**메일 주소 형식에 맞는지 검사**

```javascript
const email = 'smilejin92@gmail.com';

const regexr = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/;

console.log(regexr.test(email)); // true
```



**핸드폰 번호 형식에 맞는지 검사**

```javascript
const cell = '010-1234-5678';

const regexr = /^\d{3}-\d{4}-\d{4}$/;

console.log(regexr.test(cell)); // true
```



**특수 문자 포함 여부를 검사**

```javascript
const targetStr = 'abc#123';

// A-Z, a-z, 0-9 이외의 문자가 있는지 검사
let regexr = /[^A-Za-z0-9]/gi;

console.log(regexr.test(targetStr)); // true
```



## 5. 정규 표현식 관련 메소드

### 5.1 `RegExp.prototype` 메소드

**`RegExp.prototype.exec`** 

```javascript
// 문자열을 검색하여 매칭 결과를 반환한다. 반환값은 배열 또는 null이다.
const target = 'Is this all there is?';
const regExp = /is/ig;

// exec 메소드는 g 플래그를 지정하여도 첫번째 매칭 결과만을 반환한다.
const res = regExp.exec(target);
console.log(res); // ['Is', index: 0, input: 'Is this all there is?']
```



**`RegExp.prototype.test`**

```javascript
// 문자열을 검색하여 매칭 결과를 반환한다. 반환 값은 true 또는 false이다.
const target = 'Is this all there is?';
const regExp = /is/;

const res = regExp.test(target);
console.log(res); // true
```



### 5.2 `String.prototype` 메소드

**`String.prototype.match`**

```javascript
// 문자열을 검색하여 매칭 결과를 반환한다. 반환값은 배열 또는 null이다.
const targetStr = 'This is a pen.';
const regexr = /is/ig;

console.log(targetStr.match(regexr)); // [ 'is', 'is' ]
```



**`String.prototype.replace`**

```javascript
// 검색된 문자열을 원하는 문자열로 교체한다.
const targetStr = 'This is a pen.';
const regexr = /is/ig;

console.log(targetStr.replace(regexr, 'IS')); // ThIS IS a pen.
```



**`String.prototype.search`**

```javascript
// 검색된 문자열의 첫번째 인덱스를 반환한다.
const targetStr = 'This is a pen.';
const regexr = /is/ig;

console.log(targetStr.replace(regexr)); // 2
```



**`String.prototype.split`**

```javascript
// 검색된 문자열을 제외한 문자열을 반환한다
const targetStr = 'This is a pen.';
const regexr = /is/ig;

console.log(targetStr.split(regexr)); // ['Th', ' ', ' a pen.']
```

