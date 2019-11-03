# 타입 변환과 단축 평가

## 1. 타입 변환이란?

개발자가 의도적으로 값의 타입을 변환하는 것을 **타입 캐스팅 (Type Casting), 명시적 타입 변환(Explicit coercion)**이라 한다.

```javascript
var x = 10;

// 명시적 타입 변환
// 숫자를 문자열로 타입 캐스팅한다.
var str = x.toString();
console.log(typeof str, str); // string 10

// 변수 x의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10
```



동적 타입 언어인 자바스크립트는 개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 **암묵적으로 타입이 자동 변환되기도 한다.** 이를 **타입 강제 변환(Type coercion), 암묵적 타입 변환 (Implicit coercion)**이라 한다.

```javascript
var x = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
var str = x + '';
console.log(typeof str, str); // string 10

// 변수 x의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10
```

**암묵적 타입 변환**은 변수의 값을 재할당해서 변경하는 것이 아니라, 자바스크립트 엔진이 표현식을 에러없이 평가하기 위해 변수의 값을 바탕으로 **새로운 타입의 값을 만들어 단 한번 사용하고 버린다.**

때로는 명시적 타입 변환보다 암묵적 타입 변환이 가독성 측면에서 더 좋을 수도 있다.

```javascript
var x = (10).toString(); // 명시적
var x = 10 + ''; // 암묵적
```



## 2. 암묵적 타입 변환

**자바스크립트 엔진은 표현식을 평가할 때 코드의 문맥을 고려하여 암묵적 타입 변환을 실행한다.**

``` javascript
// 피연산자가 모두 문자열 타입이여야 하는 문맥
'10' + 2  // '102'

// 피연산자가 모두 숫자 타입이여야 하는 문맥
5 * '10'  // 50

// 피연산자 또는 표현식이 불리언 타입이여야 하는 문맥
!0 // true
if (1) { }
```



### 2.1. 문자열 타입으로 변환

```javascript
1 + '2' // "12"
```

위 예제의 **+** 연산자는 피연산자 중 하나 이상이 문자열이므로, 문자열 연결 연산자로 동작한다. 따라서, 자바스크립트 엔진은 문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환한다.

``` javascript
// 숫자 타입
0 + ''              // "0"
-0 + ''             // "0"
1 + ''              // "1"
-1 + ''             // "-1"
NaN + ''            // "NaN"
Infinity + ''       // "Infinity"
-Infinity + ''      // "-Infinity"

// 불리언 타입
true + ''           // "true"
false + ''          // "false"

// null 타입
null + ''           // "null"

// undefined 타입
undefined + ''      // "undefined"

// 심볼 타입
(Symbol()) + ''     // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''           // "[object Object]"
Math + ''           // "[object Math]"
[] + ''             // ""
[10, 20] + ''       // "10,20"
(function(){}) + '' // "function(){}"
Array + ''          // "function Array() { [native code] }"
```



ES6에서 도입된 **템플릿 리터럴**의 **String Interpolation** 또한 표현식의 평가 결과를 문자열 타입으로 암묵적 타입 변환한다. 

``` javascript
console.log(`1 + 1 = ${1 + 1}`); // "1 + 1 = 2"
```



### 2.2. 숫자 타입으로 변환

```javascript
1 - '1'    // 0
1 * '10'   // 10
1 / 'one'  // NaN
'1' > 0    // true
```

**(질문)** 문자열과 숫자 타입의 값 사이 **+** 연산자는 무조건 문자열 타입으로만 변환되는지? 어느 한쪽이 string이라면 string이 아닌 쪽을 문자열로 변환



**+** **단항 연산**자는 피연산자가 숫자 타입의 값이 아니면, 숫자 타입의 값으로 암묵적 타입 변환을 수행

```javascript
// 문자열 타입
+''             // 0 - 비어 있는 문자열
+'0'            // 0
+'1'            // 1
+'string'       // NaN

// 불리언 타입
+true           // 1
+false          // 0

// null 타입
+null           // 0

// undefined 타입
+undefined      // NaN

// 심볼 타입
+Symbol()       // TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}             // NaN
+[]             // 0 - 비어 있는 배열
+[10, 20]       // NaN
+(function(){}) // NaN
```



### 2.3. 불리언 타입으로 변환

`if`문이나 `for`문과 같은 제어문, 또는 삼항 조건 연산자의 **조건식은 boolean 값을 반환해야하는 표현식이다**. 자바스크립트 엔진은 조건식의 평가 결과를 boolean 타입으로 암묵적 타입 변환한다.

``` javascript
if ('')    console.log('1'); // '' as empty string, representing false
if (true)  console.log('2'); // always true
if (0)     console.log('3'); // 0 as falsy value, false
if ('str') console.log('4'); // 'str' as string withe legnth, representing true
if (null)  console.log('5'); // null as falsy value, false

// 2 4
```

이때 자바스크립트 엔진은 boolean 타입이 아닌 값을 **Truthy value 또는 Falsy value**로 구분한다.

* false
* undefined
* null
* 0, -0
* NaN
* '' (empty string)



## 3.명시적 타입 변환

### 3.1. 문자열 타입으로 변환

* String 생성자 함수를 new 연산자 없이 호출하는 방법
* Object.prototype.toString 메소드를 사용하는 방법
* 문자열 연결 연산자를 이용하는 방법

