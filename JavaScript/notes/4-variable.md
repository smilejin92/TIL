# 변수

## 1. 변수란 무엇인가?

* 하나의 값을 저장할 수 있는 메모리 공간에 붙인 이름, 또는 **메모리 공간 자체**
* **할당** - 변수에 값을 저장하는 것
* **참조** - 변수에 저장된 값을 읽어 들이는 것
* 좋은 이름(식별자)의 변수는 가독성을 높여준다
* **식별자는 어떤 값을 구별하여 식별해낼 수 있는 고유한 이름**을 말한다 (주소를 가진다). 사람을 이름으로 구별하여 식별하듯 값도 식별자에 의해 구별하여 식별할 수 있다.



## 2. 변수 선언 (Variable Declaration)

* 변수를 생성하는 것
* 변수값을 저장하기 위한 메모리 영역의 확보를 명령
* `var`, `let`, `const`

``` javascript
// initialization - 값을 저장하기 위한 메모리 공간을 확보, 암묵적으로 undefined 값을 할당
// assignment - 값을 할당
var score; // initialization, undefined
score = 30; // assignment

// initialization & assignment
var result = 30;
```

* undefined (메모리는 할당되어 있지만 아직 무슨 값이 들어올지 모르겠다, not assigned) 
* null (empty value, assigned)
* 선언한 변수 이름 (식별자)은 실행 컨텍스트 (execution context)에 등록됨. **실행 컨텍스트**는 자바스크립트 엔진이 실행 가능한 코드를 평가 (evaluation)하고 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역.



## 3. 변수 선언의 실행 시점과 변수 호이스팅

``` javascript
console.log(score); // score가 선언되지도 않았는데 출력
var score; // 변수 선언
```

위의 코드에서 선언되지 않은 변수를 console.log 하려했으니 당연히 에러가 발생할 줄 알았으나, undefined가 제대로 출력됨.

위의 코드가 실행될 수 있는 이유는 모든 (변수, 함수 등) 선언이 소스 코드가 실행되는 런타임이 아니라 **그 이전 단계인 Syntax analysis 단계 (평가)**에서 먼저 실행됨. 이미 소스 코드 전체를 평가하여 모든 식별자를 등록하고 (**변수의 경우 암묵적으로 undefined 값을 할당해놓음**) 초기화하여(**variable hoisting**) 소스 코드를 한 줄씩 실행함. 모든 선언문이 코드의 선두로 끌어 올려진 것처럼 동작함. 따라서, 런타임 환경에서는 선언문을 다시 실행하지 않음.



## 5. 값의 할당

* 자바스크립트 엔진은 **변수 선언과 값의 할당을 구분하여 실행한다.** 
* 변수 (및 함수) 선언은 런타임 이전에 먼저 실행되지만, 할당은 런타임에서 순차적으로 진행됨

즉, 변수의 선언과 값의 할당을 하나의 문장으로 단축 표현해도 자바스크립트 엔진은 변수의 선언과 값의 할당을 분리해서 각각 실행한다는 의미. 따라서 변수에 `undefined`가 할당되어 초기화되는 것은 변함이 없다.

**재할당** 시 이전 메모리 공간을 overwrite하는게 아니고 새로운 메모리 셀에 값을 할당. 더이상 참조할 수 없는 값은 가비지 컬렉터에 의해 메모리에서 자동 해제되지만, 언제 해제될 지는 예측할 수 없음.



## 6. 값의 재할당

* var 키워드로 선언한 변수는 사실 선언과 동시에 `undefined`로 초기화되기 때문에 처음 값을 할당하는 것도 굳이 따지면 재할당이다.
* 재할당 할 수 없는 값을 **상수 (const)**라 부른다 (ES6). 따라서, 절대적으로 바뀌지 않는 값이 있으면 const로 선언



## 5. 식별자 네이밍 규칙

* 식별자 - 어떤 값을 구별하여 식별해낼 수 있는 이름

* 식별자는 특수문자를 제외한 문자, 숫자, underscore(_), 달러 기호 ($)를 포함할 수 있다.

  ``` javascript
  var person, $elem, _name, first_name, val1;
  ```

* 단, 식별자는 특수문자를 제외한 문자, underscore, 달러 기호로 시작해야한다. (숫자 시작 X)

* 예약어는 식별자로 사용할 수 없다 (ex. this, await, break, case, catch, class, const, continue...)

  ``` javascript
  var first-name, 1st, this;
  ```

* 변수의 존재 목적을 쉽게 이해할 수 있도록 의미를 명확히 표현

* 자주 사용되는 네이밍 컨벤션을 따른다

  ``` javascript
  // camelCase
  var firstName;
  
  // snake_case
  var first_name;
  
  // PascalCase
  var FirstName;
  
  // typeHungarianCase
  var strFirstName;
  ```

