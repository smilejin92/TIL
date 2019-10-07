# Data Type & Operator

### ch.5 데이터 타입

#### 데이터 타입에 의한 메모리 공간의 확보 / 값의 해석

데이터 타입(Data Type)은 값의 종류를 말한다. 자바스크립트의 모든 값은 데이터 타입을 갖는다. 데이터 타입이 필요한 이유는 아래와 같다.

- 값을 저장할 때 확보해야 하는 **메모리 공간의 크기**를 결정하기 위해
- 값을 참조할 때 한번에 읽어 들여야 할 **메모리 공간의 크기**를 결정하기 위해
- 메모리에서 읽어 들인 **2진수를 어떻게 해석**할 지를 결정하기 위해



#### 값 (value)

* **더이상 평가할 수 없는 하나의 표현식**

* 메모리에 들어가는 대상

* 표현식 - 값을 생성하는 문(statement), 평가되어 값을 생성

* 타입을 가지고 있다

  ``` javascript
  // 10 + 20은 10, 20의 값과 +의 연산자로 구성된 표현식이다.
  // 이 표현식은 JS 엔진에 평가되어 30이라는 값을 만든다.
  // 생성된 값 30은 더 이상 평가할 수 없다.
  10 + 20
  ```

* 변수(Variable)는 **하나 값**을 저장할 수 있는 메모리 공간에 붙인 이름 또는 **메모리 공간 자체**를 말한다. 따라서 값은 변수에 할당할 수 있다.

  ``` javascript
  // 변수에는 표현식 10 + 20의 평가되어 생성한 값 30이 할당된다.
  var sum = 10 + 20;
  ```



#### 값의 생성

* Literal

  * 소스 코드 안에서 직접 만들어 낸 고정된 값 자체

  * **리터럴 표기법은 사람이 이해할 수 있는 표기법으로 값의 생성을 자바스크립트 엔진에게 명령하는 것이다.**

    ``` javascript
    // 리터럴 표기법으로 숫자 리터럴 3을 기술하였다.
    // 자바스크립트 엔진은 런타임에 숫자 리터럴 3을 해석하여 숫자 타입의 값 3을 생성한다.
    3
    ```

  * 리터럴 표기법을 사용하면 아래와 같이 자바스크립트에서 사용할 수 있는 다양한 타입의 값(숫자, 문자열, 불리언, null, undefined, 객체, 배열, 함수, 정규 표현식 등)을 생성할 수 있다.

    ``` javascript
    // 정수 리터럴
    100
    
    // 부동 소숫점 리터럴
    10.5
    
    // 2진수 리터럴(0b로 시작)
    0b01000001
    
    // 8진수 리터럴(ES6에서 도입. 0o로 시작)
    0o101
    
    // 16진수 리터럴(ES6에서 도입. 0x로 시작)
    0x41
    
    // 문자열 리터럴
    'Hello'
    "World"
    
    // 불리언 리터럴
    true
    false
    
    // null 리터럴
    null
    
    // undefined 리터럴
    undefined
    
    // 객체 리터럴
    { name: 'Lee', gender: 'male' }
    
    // 배열 리터럴
    [ 1, 2, 3 ]
    
    // 함수 리터럴
    function() {}
  
    // 정규표현식 리터럴
    /ab+c/
    ```
  
  * 리터럴은 그 자체로 값이 될 수 있지만 **값이 리터럴인 것은 아니다**. 리터럴 100은 자바스크립트 엔진에 의해 평가되어 숫자값 100이 되지만 숫자값 100이 리터럴은 아니다.



#### 표현식

표현식(**expression**)은 리터럴, 식별자(변수나 함수 등의 이름), 연산자, 함수 호출 등의 조합을 말한다. 표현식은 평가(**evaluation** - 표현식을 해석하여 하나의 값을 만드는 과정)되어 하나의 값을 만든다.

즉, **표현식은 하나의 값으로 평가될 수 있는 문(statement)이다** (리터럴 <= 표현식). 또한, **변수에 할당할 수 있는 문은 표현식이다.**

<img src="./images/expression.png" style="zoom:50%;" />



### 데이터 타입의 분류 - primitive type

원시 타입(primitive type) - 재할당 시 이전에 할당된 메모리 셀의 데이터를 지우지/수정하지 않고 (immutable) 다른 공간에 재할당. 지우고 다시 쓸 수 없음.



