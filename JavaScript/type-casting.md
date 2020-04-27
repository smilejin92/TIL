# 타입 변환과 단축 평가

## 1. 타입 변환이란?

개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입 변환(explicit coercion)** 또는 **타입 캐스팅(type casting)**이라 한다.

```javascript
var x = 10;

// 명시적 타입 변환
// 숫자를 문자열로 타입 캐스팅한다.
var str = x.toString();
console.log(typeof str); // string

// 변수 x의 값이 변경된 것은 아니다.
console.log(typeof x); // number
```

개발자의 의도와는 상관 없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되기도 한다. 이를 **암묵적 타입 변환(implicit coercion)** 또는 **타입 강제 변환(type coercion)**이라고 한다.

```javascript
var x = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
var str = x + '';
console.log(typeof str); // string

// 변수 x의 값이 변경된 것은 아니다.
console.log(typeof x); // number
```

명시적 타입 변환이나 암묵적 타입 변환이 기존 원시 값을 직접 변경하는 것은 아니다. 원시 값은 변경 불가능한 값(immutable value)이므로 변경할 수 없다. **타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.**

&nbsp;  

## 2. 암묵적 타입 변환

자바스크립트 엔진은 표현식을 평가할 때 개발자의 의도와는 상관없이 코드의 문맥을 고려하여 암묵적으로 데이터 타입을 강제 변환(암묵적 타입 변환)할 때가 있다.

```javascript
// 피연산자가 모두 문자열 타입이어야 하는 문맥
'10' + 2 // '102'

// 피연산자가 모두 숫자 타입이어야 하는 문맥
5 * '10' // 50

// 피연산자 또는 표현식이 불리언 타입이어야 하는 문맥
!0 // true
if (1) { } // 1 = true
```

이처럼 표현식을 평가할 때 코드의 문맥에 부합하지 않는 다양한 상황이 발생할 수 있다. 이때 자바스크립트는 가급적 에러를 발생시키지 않도록 암묵적 타입 변환을 통해 표현식을 평가한다.

암묵적 타입 변환이 발생하면 문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환한다.

&nbsp;  

### 2.1. 문자열 타입으로 변환

```javascript
1 + '2' // '12'
```

위 예제의 `+` 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다. 자바스크립트 엔진은 문자열 연결 연산자 표현식을 평가하기 위해 문자열 연결 연산자의 피연산자 중 문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환한다.

또한 자바스크립트 엔진은 표현식을 평가할 때 코드 문맥에 부합하도록 암묵적 타입 변환을 실행한다. 예를 들어, ES6에서 도입된 템플릿 리터럴의 표현식 삽입은 표현식의 평가 결과를 문자열 타입으로 암묵적 타입 변환한다.

```javascript
console.log(`1 + 1 = ${1 + 1}`); // '1 + 1 = 2'
```

자바스크립트 엔진은 문자열 타입이 아닌 값을 문자열 타입으로 암묵적 타입 변환을 수행할 때 아래와 같이 동작한다.

```javascript
// 숫자 타입
0 + '' // '0'
NaN + '' // 'NaN'
Infinity + '' // 'Infinity'

// 불리언 타입
true + '' // 'true'
false + '' // 'false'

// null 타입
null + '' // 'null'

// undefined 타입
undefined + '' // 'undefined'

// Symbol 타입
(Symbol()) + '' // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + '' // '[object Object]'
[] + '' // ''
[10, 20] + '' // '10,20'
```

&nbsp;  

### 2.2. 숫자 타입으로 변환

**산술 연산자**

```javascript
1 - '1' // 0
1 * '10' // 10
1 / 'one' // NaN
```

위 예제에서 사용한 연산자는 모두 산술 연산자이다. 산술 연산자의 역할은 숫자 값을 만드는 것이다. 따라서 산술 연산자의 모든 피연산자는 코드 문맥 상 모두 숫자 타입이어야 한다.

자바스크립트 엔진은 산술 연산자 표현식을 평가하기 위해 산술 연산자의 피연산자 중 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환한다. 이때 피연산자를 숫자 타입으로 변환할 수 없는 경우 표현식의 평가 결과는 NaN이 된다.

