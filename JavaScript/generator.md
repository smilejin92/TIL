# 제너레이터와 async/await

## 1. 제너레이터란?

ES6에서 도입된 제너레이터(generator)는 코드 블록의 실행을 일시 중지했다가 필요한 시점에 재개할 수 있는 특수한 함수이다. 제너레이터와 일반 함수는 다음과 같은 차이가 있다.

&nbsp;  

**1. 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다.**

일반 함수를 호출하면 제어권이 함수에게 넘어가고 함수 코드를 일괄 실행한다. 즉, 함수 호출자(caller)는 함수를 호출한 이후 함수의 실행을 제어할 수 없다. 제너레이터 함수는 함수의 실행을 함수 호출자가 제어할 수 있다. 다시 말해, 함수 호출자가 함수의 실행을 일시 중지시키거나 재개시킬 수 있다. 이는 **함수의 제어권을 함수가 독점하는 것이 아니라 함수 호출자에게 양도(yield)할 수 있다**는 것을 의미한다.

&nbsp;  

**2. 제너레이터 함수는 함수 호출자와 함수의 상태를 주고 받을 수 있다.**

일반 함수를 호출하면 매개변수를 통해 함수 외부에서 값을 주입받고 함수 코드를 일괄 실행하여 결과값을 함수 외부로 반환한다. 즉, 함수가 실행되고 있는 동안에는 함수 외부에서 함수 내부로 값을 전달하여 함수의 상태를 변경할 수 없다. 반면 제너레이터 함수는 함수 호출자와 양방향으로 함수의 상태를 주고 받을 수 있다. 다시 말해, **제너레이터 함수는 함수 호출자에게 상태를 전달할 수 있고, 함수 호출자로부터 상태를 전달받을 수도 있다.**

&nbsp;  

**3. 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.**

일반 함수를 호출하면 함수 코드를 일괄 실행하고 값을 반환한다. **제너레이터 함수를 호출하면 함수 코드를 실행하는 것이 아니라 제너레이터 객체를 반환한다.**

&nbsp;  

## 2. 제너레이터 함수의 정의

제너레이터 함수는 `function*` 키워드로 선언한다. 그리고 **하나 이상의 `yield` 표현식을 포함한다.** 이것을 제외하면 일반 함수를 정의하는 방법과 같다.

```javascript
// 제너레이터 함수 선언문
function* genDecFunc() {
  yield 1;
}

// 제너레이터 함수 표현식
const genExpFunc = function* () {
  yield 1;
};

// 제너레이터 메소드
const obj = {
  * genObjMethod() {
    yield 1;
  }
};

// 제너레이터 클래스 메소드
class MyClass {
  * genClsMethod() {
    yield 1;
  }
}
```

&nbsp;  

애스터리스크(`*`)의 위치는 `function` 키워드와 함수 이름 사이라면 어디든지 상관없다. 다음 예제의 제너레이터 함수는 모두 유효하다. 하지만 일관성을 유지하기 위해 `function` 키워드 바로 뒤에 붙이는 것을 권장한다.

```javascript
function* genFunc() { yield 1; } // 권장

function * genFunc() { yield 1; }

function *genFunc() { yield 1; }

function*genFunc() { yield 1; }
```

&nbsp;  

제너레이터 함수는 화살표 함수로 정의할 수 없다.

```javascript
const genArrowFunc = * () => {
  yield 1;
};
// SyntaxError: Unexpected token '*'
```

&nbsp;  

제너레이터 함수는 `new` 연산자와 함께 생성자 함수로 호출할 수 없다.

```javascript
function* genFunc() {
  yield 1;
}

new genFunc(); // TypeError: genFunc is not a constructor
```

&nbsp;  

## 3. 제너레이터 객체

**제너레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라, 제너레이터 객체를 생성해 반환한다. 제너레이터 함수가 반환한 제너레이터 객체는 이터러블(iterable)이면서 동시에 이터레이터(iterator)다.** 다시 말해, 제너레이터 객체는 `Symbol.iterator` 메소드를 상속 받는 이터러블이면서 `value`, `done` 프로퍼티를 갖는 이터레이터 리절트 객체를 반환하는 `next` 메소드를 소유하는 이터레이터다.