#### **숫자(number) 타입: 숫자 (정수, 실수)**

- 자바스크립트에서는 모든 수를 실수(float)로 저장한다 (배정밀도 64비트 부동소수점).

``` javascript
// 모두 숫자 타입
var integer = 10;
var double = 10.12;
var negative = -20;
var binary = 0b100001;
var octal = 0o101;
var hex = 0x41;
```

* 모든 수를 실수로 처리하기 때문에, **정수로 표시되는 수 끼리 나누더라도 실수가 나올 수 있다.**

``` javascript
// 숫자 타입의 3가지 특별한 값
console.log(10 / 0);       // Infinity
console.log(10 / -0);      // -Infinity
console.log(1 * 'String'); // NaN
```

- Infinity : 양의 무한대
- -Infinity : 음의 무한대
- NaN : 산술 연산 불가 (not-a-number)



---

#### **문자열(string)**

* 텍스트 데이터를 나타내는데 사용
* 0개 이상의 16비트 유니코드 문자들의 집합
* **작은 따옴표** (' '), 큰 따옴표 (" "), 백틱 (``) 안에 텍스트를 넣어 생성

``` javascript
// 문자열 타입
var string;
string = "문자열"; // 큰 따옴표
string = '문자열'; // 작은 따옴표
string = `문자열`; // 백틱 (ES6)

string = "큰 따옴표로 감싼 문자열 내의 '작은 따옴표'는 문자열로 인식된다.";
string = '작은 따옴표로 감싼 문자열 내의 "큰 따옴표"는 문자열로 인식된다.';
```



**템플릿 리터럴** - 백틱 (``) 문자를 사용

``` javascript
const template = `템플릿 리터럴은 '작은따옴표(single quotes)'와 "큰따옴표(double quotes)"를 혼용할 수 있다.`;

console.log(template);
// 템플릿 리터럴은 '작은따옴표(single quotes)'과 "큰따옴표(double quotes)"를 혼용할 수 있다.
```

ES6 템플릿 리터럴은 일반적인 문자열과 달리 여러 줄에 걸쳐 문자열을 작성할 수 있으며 템플릿 리터럴 내의 모든 공백은 있는 그대로 적용된다. (`\n` not required)



**Escape Sequence** - 보이는 문자 그대로가 아닌 다른 의미로 해석되는 문자

| Escape Sequence | 의미                              |
| --------------- | --------------------------------- |
| \0              | Null                              |
| \b              | 백스페이스                        |
| \f              | 새로운 페이지                     |
| \n              | 개행 (LF, Line Feed)              |
| \r              | 캐리지 리턴 (CR, Carriage Return) |
| \t              | 탭 (수평)                         |
| \v              | 탭 (수직)                         |
| \\'             | 작은 따옴표                       |
| \\"             | 큰 따옴표                         |
| \\              | 백슬래시                          |



```javascript
// Escape sequence example
var template = '<ul class="nav-items">\n';
template += '\t<li><a href="#home">Home</a></li>\n';
template += '\t<li><a href="#about">About</a></li>\n';
template += '</ul>';

console.log(template);

/* output
<ul class="nav-items">
  <li><a href="#home">Home</a></li>
  <li><a href="#about">About</a></li>
</ul>
*/
```

템플릿 리터럴을 사용하면 escape sequence를 쓰는 시간을 줄일 수 있다 (ES6)



**String Concatenation** - (+) 연산자로 문자열 연결

``` javascript
var first = 'Jinhyun';
var last = 'Kim';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');

// My name is Jinhyun Kim.
```



**String Interpolation** - 템플릿 리터럴을 사용해 (+) 연산자 없이 문자열을 연결/삽입하는 기능

``` javascript
var first = 'Jinhyun';
var last = 'Kim';

// ES6: String Interpolation
console.log(`My name is ${first} ${last}.`);

// My name is Jinhyun Kim.
```

문자열 인터폴레이션은 `${ expression }`으로 표현식을 감싼다. 이때 표현식의 평가 결과는 **문자열로** **강제 타입 변환**된다.

``` javascript
console.log(`1 + 1 = ${1 + 1}`); // 1 + 1 = 2
```



---

#### **불리언(boolean) 타입**: 논리적 참(true)과 거짓(false)