&nbsp;  

**비교 연산자**

```javascript
'1' > 0 // true
```

비교 연산자의 역할은 불리언 값을 만드는 것이다. `>` 비교 연산자는 피연산자의 크기를 비교하므로 모든 연산자는 코드의 문맥 상 모두 숫자 타입이어야 한다. 자바스크립트 엔진은 비교 연산자 표현식을 평가하기 위해 비교 연산자의 피연산자 중 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환한다.

&nbsp;  

**+ 단항 연산자**

`+` 단항 연산자는 피연산자가 숫자 타입의 값이 아니면 숫자 타입의 값으로 암묵적 타입 변환을 수행한다.

```javascript
// 문자열 타입
+'' // 0
+'0' // 0
+'1' // 1
+'string' // NaN

// 불리언 타입
+true // 1
+false // 0

// null 타입
+null // 0

// undefined 타입
+undefined // NaN

// Symbol 타입
+Symbol() // TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{} // NaN
+[] // 0
+[10, 20] // NaN
```

&nbsp;  

### 2.3. 불리언 타입으로 변환

if 문이나 for 문과 같은 제어문 도는 삼항 조건 연산자의 조건식은 불리언 값을 반환해야 하는 표현식이다. 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환한다.

```javascript
if ('') console.log('1');
if (true) console.log('2');
if (0) console.log('3');
if ('str') console.log('4');
if (null) console.log('5');

// 2 4
```

이때 **자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy 값(참으로 평가되는 값) 또는 Falsy 값(거짓으로 평가되는 값)으로 구분한다.** 제어문의 조건식과 같이 불리언 값으로 평가되어야 할 문맥에서 Truthy 값은 true로, Falsy 값은 false로 암묵적 타입 변환된다.

**Falsy 값**

* false
* undefined
* null
* 0, -0
* NaN
* '' (빈문자열)

Falsy 값 이외의 모든 값은 모두 true로 평가되는 Truthy 값이다.

&nbsp;  

## 3. 명시적 타입 변환

개발자의 의도에 의해 명시적으로 타입을 변경하는 방법은 다양하다.

* `new` 연산자 없이 표준 빌트인 생성자 함수를 호출
* 빌트인 메소드
* 암묵적 타입 변환 사용

> **표준 빌트인 생성자 함수와 빌트인 메소드**
>
> 표준 빌트인(built-in) 생성자 함수와 표준 빌트인 메소드는 자바스크립트에서 기본 제공하는 함수이다. 표준 빌트인 생성자 함수는 객체를 생성하기 위한 함수이며 `new` 연산자와 함께 호출한다. 표준 빌트인 메소드는 자바스크립트에서 기본 제공하는 빌트인 객체의 메소드이다.

&nbsp;  

### 3.1. 문자열 타입으로 변환

문자열 타입이 아닌 값을 문자열 타입으로 변화하는 방법은 아래와 같다.

```javascript
// 1. new 연산자 없이 String 생성자 함수를 호출
String(1); // '1'
String(NaN); // 'NaN'
String(Infinity); // 'Infinity'
String(true); // 'true'

// 2. Object.prototype.toString 메소드 사용
(1).toString(); // '1'
(NaN).toString(); // 'NaN'
(Infinity).toString(); // 'Infinity'
(true).toString(); // 'true'

// 3. 문자열 연결 연산자를 이용하는 방법
1 + ''; // '1'
NaN + ''; // 'NaN'
Infinity + ''; // 'Infinity'
true + ''; // 'true'
```

&nbsp;  

### 3.2. 숫자 타입으로 변환

숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법은 아래와 같다.

```javascript
// 1. new 연산자 없이 Number 생성자 함수를 호출
Number('0'); // 0
Number('-1'); // -1
Number('10.53'); // 10.53
Number(true); // 1

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 변환 가능)
parseInt('0'); // 0
parseint('-1'); // -1
parseFloat('10.53'); // 10.53

// 3. + 단항 산술 연산자를 이용하는 방법
+'0'; // 0
+'-1'; // -1
+'10.53'; // 10.53
+true; // 1

// 4. * 산술 연산자를 이용하는 방법
'0' * 1; // 0
'-1' * 1; // -1
'10.53' * 1; // 10.53
true * 1; // 1
```