```javascript
// 제너레이터 함수
function* genFunc() {
  yield 1;
  yield 2;
  yield 3;
}

// 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.
const generator = genFunc();

// 제너레이터 객체는 이터러블(iterable)이면서 동시에 이터레이터(iterator)다.
// 이터러블은 Symbol.iterator 메소드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 객체다.
console.log(Symbol.iterator in generator); // true

// 이터레이터는 next 메소드를 갖는다.
console.log('next' in generator); // true
```

&nbsp;  

## 4. 제너레이터의 일시 중지와 재개

제너레이터는 `next` 메소드와 `yield` 키워드를 통해 실행을 일시 중지했다가 필요한 시점에 다시 재개할 수 있다. 일반 함수는 호출 이후 제어권을 함수가 독점하지만 제너레이터는 함수 호출자에게 제어권을 양도(yield)하여 필요한 시점에 함수 실행을 재개할 수 있다.

제너레이터 객체의 `next` 메소드를 호출하면 제너레이터 함수의 코드 블록을 실행한다. 단, 일반 함수처럼 한 번에 코드 블록의 모든 코드를 실행하는 것이 아니라, `yield` 표현식까지만 실행한다. **`yield` 키워드는 제너레이터 함수의 실행을 일시 중지시키거나 `yield` 키워드 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 반환한다.**

```javascript
// 제너레이터 함수
function* genFunc() {
  yield 1;
  yield 2;
  yield 3;
}

// 제너레이터 객체
const generator = genFunc();

// 처음 next 메소드를 호출하면 첫 번째 yield 표현식까지 실행되고 일시 중지된다.
// next 메소드는 이터레이터 리절트 객체({ value, done })를 반환한다.
// value 프로퍼티에는 첫 번째 yield 표현식에서 yield된 값 1이 할당된다.
// done 프로퍼티에는 제너레이터 함수가 끝까지 실행되었는지를 나타내는 false가 할당된다.
console.log(generator.next()); // { value: 1, done: false }

console.log(generator.next()); // { value: 2, done: false }

console.log(generator.next()); // { value: 3, done: false };

// 마지막 next 메소드를 호출하면 남은 yield 표현식이 없으므로 제너레이터 함수의 마지막까지 실행한다.
// 이때 next 메소드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에는 제너레이터 함수의 반환값 undefined가 할당된다.
// done 프로퍼티에는 제너레이터 함수가 끝까지 실행되었음을 나타내는 true가 할당된다.
console.log(generator.next()); // { value: undefined, done: true }
```

**제너레이터 객체의 `next` 메소드를 호출하면 `yield` 표현식까지 실행되고 일시 중지(suspend)된다. 이때 함수의 제어권이 호출자에게 양도된다.** 이후 필요한 시점에 호출자가 또 다시 `next` 메소드를 호출하면 일시 중지된 코드부터 실행을 재개(resume)하기 시작하여 다음 `yield` 표현식까지 실행되고 또 다시 일시 중지된다.

**이때 제너레이터 객체의 `next` 메소드는 `value`, `done` 프로퍼티를 가지는 이터레이터 리절트 객체를 반환한다. `next` 메소드가 반환한 이터레이터 객체의 `value` 프로퍼티에는 `yield` 표현식에서 yield된 값(yield 키워드 뒤의 값)이 할당되고 `done` 프로퍼티에는 제너레이터 함수가 끝까지 실행되었는지를 나타내는 불리언 값이 할당된다.**

이처럼 `next` 메소드를 반복 호출하여 yield 표현식까지 실행과 일시 중지를 반복하다가, 제너레이터 함수가 끝까지 실행되면 `next` 메소드가 반환하는 이터레이터 객체의 `value` 프로퍼티에는 제너레이터 함수의 반환값이 할당되고 `done` 프로퍼티에는 제너레이터 함수가 끝까지 실행되었음을 나타내는 false가 할당된다.

```pseudocode
generator.next() -> yield -> generator.next() -> yield -> ... -> generator.next() -> return
```

&nbsp;  

