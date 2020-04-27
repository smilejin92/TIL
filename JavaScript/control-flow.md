# 제어문

제어문(control flow statement)은 주어진 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행된다. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.

## 1. 블록문

* 블록문(block statement / compound statement)은 0개 이상의 문을 중괄호로 묶은 것으로 **코드 블록** 또는 **블록**이라고 부르기도 한다.
* 자바스크립트는 블록문을 하나의 실행 단위로 취급한다.
* 블록문은 단독으로 사용할 수도 있으나 일반적으로 제어문이나 함수를 정의할 때 사용하는 것이 일반적이다.
* 블록문은 언제나 문의 종료를 의미하는 자체 종결성(self closing)을 갖기 때문에 블록문의 끝에는 세미콜론을 붙이지 않는다.

```javascript
// 블록문
{
  var foo = 10;
}

// 제어문
var x = 1;
if (x < 10) {
  x++;
}

// 함수 선언문
function sum(a, b) {
  return a + b;
}
```

&nbsp;  

## 2. 조건문

* 조건문(conditional statement)은 주어진 조건식(conditional expression)의 평가 결과에 따라 코드 블럭의 실행을 결정한다.
* 조건식은 불리언 값으로 평가될 수 있는 표현식이다.



### 2.1. if...else 문

* if...else 문은 주어진 조건식의 평가 결과(논리적 참/거짓)에 따라 실행 할 코드 블록을 결정한다.
* 조건식의 평가 결과가 true일 경우, if 문 다음의 코드 블록이 실행되고, false일 경우 else 문 다음의 코드 블록이 실행된다.
* 만약 if 문의 조건식이 불리언 값이 아닌 값으로 평가되면 자바스크립트 엔진에 의해 암묵적으로 데이터 타입이 불리언 값으로 강제 변환되어 실행할 코드 블록을 결정한다.
* 조건식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶으면 else if 문을 사용한다.
* else if 문과 else 문은 옵션이다.
* if 문과 else 문은 2번 이상 사용할 수 없지만 else if 문은 여러 번 사용할 수 있다.
* 만약 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.

```javascript
if (조건식) {
  // 조건식이 참이면 이 코드 블록이 실행된다.
} else {
  // 조건식이 거짓이면 이 코드 블록이 실행된다.
}
```

if 문의 조건식은 불리언 값으로 평가되어야 한다. **만약 if 문의 조건식이 불리언 값이 아닌 값으로 평가되면 자바스크립트 엔진에 의해 암묵적으로 데이터 타입이 불리언 값으로 강제 변환되어 실행할 코드 블록을 결정한다.**

조건식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶으면 else if 문을 사용한다.

```javascript
if (조건식1) {
  // 조건식1이 참이면 이 코드 블록이 실행된다.
} else if (조건식2) {
  // 조건식2가 참이면 이 코드 블록이 실행된다.
} else {
  // 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```

else if 문과 else 문은 옵션이다. if 문과 else 문은 2번 이상 사용할 수 없지만 else if 문은 여러 번 사용할 수 있다.

```javascript
// if 문
if (num > 0) {
  kind = '양수';
}

// if...else 문
if (num > 0) {
  kind = '양수'
} else {
  kind = '음수'
}

// if...else if 문
if (num > 0) {
  kind = '양수';
} else if (num < 0) {
  kind = '음수';
} else {
  kind = '0';
}
```

만약 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.

```javascript
if (num > 0) kind = '양수';
else if (num < 0) kind = '음수';
else kind = '0';
```

&nbsp;  

### 2.2 switch 문

* switch 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 순서를 이동시킨다. 
* case문은 상황(case)을 의미하는 표현식을 지정하고 콜론으로 마친다. 그리고 그 뒤에 실행할 문들을 위치시킨다.
* 만약 switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없다면 실행 순서는 default 문으로 이동한다.
* break 문이 없다면 case 문의 표현식과 일치하지 않더라도 실행 순서는 다음 case 문으로 연이어 이동한다 (Fall through)
* default 문에는 break 문을 생략하는 것이 일반적이다.

```javascript
switch (표현식) {
  case 표현식1:
    표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
}
```

if...else 문의 조건식은 불리언 값으로 평가되어야 하지만, switch 문의 표현식은 문자열, 숫자 값인 경우가 많다. **switch 문은 논리적 참/거짓 보다는 다양한 상황(case)에 따라 실행할 코드 블록을 결정할 때 사용한다.**

아래 예제는 switch문을 사용해 변수 `month`의 값에 해당하는 월을 `monthName`에 할당하는 예제이다.

```javascript
// 월을 영어로 변환 (ex. 11 -> 'November')
var month = 11;
var monthName;

switch (month) {
  case 1: monthName = 'January';
  case 2: monthName = 'Feburary';
  case 3: monthName = 'March';
  case 4: monthName = 'April';
  case 5: monthName = 'May';
  case 6: monthName = 'June';
  case 7: monthName = 'July';
  case 8: monthName = 'August';
  case 9: monthName = 'September';
  case 10: monthName = 'October';
  case 11: monthName = 'November';
  case 12: monthName = 'December';
  default: monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```

