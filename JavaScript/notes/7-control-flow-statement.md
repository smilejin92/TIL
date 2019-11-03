# 제어문

제어문(control flow statement)은 주어진 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다.

## 1. 블록문 (Block statement)

* **0개 이상의 문**(statement)을 중괄호로 묶은 것을 **코드 블록** 또는 **블록문**이라고 부른다.
* 하나의 실행 단위로 취급된다.
* 대체로 제어문이나, 함수 선언문 등에서 사용하는 것이 일반적이다.
* 블록문 끝에는 세미콜론(;)을 붙이지 않는다.
* **자바스크립트는 함수 외에 코드블록은 스코프의 역할을 안한다 (var를 사용했을때)**

``` javascript
// 블록문
// foo = undefined;
{
    var foo = 10;
    console.log(foo);
}
// foo = 10;

// 제어문
while (x < 10) {
    x++;
}

// 함수 선언문
function sum(a, b) {
    return a + b;
}
```



## 2. 조건문

조건문 (conditional statement)은 주어진 **조건식(conditional expression)의 평가 결과에 따라 코드 블럭의 실행을 결정한다.** 조건식은 boolean 값으로 평가될 수 있는 표현식이다.

### 2.1. if / else if / else 문

``` javascript
if (조건식1) {
  // 조건식1이 참이면 이 코드 블록이 실행된다.
} else if (조건식2) {
  // 조건식2이 참이면 이 코드 블록이 실행된다.
} else {
  // 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```

**삼항 조건 연산자**로 단축하여 사용하기도 한다 (see ch. 6). 단, 삼항 조건 연산자는 **값으로 평가되는 표현식을 만들지만**, `if..else`문은 표현식이 아닌 문이다. 따라서 `if..else`문은 변수에 할당할 수 없다.

``` javascript
var num = 2;
var kind = num ? (num > 0 ? '양수' : '음수') : '영';
console.log(kind); // 양수
```



### 2.2. switch 문

`switch` 문은 주어진 표현식을 평가하여, 그 값과 일치하는 표현식을 갖는 `case` 문으로 실행 순서를 이동시킨다. `switch`문의 표현식과 일치하는 표현식을 갖는 `case`문이 없다면, 실행 순서는 `default` 문으로 이동한다.

``` javascript
switch (expression) {
    case expression1:
        // expression과 expression1이 일치하면 실행될 문
        break;
    case expression2:
        // expression과 expression2가 일치하면 실행될 문
        break;
    default:
        // expression과 일치하는 표현식을 갖는 case가 없을 때 실행될 문
}
```

`if..else` 문의 조건식은 **반드시 불리언 값으로 평가되지만,** `switch`문의 표현식은 **문자열, 숫자 값**인 경우가 많다. `if..else` 문은 논리적 참, 거짓으로 실행할 코드 블록을 결정하지만, `switch` 문은 **다양한 상황에 따라 실행할 코드 블록을 결정할 때 사용한다.**



**Fall Through**

`swtich`문의 표현식의 평가 결과와 일치하는 `case`로 이동하였지만, 해당 `case`를 탈출 (`break`)하지 않고, `switch`문이 끝날 때까지 모든 `case`문과 `default`문을 실행하는 현상.

```javascript
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = 'January';
  case 2:
    monthName = 'February';
	.
    .
    .
  case 11:
    monthName = 'November';
  case 12:
    monthName = 'December';
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```



하지만, `break`를 생략한 fall through가 유용한 경우도 있다. fall through 활용해 여러 개의 `case`문을 하나의 조건으로 사용할 수도 있다.

``` javascript
var year = 2000; // 2000년은 윤년으로 2월이 29일이다.
var month = 2;
var days = 0;

switch (month) {
  // FALL THROUGH
  case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    days = 31;
    break;
  // FALL THROUGH
  case 4: case 6: case 9: case 11:
    days = 30;
    break;
  case 2:
    // 윤년 계산 알고리즘
    // 1. 년도가 4로 나누어 떨어지는 해는 윤년(2000, 2004, 2008, 2012, 2016, 2020…)
    // 2. 그 중에서 년도가 100으로 나누어 떨어지는 해는 평년(2000, 2100, 2200...)
    // 3. 그 중에서 년도가 400으로 나누어 떨어지는 해는 윤년(2000, 2400, 2800...)
    days = ((year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0)) ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}

console.log(days); // 29
```



## 3. 반복문

반복문 (Loop statement)은 주어진 조건식의 평가 결과가 참인 경우 코드 블럭을 실행한다. 그 후 조건식을 다시 검사하여 여전히 참인 경우 코드 블록을 다시 실행한다. 이는 조건식이 거짓일 때까지 반복된다.

### 3.1. for 문

``` javascript
for (var i = 0; i < 2; i++) {
  console.log(i);
}
// 0 1

for (var i = 1; i <= 6; i++) {
  for (var j = 1; j <= 6; j++) {
    if (i + j === 6) console.log(`[${i}, ${j}]\n`);
  }
}
// [1, 5]
// [2, 4]
// [3, 3]
// [4, 2]
// [5, 1]
```



### 3.2. while 문

``` javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count);
  count++;
  if (count === 3) break;
}
// 0 1 2
```



### 3.3. do...while 문

코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서, 코드 블록은 무조건 한번 이상 실행된다.

``` javascript
var count = 0;

// while의 조건문이 불일치할 때까지 do 안의 코드를 실행
do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2
```



(break, label)



### 3.5. continue 문

continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 이동한다.

``` javascript
var string = 'Hello World.';
var search = 'l';
var count = 0;

// continue 문을 사용면 if 문 밖에 코드를 작성할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 카운트를 증가시키지 않는다.
  if (string[i] !== search) continue;

  count++;
  // code
  // code
  // code
}
```