이터레이터의 `next` 메소드와는 달리 제너레이터 객체의 `next` 메소드에는 인수를 전달할 수 있다. **제너레이터 객체의 `next` 메소드에 전달한 인수는 제너레이터 함수의 yield 표현식을 할당받는 변수에 할당된다.** yield 표현식을 할당받는 변수에 yield 표현식의 평가 결과가 할당되지 않는 것에 주의해야 한다.

```javascript
function* genFunc() {
  // 처음 next 메소드를 호출하면 첫 번째 yield 표현식까지 실행되고 일시 중지된다.
  // 이때 yield된 값 1은 next 메소드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당된다.
  // x 변수에는 아직 아무것도 할당되지 않았다. x 변수의 값은 next 메소드가 두 번째 호출될 때 결정된다.
  const x = yield 1;
  
  // 두 번째 next 메소드를 호출할 때 전달한 인수 10은 첫 번째 yield 표현식을 할당받는 x에 할당된다.
  // 즉, const x = yield 1;은 두 번째 next 메소드를 호출했을 때 완료된다.
  // 두 번째 next 메소드를 호출하면 두 번째 yield 표현식까지 실행되고 일시 중지된다.
  // 이때 yield된 값 x + 10은 next 메소드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당된다.
  const y = yield (x + 10);
  
  // 세 번째 next 메소드를 호출할 때 전달한 인수 20은 두 번째 yield 표현식을 할당받는 y에 할당된다.
  // 즉, const y = yield (x + 10);은 세 번째 next 메소드를 호출했을 때 완료된다.
  // 세 번째 next 메소드를 호출하면 함수 끝까지 실행된다.
  // 이때 제너레이터 함수의 반환 값 x + y는 next 메소드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당된다.
  // 일반적으로 제너레이터의 반환값은 의미가 없다.
  // 따라서 제너레이터에서는 값을 반환할 필요가 없고 return은 종료의 의미로만 사용해야 한다.
  return x + y;
}

// 제너레이터 객체
const generator = genFunc();

// 처음 호출하는 next 메소드에는 인수를 전달하지 않는다.
// 만약 처음 호출하는 next 메소드에 인수를 전달하면 무시된다.
let res = generator.next();
console.log(res); // { value: 1, done: false }

// next 메소드에 인수로 전달한 10은 genFunc 함수의 x 변수에 할당된다.
// next 메소드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에는 두 번째 yield된 값 20이 할당된다.
res = generator.next(10);
console.log(res); // { value: 20, done: false }

// next 메소드에 인수로 전달한 20은 genFunc 함수의 y변수에 할당된다.
// next 메소드가 반환한 이터레이터 객체의 value 프로퍼티에는 제너레이터 함수의 반환 값 30이 할당된다.
res = generator.next(20);
console.log(res); // { value: 30, done: true }
```

이처럼 제너레이터 함수는 `next` 메소드와 `yield` 표현식을 통해 함수 호출자와 함수의 상태를 주고 받을 수 있다. 함수 호출자는 `next` 메소드를 통해 `yield` 표현식까지 함수를 실행시켜 제너레이터 객체가 관리하는 상태(yield된 값)를 꺼내올 수 있고, `next` 메소드에 인수를 전달해서 제너레이터 객체에 상태(yield 표현식을 할당받는 변수)를 밀어 넣을 수 있다. 이러한 제너레이터의 특징을 활용하면 비동기 태스크를 동기적으로 수행할 수 있다.

&nbsp;  

## 5. 제너레이터의 활용

### 5.1. 이터러블의 구현

제너레이터 함수를 사용하면 이터레이션 프로토콜을 준수하여 이터러블을 생성하는 것보다 간단히 이터러블을 구현할 수 있다. 먼저 이터레이션 프로토콜을 준수하여 무한 피보나치 수열을 생성하는 함수를 구현해 보자.

```javascript
const infiniteFibonacci = (function () {
  let [pre, cur] = [0, 1];
  
  return {
    [Symbol.iterator]() {
      return this;
    },
    next() {
      [pre, cur] = [cur, pre + cur];
      return { value: cur };
    }
  };
}());

// infiniteFibonacci는 무한 이터러블이다.
for (cont num of infiniteFibonacci) {
  if (num > 10000) break;
  console.log(num); // 1 2 3 5 8 ...
}
```