``` javascript
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 => 문자열 타입
console.log(String(1));        // "1"
console.log(String(NaN));      // "NaN"
console.log(String(Infinity)); // "Infinity"
// 불리언 타입 => 문자열 타입
console.log(String(true));     // "true"
console.log(String(false));    // "false"

// 2. Object.prototype.toString 메소드를 사용하는 방법
// 숫자 타입 => 문자열 타입
console.log((1).toString());        // "1"
console.log((NaN).toString());      // "NaN"
console.log((Infinity).toString()); // "Infinity"
// 불리언 타입 => 문자열 타입
console.log((true).toString());     // "true"
console.log((false).toString());    // "false"

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 => 문자열 타입
console.log(1 + '');        // "1"
console.log(NaN + '');      // "NaN"
console.log(Infinity + ''); // "Infinity"
// 불리언 타입 => 문자열 타입
console.log(true + '');     // "true"
console.log(false + '');    // "false"
```



### 3.2. 숫자 타입으로 변환

- Number 생성자 함수를 new 연산자 없이 호출하는 방법
- parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
- \+ 단항 연결 연산자를 이용하는 방법
- \* 산술 연산자를 이용하는 방법

```javascript
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 숫자 타입
console.log(Number('0'));     // 0
console.log(Number('-1'));    // -1
console.log(Number('10.53')); // 10.53
// 불리언 타입 => 숫자 타입
console.log(Number(true));    // 1
console.log(Number(false));   // 0

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 변환 가능)
// 문자열 타입 => 숫자 타입
console.log(parseInt('0'));       // 0
console.log(parseInt('-1'));      // -1
console.log(parseFloat('10.53')); // 10.53

// 3. + 단항 연결 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
console.log(+'0');     // 0
console.log(+'-1');    // -1
console.log(+'10.53'); // 10.53
// 불리언 타입 => 숫자 타입
console.log(+true);    // 1
console.log(+false);   // 0

// 4. * 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
console.log('0' * 1);     // 0
console.log('-1' * 1);    // -1
console.log('10.53' * 1); // 10.53
// 불리언 타입 => 숫자 타입
console.log(true * 1);    // 1
console.log(false * 1);   // 0
```



### 3.3. 불리언 타입으로 변환

- Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
- ! 부정 논리 연산자를 두번 사용하는 방법

```javascript
// 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 불리언 타입
console.log(Boolean('x'));       // true
console.log(Boolean(''));        // false
console.log(Boolean('false'));   // true
// 숫자 타입 => 불리언 타입
console.log(Boolean(0));         // false
console.log(Boolean(1));         // true
console.log(Boolean(NaN));       // false
console.log(Boolean(Infinity));  // true
// null 타입 => 불리언 타입
console.log(Boolean(null));      // false
// undefined 타입 => 불리언 타 입
console.log(Boolean(undefined)); // false
// 객체 타입 => 불리언 타입
console.log(Boolean({}));        // true - 객체는 비어있어도 true
console.log(Boolean([]));        // true

// 2. ! 부정 논리 연산자를 두번 사용하는 방법
// 문자열 타입 => 불리언 타입
console.log(!!'x');       // true
console.log(!!'');        // false
console.log(!!'false');   // true
// 숫자 타입 => 불리언 타입
console.log(!!0);         // false
console.log(!!1);         // true
console.log(!!NaN);       // false
console.log(!!Infinity);  // true
// null 타입 => 불리언 타입
console.log(!!null);      // false
// undefined 타입 => 불리언 타입
console.log(!!undefined); // false
// 객체 타입 => 불리언 타입
console.log(!!{});        // true
console.log(!![]);        // true
```



## 4. 단축 평가

**OR (|| - 논리합), AND (&& - 논리곱)** 연산자의 결과 값은 **불리언 값이 아닐 수도 있다.** 이  두 연산자는 **언제나 피연산자 중 어느 한쪽 값을 반환한다.** 

``` javascript
// 논리합(||) 연산자
'Cat' || 'Dog'  // 'Cat' - truthy value
false || 'Dog'  // 'Dog' - truthy value
'Cat' || false  // 'Cat' - truthy value

// 논리곱(&&) 연산자
'Cat' && 'Dog'  // Dog
false && 'Dog'  // false
'Cat' && false  // false
```

논리곱 연산자 `&&`와 논리합 연산자 `||`는 이와 같이 **논리 평가를 결정한 피연산자를 그대로 반환한다. 이를 단축 평가 (Short-circuit evaluation)라 부른다. **단축 평가는 아래의 규칙을 따른다.

| 단축 평가 표현식    | 평가 결과 |
| ------------------- | --------- |
| true \|\| anything  | true      |
| false \|\| anything | anything  |
| true && anything    | anything  |
| false && anything   | false     |



단축 평가는 아래와 같은 상황에서 유용하게 사용된다.

* 객체가 null인지 확인하고 프로퍼티를 참고할 때

  ``` javascript
  var elem = null;
  
  console.log(elem.value); // 일반 변수에 프로퍼티를 참조하려 하면 TypeError가 발생한다
  console.log(elem && elem.value); // elem은 null (falsy) 값을 가지고 있으므로 && 이후의 연산을 할 필요 없이 바로 null을 출력한다.
  ```



* 함수 매개변수에 기본값을 설정할 때

  ```javascript
  function getStringLength(str) {
      // 매개변수 str이 true (길이가 있다면)면 str = str로 설정
      // 매개변수 str이 false (길이가 없다면)면 str = ''로 설정
      str = str || ''; 
      return str.length;
  }
  ```