* 참과 거짓으로 구분되는 조건에 의해 프로그램의 흐름을 제어하는 조건문에서 자주 사용

```javascript
var foo = true;
console.log(foo); // true

foo = false;
console.log(foo); // false
```



---

#### **undefined 타입**

* 선언은 되었지만 값을 할당하지 않은 변수에 암묵적으로 할당되는 값

* 변수를 참조했을 때 undefined가 반환된다면 참조한 변수가 선언 이후 값이 할당된 적인 없는 변수라는 것을 간파할 수 있다.

```javascript
var foo;
console.log(foo); // undefined
```



---

#### **null 타입**

* 값이 없다는 것을 **의도적으로 명시**할 때 사용하는 값
* 변수가 이전에 참조하던 값을 더이상 참조하지 않겠다는 의미로 사용
* 함수가 유효한 값을 반환할 수 없는 경우, 명시적으로 null을 반환하기도 함 (ex. `document.querySelector()`)



---

#### **Symbol 타입**

* ES6에서 새롭게 추가된 7번째 타입

* 변경 불가능한 원시 타입의 값
* 이름의 충돌 위험이 없는 object의 유일한 property key를 만들기 위해 사용
* Symbol() 함수를 호출하여 생성

``` javascript
// 심볼 값 생성
var key = Symbol('key');
console.log(typeof key); // symbol

// 객체 생성
var obj = {};

// 심볼 key를 이름의 충돌 위험이 없는 유일한 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); // value
```





---

### 데이터 타입의 분류 - object / reference type

* 객체, 함수, 배열 등



---

### 동적 타이핑 (dynamic typing)

**정적 타입 언어 (C, Java)는 변수의 타입을 변경할 수 없으며 변수에 선언한 타입에 맞는 값만을 할당할 수 있다.** 정적 타입 언어는 컴파일 시점에 타입 체크(선언한 데이터 타입에 맞는 값을 할당했는지 검사하는 처리)를 수행한다.

자바스크립트는 정적 타입 언어와는 다르게 **변수를 선언할 때 타입을 선언하지 않는다.** 다만 var, let, const 키워드를 사용해 변수를 선언할 뿐이다. 자바스크립트의 변수는 정적 타입 언어와 같이 미리 선언한 데이터 타입의 값만을 할당할 수 있는 것이 아니다. **어떠한 데이터 타입의 값이라도 자유롭게 할당할 수 있다.**

``` javascript
var foo;
console.log(typeof foo);  // undefined

foo = 3;
console.log(typeof foo);  // number

foo = 'Hello';
console.log(typeof foo);  // string

foo = true;
console.log(typeof foo);  // boolean

foo = null;
console.log(typeof foo);  // object

foo = Symbol(); // 심볼
console.log(typeof foo);  // symbol

foo = {}; // 객체
console.log(typeof foo);  // object

foo = []; // 배열
console.log(typeof foo);  // object

foo = function () {}; // 함수
console.log(typeof foo);  // function
```

**자바스크립트 변수는 선언이 아닌 할당에 의해 타입이 결정된다. 그리고 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다.**



#### 동적 타이핑의 취약점

* 데이터 타입을 추적하기 어려울 수 있다.
* 변수의 값은 언제든지 의도치 않게 변경될 수 있다.
*  변수가 저장하고 있는 값을 확인하기 전에는 값의 타입을 확신할 수 없다.
* 신뢰성(reliability)은 떨어진다.



#### 극복 방법

- 변수의 사용을 적극적으로 줄인다. 변수의 개수가 많으면 많을수록 오류가 발생할 확률은 높아진다.
- 전역 변수는 사용하지 않는다. 변수의 생명주기를 최대한 짧게 만든다.
- 변수보다는 상수를 사용해 값의 변경을 억제한다.
- 변수 이름은 변수의 존재 이유를 파악할 수 있도록 명명한다.



---

### ch. 6  연산자

#### 문 (statement)과 표현식

**문(statement)은 하나 이상의 표현식과 키워드의 조합으로 구성된 자바스크립트 엔진에게 내리는 명령**이다. 문의 집합으로 이루진 것이 바로 프로그램이며 문을 작성하고 순서에 맞게 나열하는 것이 프로그래밍이다.

* 선언문
* 표현식 (문) - 할당문
* 조건문
* 반복문

<img src="./images/statement.png" style="zoom:50%;" />