위 예제의 의도는 변수 `monthName`에 문자열 'November'를 할당하는 것이었다. 하지만 switch 문이 종료되고 `monthName`을 콘솔에 출력하면 'Invalid month' 문자열이 출력된다. 이는 switch 문의 표현식의 평가 결과와 일치하는 case 문으로 이동하여 문을 실행한 것은 맞지만, 문을 실행한 후 switch 문을 **탈출**하지 않고 해당 case 이후의 모든 case 문과 default 문을 실행했기 때문이다. 이를 **폴스루(Fall through)**라 한다.

1. `monthName = 'November';` (case 11)
2. `monthName = 'December';` (case 12)
3. `monthName = 'Invalid month';` (default)

폴스루를 방지하려면, case 문에 해당하는 문의 마지막에 break 문을 사용하지 않았기 때문이다. break 문이 없다면 case 문의 표현식과 일치하지 않더라도 실행 순서는 다음 case 문으로 연이어 이동한다. 단, default 문에는 break 문을 생략하는 것이 일반적이다. default 문은 switch 문의 가장 마지막에 위치하므로 default 문의 실행이 종료되면 switch 문을 빠져나간다.

&nbsp;  

## 3. 반복문

반복문(Loop Statement)은 주어진 조건식의 평가 결과가 참인 경우 코드 블럭을 실행한다. 그 후 조건식을 다시 검사하여 여전히 참인 경우 코드 블록을 다시 실행한다. 이는 조건식이 거짓일 때까지 반복된다.

### 3.1. for 문

for 문은 조건식이 거짓으로 판별될 때까지 코드 블록을 반복 실행한다. 

```javascript
// 문법
for (변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}

// 예제
for (var i = 0; i < 2; i++) {
  console.log(i);
}

// 출력
// 1
// 2
```

위 예제는 아래의 과정을 통해 실행된다.

1. for 문 최초 실행시 변수 선언문 `var i = 0`이 실행. 변수 선언문은 최초에만 실행된다.
2. `i < 2` 조건식 평가(`true`)
3. 2의 결과가 true이므로 코드 블록으로 이동하여 실행(`console.log(i)`)
4. `i++` 증감식 실행
5. 2로 이동하여 반복

for 문의 변수 선언문, 조건식, 증감식은 모두 옵션이므로 반드시 사용할 필요는 없다. 어떤 식도 선언하지 않으면 무한 루프가 된다.

```javascript
// 무한 루프
for () {
  ...
}
```

for 문 내에 for 문을 중첩하여 사용할 수 있다.

```javascript
// 100회 반복 (10 * 10)
for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    ...
  }
}
```

&nbsp;  

### 3.2. while 문

while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. 조건문의 평가 결과가 거짓이되면 실행을 종료한다. 만약 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환되어 논리적 참/거짓을 구별한다.

```javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}

// 조건식의 평가 결과가 언제나 참이면 무한 루프가 된다.
while (true) {
  ...
}

// 무한루프를 탈출하기 위해서는 코드 블럭 내에 탈출 조건을 만들고 break 문으로 코드 블럭을 탈출한다.
while (true) {
  console.log(count);
  count++;
  // count가 3이면 코드 블록을 탈출
  if (count === 3) break;
}
```

&nbsp;  

## 4. break 문

break 문은 레이블 문, 반복문 또는 switch 문의 코드 블록을 탈출한다. 그 외에 break문을 사용하면 SyntaxError(문법 에러)가 발생한다.

중첩된 for 문의 내부 for 문에서 break 문을 실행하면 외부 for 문으로 진입한다. break 문은 반복문에서 불필요한 반복을 회피할 수 있어 유용하다.

```javascript
for (var i = 0; i < 5; i++) { // outer
  for (var j = 0; j < 5; j++) { // inner
     if (j === 1) break; // j가 1이면 inner 밖으로 탈출
  }
  // 탈출 후 위치
}
```

&nbsp;  

break 문은 switch 문에서 폴 스루(fall through)를 방지하는 용도로 사용할 수 있다.

```javascript
var month = 1;

switch (month) {
  case 1:
    console.log('January');
    break;
  case 2:
    console.log('Feburary');
    break;
  default:
    console.log('Invalid month');
}
// January
```

&nbsp;  

## 5. continue 문

continue 문은 반복문의 코드 블록 실행을 현 시점에서 중단하고, 반복문의 증감식으로 이동한다. break 문처럼 반복문을 탈출하지 않는다.

아래는 문자열에서 특정 문자의 개수를 카운트하는 예제이다.

```javascript
var string = 'Hello World.';
var search = 'l';
var count = 0;

for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}
```

&nbsp;  

## 참고 자료

* [poiemaweb.com - 제어문](https://poiemaweb.com/fastcampus/control-flow)