&nbsp;  

이번에는 제너레이터를 사용하여 무한 피보나치 수열을 생성하는 함수를 구현해 보자. 제너레이터 함수를 사용하면 이터레이션 프로토콜을 준수하여 이터러블을 생성하는 것보다 간단히 이터러블을 구현할 수 있다.

```javascript
const infiniteFibonacci = (function* () {
  let [pre, cur] = [0, 1];
  
  while (true) {
    [pre, cur] = [cur, pre + cur];
    yield cur;
  }
}());

for (const num of infiniteFibonacci) {
  if (num > 10000) break;
  console.log(num); // 1 2 3 5 8 ...
}
```

&nbsp;  

### 5.2. 비동기 처리

제너레이터 함수는 `next` 메소드와 `yield` 표현식을 통해 함수 호출자와 함수의 상태를 주고 받을 수 있다. 이러한 특징을 활용하면 프로미스를 사용한 비동기 처리를 동기 처리처럼 구현할 수 있다. 다시 말해, 프로미스의 후속 처리 메소드 `then` / `catch` / `finally` 없이 비동기 처리 결과를 반환하도록 구현할 수 있다.

```javascript
const async = genFunc => {
  const generator = genFunc(); // 2
  
  const onResolved = arg => {
  	const result = generator.next(arg); // 5
    return result.done
    	? result.value
    	: result.value.then(pValue => onResolved(pValue)); // 7
  };
  
  return onResolved; // 3
};

(async(function* fetchTodo() { // 1
  const url = 'https://jsonplaceholder.typicode.com/todos/1';

  const response = yield fetch(url); // 6
  const todo = yield response.json(); // 8
  console.log(todo);
  // {userId: 1, id: 1, title: 'delectus aut autem', completed: false}
})());
```

1. `async` 함수가 호출(1)되면 인수로 전달받은 제너레이터 함수 `fetchTodo`를 호출하여 제너레이터 객체를 생성(2)하고 `onResolved` 함수를 반환(3)한다.
2. `next` 메소드가 처음 호출(5)되면 첫 번째 `yield` 문(6)까지 실행된다. 이때 `next` 메소드가 반환한 이터레이터 리절트 객체(`result`)의 `done` 프로퍼티의 값은 false이며, `value` 프로퍼티의 값은 6에서 yield된 (fetch 함수가 반환한) 프로미스 객체이다.  `result.done`이 false이므로 `result.value`가 resolve한 Response 객체를 `onResolved` 함수에 인수로 전달하며 재귀 호출(7)한다.
3. `onResolved` 함수에 인수로 전달된 Response 객체를 `next` 메소드에 인수로 전달하며 `next` 메소드를 두 번째 호출(5)한다. 이때 `next` 메소드에 인수로 전달한 Response 객체는 제너레이터 함수 `fetchTodo`의 `response` 변수(6)에 할당되고, 두 번째 `yield` 문(8)까지 실행된다.
4. 두 번째 `next` 메소드가 반환한 이터레이터 리절트 객체(`result`)의 `done` 프로퍼티 값은 false이며, `value` 프로퍼티의 값은 8에서 yield된 (`response.json()`가 반환한) 프로미스 객체이다. `result.done`이 false이므로 `result.value`가 resolve한 `todo` 객체를 `onResolved` 함수에 인수로 전달하며 재귀호출(7)한다.
5. `onResolved` 함수에 인수로 전달된 todo 객체를 `next` 메소드에 인수로 전달하며 `next` 메소드를 세 번째 호출(5)한다. 이때 `next` 메소드에 인수로 전달한 todo 객체는 제너레이터 함수 `fetchTodo`의 `todo` 변수(8)에 할당되고, 제너레이터 함수의 끝까지 실행된다.
6. 세 번째 `next` 메소드가 반환한 이터레이터 리절트 객체(`result`)의 `done` 프로퍼티 값은 true이며, `value` 프로퍼티의 값은 제네레이터 함수 `fetchTodo`의 반환값인 undefined이다. `result.done`이 true이므로 `result.value`를 그대로 반환한다 (재귀 끝).