문은 구성되며 세미콜론(;)으로 끝나야하지만, 코드 블록 뒤에는 세미콜론을 붙이지 않는다.



#### 표현식인 문과 표현식이 아닌 문

표현식인 문은 **값으로 평가될 수 있는 문**이며, 표현식이 아닌 문은 **값으로 평가될 수 없는 문**을 말한다. 이 둘을 구별하기 위한 가장 간단한 방법은 각각을 **변수에 할당해 보는 것이다**.

```javascript
// 변수 선언문은 표현식이 아닌 문이다.
var x;

// 할당문은 그 자체가 표현식이지만 완전한 문이기도 하다. 즉, 할당문은 표현식인 문이다.
x = 100;
```



**완료 값 (Completion value)** - 표현식이 아닌 문은 언제나 `undefined`를 출력한다. 이를 **완료 값**이라 한다. 완료 값은 다른 값과 같이 변수에 할당할 수 없다.

![](./images/completion-value.png)

![](./images/completion-value2.png)

---

### 연산자

**연산자(Operator)**는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 **연산(operation) 등을 수행해 하나의 값을 만든다.** 이때 연산의 대상을 **피연산자 (Operand)라 한다.** 

![](./images/operation.png)

#### 1. 이항 산술 연산자

2개의 피연산자를 산술 연산하여 숫자 타입의 값을 만든다. 모든 이항 산술 연산자는 피연산자의 값을 변경하는 부수 효과 (Side effect)가 없다.

| 이항 산술 연산자 |  의미  | 부수 효과 |
| :--------------: | :----: | :-------: |
|        +         |  덧셈  |     X     |
|        -         |  뺄셈  |     X     |
|        *         |  곱셈  |     X     |
|        /         | 나눗셈 |     X     |
|        %         | 나머지 |     X     |





#### 2. 단항 산술 연산자

1개의 피연산자를 산술 연산하여 숫자 타입의 값을 만든다. 주의할 것은 이항 산술 연산자와는 달리 **증가/감소(++/--) 연산자는 피연산자의 값을 변경하는 부수 효과가 있다.** 다시 말해 증가/감소 연산을 하면 피연산자의 값이 바뀐다.

| 단항 산술 연산자 | 의미                                                 | 부수 효과 |
| :--------------: | ---------------------------------------------------- | :-------: |
|        ++        | 증가                                                 |     O     |
|        --        | 감소                                                 |     O     |
|        +         | 어떠한 효과도 없다. 음수를 양수로 반전하지도 않는다. |     X     |
|        -         | 양수를 음수로, 음수를 양수로 반전한 값을 반환한다    |     X     |



증가/감소(++/--) 연산자는 위치에 의미가 있다.

- **피연산자 앞에** 위치한 **전위 증가/감소** 연산자(**Prefix increment/decrement operator**)는 먼저 피연산자의 값을 증가/감소시킨 후, 다른 연산을 수행한다.

- **피연산자 뒤에** 위치한 **후위 증가/감소** 연산자(**Postfix increment/decrement operator**)는 먼저 다른 연산을 수행한 후, 피연산자의 값을 증가/감소시킨다.

  ``` javascript
  var x = 5, result;
  
  // 선할당 후증가 (Postfix increment operator)
  result = x++; // result에 x의 값을 할당한 후, x를 1 증가
  console.log(result, x); // 5 6
  
  // 선증가 후할당 (Prefix increment operator)
  result = ++x; // x의 값을 1 증가시킨 후, result에 할당
  console.log(result, x); // 7 7
  
  // 선할당 후감소 (Postfix decrement operator)
  result = x--; // result에 x의 값을 할당한 후, x를 1 감소
  console.log(result, x); // 7 6
  
  // 선감소 후할당 (Prefix decrement operator)
  result = --x; // x의 값을 1 감소시킨 후, result에 할당
  console.log(result, x); // 5 5
  ```



**(+)** 단항 연산자는 피연산자에 어떠한 효과도 없다. 음수를 양수로 반전하지도 않는다. 그런데 **숫자 타입이 아닌 피연산자에 사용하면 피연산자를 숫자 타입으로 변환하여 반환한다.** **이때 피연산자를 변경하는 것은 아니고,** 숫자 타입으로 변환한 값을 생성해서 반환한다. 따라서 부수 효과는 없다.