&nbsp;  

### 3.3. 불리언 타입으로 변환

불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법은 아래와 같다.

```javascript
// 1. new 연산자 없이 Boolean 생성자 함수를 호출
Boolean('string with length'); // true
Boolean(''); // false
Boolean(0); // false
Boolean(NaN); // false
Boolean(Infinity); // true
Boolean(null); // false
Boolean(undefined); // false
Boolean({}); // true

// 2. ! 부정 논리 연산자를 두번 사용하는 방법
!!'string with length'; // true
!!''; // false
!!0; // false
!!NaN; // false
!!Infinity; // true
!!null; // false
!!undefined; // false
!!{}; // true
```

&nbsp;  

## 4. 단축 평가

AND 연산자와 OR 연산자는 **논리 연산의 결과를 결정한 피연산자를 타입 변환하지 않고 그대로 반환한다. 이를 단축 평가(short-circuit evaluation)라 부른다. 단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우, 나머지 평가 과정을 중단하는 것이다.**

&nbsp;  

**AND 연산자**

```javascript
'Cat' && 'Dog' // 'Dog'
```

**AND 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다.** AND 연산자는 결합 순서가 좌항에서 우항으로 평가가 진행된다.

첫 번째 피연산자 'Cat'은 Truthy 값이므로 true로 평가된다. 하지만 이 시점까지는 평가 결과를 알 수 없다. 두 번째 피연산자까지 평가해 보아야 위 표현식을 평가할 수 있다. 두 번째 피연산자 'Dog'도 Truthy 값이므로 위 표현식의 평가 결과는 'Dog'이다. **AND 연산자는 논리 연산의 결과를 결정한 두 번째 피연산자를 그대로 반환한다.**

&nbsp;  

**OR 연산자**

OR 연산자도 AND 연산자와 동일하게 동작한다.

```javascript
'Cat' || 'Dog' // 'Cat'
```

OR 연산자는 두 개의 피연산자 중 하나만 true로 평가되어도 true를 반환한다. OR 연산자도 왼쪽에서 오른쪽으로 평가가 진행된다.

첫 번째 피연산자 'Cat'은 Truthy 값이므로 true로 평가된다. 이 시점에 두 번째 피연산자까지 평가해 보지 않아도 위 표현식을 평가할 수 있다. 이때 **OR 연산자는 논리 연산의 결과를 결정한 첫 번째 피연산자 'Cat'을 그대로 반환한다.**

단축 평가는 아래 규칙을 따른다.

| 단축 평가 표현식    | 평가 결과 |
| ------------------- | --------- |
| true \|\| anything  | true      |
| false \|\| anything | anything  |
| true && anything    | anything  |
| false && anything   | false     |

```javascript
// OR 연산자
'Cat' || 'Dog' // 'Cat'
false || 'Dog' // 'Dog'
'Cat' || false // 'Cat'

// AND 연산자
'Cat' && 'Dog' // 'Dog'
false && 'Dog' // false
'Cat' && false // false
```

&nbsp;  

단축 평가는 아래와 같은 경우에 유용하게 쓰인다.

```javascript
// 1. 객체를 가리키는 변수가 null(또는 undefined)인지 확인하고 프로퍼티를 참조할 때
var elem = null;

var value = elem.value; // TypeError: Cannot read property 'value' of null
var value = elem && elem.value; // elem이 truthy 객체면 elem.value를 할당 


// 2. 함수 매개변수에 기본 값을 설정할 때
// ES5
function getStringLength(str) {
  str = str || '';
  return str.length;
}

// ES6
function getStringLength(str = '') {
  return str.length;
}
```

&nbsp;  

## 참고 자료

* [poiemaweb.com - 타입 변환과 단축 평가](https://poiemaweb.com/fastcampus/type-casting)