&nbsp;  

위 예제의 제너레이터 함수를 실행하는 **제너레이터 실행기**인 `async` 함수는 이해를 돕기 위해 간략화한 예제이므로 완전하지 않다. 다음에 설명할 async / await를 사용하면 `async` 함수와 같은 제너레이터 실행기를 사용할 필요가 없지만, 만약 제너레이터 실행기가 필요하다면 [co](https://github.com/tj/co)를 사용하기 바란다.

```javascript
const fetch = require('node-fetch');
// https://github.com/tj/co
const co = require('co');

co(function* fetchTodo() {
  const url = 'https://jsonplaceholder.typicode.com/todos/1';

  const response = yield fetch(url);
  const todo = yield response.json();
  console.log(todo);
  // { userId: 1, id: 1, title: 'delectus aut autem', completed: false }
});
```

&nbsp;  

## 6. async / await

제너레이터를 사용해서 비동기 처리를 동기 처리처럼 구현하긴 했지만, 코드가 무척이나 장황해지고 가독성이 떨어진다. ES8에서는 제너레이터보다 간단하고 가독성 좋게 **비동기 처리를 동기 처리처럼 구현할 수 있는 async / await가 도입되었다.**

async / await을 사용하면 프로미스의 then / catch / finally 후속 처리 메소드에 콜백 함수를 전달하여 비동기 처리 결과를 후속 처리할 필요 없이, 마치 동기 처리처럼 프로미스를 사용할 수 있다. 다시 말해, 프로미스의 후속 처리 메소드 없이 동기 처리처럼 프로미스가 처리 결과를 반환하도록 구현할 수 있다. 위 예제를 async / await로 다시 구현해 보자.

```javascript
async function fetchTodo() {
  const url = 'https://jsonplaceholder.typicode.com/todos/1';
  
  const response = await fetch(url);
  const todo = await response.json();
  console.log(todo);
  // {userId: 1, id: 1, title: 'delectus aut autem', completed: false}
}

fetchTodo();
```

&nbsp;  

### 6.1. async 함수

`await` 키워드는 반드시 async 함수 내부에서 사용해야 한다. async 함수는 `async` 키워드를 사용해 정의하며, **언제나 프로미스를 반환한다.** async 함수가 명시적으로 프로미스를 반환하지 않더라도, async 함수의 반환값을 프로미스로 래핑하여 반환한다.

```javascript
// async 함수 선언문
async function foo(n) { return n; }
foo(1); // Promise {<resolved>: 1}

// async 함수 표현식
const bar = async function () {};
bar(); // Promise {<resolved>: undefined}

// async 화살표 함수
const baz = async n => Promise.resolve(n * n);
baz(3); // Promise {<resolved>: 9}

// async 메소드
const obj = {
  async foo(n) { return n; }
}
obj.foo(4); // Promise {<resolved>: 4}

// async 클래스 메소드
class MyClass {
  async bar(n) { return n; }
}
const myClass = new MyClass();
myClass.bar(5); // Promise {<resolved>: 5}
```

&nbsp;  

### 6.2. await 키워드

`await` 키워드는 프로미스가 settled된 상태(비동기 처리가 수행된 상태)가 될 때까지 대기하다가, 프로미스가 settled 상태가 되면 resolve된 처리 결과 또는 reject된 에러를 반환한다.

```javascript
const getGithubUserName = async id => {
  const res = await fetch(`https://api.github.com/users/${id}`); // 1
  const { name } = await res.json(); // 2
  console.log(name); // Jinhyun Kim
};

getGithubUserName('smilejin92');
```

await 키워드는 프로미스가 settled 상태가 될 때까지 대기한다고 했다. 따라서 1의 fetch 함수가 수행한 HTTP 요청에 대한 서버의 응답이 도착해서 fetch 함수가 반환한 프로미스가 settled 상태가 될 때까지 1에서 대기하게 된다. 이후 프로미스가 settled 상태가 되면 프로미스의 resolve된 처리 결과가 `res` 변수에 할당된다.