``` javascript
// 아무런 효과가 없다.
+10;    // -> 10
+(-10); // -> -10

// 문자열을 숫자로 타입 변환한다.
+'10'; // -> 10

// 불리언 값을 숫자로 타입 변환한다.
+true; // -> 1

// 불리언 값을 숫자로 타입 변환한다.
+false; // -> 0

// 문자열을 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
+'Hello'; // -> NaN

// 애초에 위와 같은 문법으로 코딩을 하지말자.
```



**(–)** 단항 연산자는 피연산자의 부호를 반전한 값을 반환한다. (+) 단항 연산자와 마찬가지로 **숫자 타입이 아닌 피연산자에 사용하면 피연산자를 숫자 타입으로 변환하여 반환한다.** **이때 피연산자를 변경하는 것은 아니고,** 부호를 반전한 값을 생성해서 반환한다. 따라서 부수 효과는 없다.

```javascript
// 부호를 반전한다.
-(-10); // -> 10

// 문자열을 숫자로 타입 변환한다.
-'10'; // -> -10

// 불리언 값을 숫자로 타입 변환한다.
-true; // -> -1

// 문자열을 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
-'Hello'; // -> NaN
```



#### 3. 문자열 연결 연산자

**(+)** **연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다.**

```javascript
// 문자열 연결 연산자
'1' + 2; // -> '12'
1 + '2'; // -> '12'
```



##### 암묵적 타입 변환 (Implicit coercion) - 강제 타입 변환 (Type coercion)

``` javascript
// true는 1로 타입 변환된다.
1 + true; // -> 2

// false는 0으로 타입 변환된다.
1 + false; // -> 1

// null는 0으로 타입 변환된다.
1 + null; // -> 1

// undefined는 숫자로 타입 변환되지 않는다.
+undefined;    // -> NaN
1 + undefined; // -> NaN
```

**(주의)** 개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 **암묵적으로 타입이 자동 변환되기도 한다.**



#### 4. 할당 연산자

**할당 연산자**는 우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당.

| 할당 연산자 | 사례   | 동일 표현 | 부수 효과 |
| :---------: | ------ | --------- | :-------: |
|      =      | x = 5  | x = 5     |     O     |
|     +=      | x += 5 | x = x + 5 |     O     |
|     -=      | x -= 5 | x = x - 5 |     O     |
|     *=      | x *= 5 | x = x * 5 |     O     |
|     /=      | x /= 5 | x = x / 5 |     O     |
|     %=      | x %= 5 | x = x % 5 |     O     |



#### 5. 비교 연산자

##### 동등 / 일치 비교 연산자

| 비교 연산자 | 의미        | 사례    | 설명                     | 부수 효과 |
| :---------: | ----------- | ------- | ------------------------ | :-------: |
|     ==      | 동등 비교   | x == y  | x와 y의 값이 같음        |     X     |
|     ===     | 일치 비교   | x === y | x와 y의 값과 타입이 같음 |     X     |
|     !=      | 부동등 비교 | x != y  | x와 y의 값이 다름        |     X     |
|     !==     | 불일치 비교 | x !== y | x와 y의 값과 타입이 다름 |     X     |



**(주의)** 동등 비교 연산자는 **타입**에 관계없이 **값**이 같으면 `true`를 반환함. **일치 비교 연산자**를 사용하도록 하자. 단, 일치 비교 연사자에서는 `NaN`을 주의하자.

``` javascript
// NaN은 자신과 일치하지 않는 유일한 값이다.
NaN === NaN; // false

// 빌트인 함수 isNan()은 주어진 값이 NaN인지 체크하고 결과를 반환한다.
isNaN(NaN); // true
isNaN(10);  // false
isNaN(1 + undefined); // true
```



#### 6. 대소 관계 비교 연산자

피연산자의 크기를 비교하여 불리언 값을 반환한다.

| 대소 관계 비교 연산자 | 예제   | 설명                  | 부수효과 |
| :-------------------: | :----- | :-------------------- | :------: |
|           >           | x > y  | x가 y보다 크다        |    X     |
|           <           | x < y  | x가 y보다 작다        |    X     |
|          >=           | x >= y | x가 y보다 같거나 크다 |    X     |
|          <=           | x <= y | x가 y보다 같거나 크다 |    X     |



#### 7. 삼항 조건 연산자

조건식의 평가 결과에 따라 반환할 값을 결정한다. 자바스크립트의  **유일한** 삼항 연산자이며, 부수 효과는 없다.

``` javascript
조건식 ? (조건식이 true일때 반환할 값) : (조건식이 false일때 반환할 값)
```



만약 조건식의 평가 결과가 boolean 값이 아니면 **boolean 값으로 암묵적 타입 변환된다.**

``` javascript
// example 1
var x = 2;
var result = x % 2 ? '홀수' : '짝수'; // 2 % 2는 0이고 0은 false로 암묵적 타입 변환된다.
console.log(result); // 짝수

// example 2
var age = 26;
var beverage = (age >= 21) ? "Beer" : "Juice"; // (age >= 21)는 true
console.log(beverage); // "Beer"

// example 3 - handling a value that may be null
function greeting(person) {
    var name = person ? person.name : "stranger";
    return "Howdy, " + name;
}

console.log(greeting({name: 'Alice'}));  // "Howdy, Alice"
console.log(greeting(null));             // "Howdy, stranger"
```

**삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식인 문이다.** 따라서 삼항 조건 연산자식은 다른 표현식의 일부가 될 수 있어 매우 유용하다.



#### 8. 논리 연산자

| 논리 연산자 | 의미 | 부수 효과 |
| :---------: | :--: | :-------: |
|    \|\|     |  OR  |     X     |
|     &&      | AND  |     X     |
|      !      | NOT  |     X     |



논리 부정(!) 연산자는 언제나 불리언 값을 반환한다. **단, 피연산자는 반드시 불리언 값일 필요는 없다. 만약 피연산자가 불리언 값이 아니면 불리언 타입으로 암묵적 타입 변환된다.**

``` javascript
// 암묵적 타입 변환
!0;       // -> true
!'Hello'; // -> false, 1개 이상의 문자를 포함한 문자열은 true로 인식된다
```



**드 모르간의 법칙**

복잡한 표현식을 좀 더 가독성 좋은 표현식으로 변환할 수 있다.

```javascript
!(x || y) === (!x && !y)
!(x && y) === (!x || !y)
```



#### 9. 쉼표 연산자

쉼표(,) 연산자는 왼쪽 피연산자부터 차례대로 피연산자를 평가하고 마지막 피연산자의 평가가 끝나면 **마지막 피연산자의 평가 결과를 반환한다.**

``` javascript
var x, y, z;

x = 1, y = 2, z = 3; // 3
```



#### 10. typeof 연산자

`typeof()` 연산자는 자신의 뒤에 위치한 피연산자의 데이터 타입을 문자열로 반환한다. `typeof()` 연산자는 7가지 문자열 (string, number, boolean, undefined, symbol, object, function) 중 하나를 반환한다. **null을 반환하는 경우는 없으며, 함수의 경우 function을 반환한다.**

``` javascript
typeof ''              // -> "string"
typeof 1               // -> "number"
typeof NaN             // -> "number"
typeof true            // -> "boolean"
typeof undefined       // -> "undefined"
typeof Symbol()        // -> "symbol"
typeof null            // -> "object" ????????????????? JS 첫 번째 버전의 버그
typeof []              // -> "object"
typeof {}              // -> "object"
typeof new Date()      // -> "object"
typeof /test/gi        // -> "object"
typeof function () {}  // -> "function"
```

따라서, null 타입을 확인할 때는 일치 연산자 (===)를 사용

``` javascript
var foo = null;

typeof foo === null; // -> false
foo === null;        // -> true
```



#### 11. 지수 연산자 (Math.pow(n, e))

``` javascript
// ES 7
5 ** 2;   // -> 25
5 ** 2.5; // -> 55.90169943749474
5 ** 0;   // -> 1
5 ** -2;  // -> 0.04
(-5) ** 2; // 음수를 밑으로 계산하려면 괄호로 묶어야 한다.

// Before ES 7
Math.pow(5, 2);   // -> 25
Math.pow(5, 2.5); // -> 55.90169943749474
Math.pow(5, 0);   // -> 1
Math.pow(5, -2);  // -> 0.04
```

지수 연산자는 **모든 이항 연산자보다 우선 순위가 높다.**



([prev - Introduction to JavaScript, Variable](./intro-js-variable.md))

([Back to List](../../README.md))

