# 프로미스 (Promise)

## 1. 프로미스란?

자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용한다. 하지만 전통적인 콜백 패턴은 가독성이 나쁘고 비동기 처리 중 발생한 **에러의 예외 처리가 곤란**하며 여러 개의 비동기 처리 로직을 한번에 처리하는 것도 한계가 있다. **ES6에서 비동기 처리를 위한 또 다른 패턴으로 프로미스 (Promise)를 도입하였다.** Promise는 전통적인 콜백 패턴이 가진 단점을 보완하며 비동기 처리 시점을 명확하게 표현한다.

키워드: 콜백 패턴, 후속 처리, 순서 보장, 예외 처리

그 외 비동기 처리 패턴

2. Axios - 파싱을 내부적으로 해준다, 크로스 브라우징
3. fetch-api
4. async / await



## 2. 콜백 패턴의 단점

### 2.1. 콜백 헬

자바스크립트의 대부분의 **DOM 이벤트**와 **Timer 함수**(setTimeout, setInterval), **Ajax 요청**은 **비동기식 처리 모델로 동작**한다. 비동기식 처리 모델은 요청을 병렬로 처리하여 다른 요청이 블로킹(blocking, 작업 중단)되지 않는 장점이 있다.

하지만 비동기 처리를 위해 콜백 패턴을 사용하면 처리 순서를 보장하기 위해 여러 개의 콜백 함수가 중첩(nesting)되어 복잡도가 높아지는 **콜백 헬(Callback Hell)**이 발생하는 단점이 있다. 콜백 헬은 가독성이 떨어지며 버그를 유발하는 원인이 된다.

```javascript
// 콜백 헬 예제
step(function(value1) {
    step2(value1, function(value2) {
        step(value2, function(value3) {
            ...
        })
    })
})
```

콜백 헬이 발생하는 이유에 대해 살펴보자. 비동기 처리 모델은 실행 완료를 기다리지 않고 즉시 다음 태스크를 실행한다. 따라서 **비동기 함수(비동기를 처리하는 함수)** 내에서 처리 결과를 반환(또는 전역 변수에의 할당)하면 기대한대로 동작하지 않는다.

```javascript
// 비동기 함수
function get(url) {
  const xhr = new XMLHttpRequest(); // XMLHttpRequest 객체 생성
    
  // 서버 응답시 오출될 이벤트 핸들러
  xhr.onreadystatechange = function () {
    // 서버 응답 완료가 아니면 무시
    if (xhr.readyState !== XMLHttpRequest.DONE) return;

    if (xhr.status === 200) { // 정상 응답
      console.log(xhr.response);
      // 비동기 함수의 결과에 대한 처리는 반환할 수 없다.
      return xhr.response; // (1)
    } else { // 비정상 응답
      console.log('Error: ' + xhr.status);
    }
  };
  xhr.open('GET', url); // 비동기 방식으로 Request 오픈
  xhr.send(); // Request 전송
}

// 비동기 함수 내의 readustatechange 이벤트 핸들러에서 처리 결과를 반환하면 순서가 보장되지 않는다.
const res = get('http://jsonplaceholder.typicode.com/posts/1');
console.log(res); // (2) undefined

```

비동기 함수 내의 `readystatechange` 이벤트 핸들러에서 처리 결과를 반환하면 (1) 순서가 보장되지 않는다. 즉, (2)에서 `get` 함수가 반환한 값을 참조할 수 없다. 그 이유에 대해 살펴보자.

* `get` 함수가 호출되면 `get` 함수의 실행 컨텍스트가 생성되고 콜 스택에 push되어 실행된다. 
* `get` 함수가 반환하는 `xhr.response`는 `readystatechange` 이벤트 핸들러가 반환한다.
* `readystatechange` 이벤트가 발생하는 시점을 명확히 알 수 없지만, **반드시 `get` 함수가 종료한 이후 발생한다.** `get` 함수의 마지막 문인 `xhr.send()`가 실행되어야 request를 전송하고, request를 전송해야 `readystatechange` 이벤트가 발생할 수 있기 때문이다.
* `get` 함수가 종료하면 곧바로 `console.log()`가 호출되어 콜 스택에 push된다.
* `console.log()`보다 `readystatechange` 이벤트가 먼저 발생했더라도, 태스크 큐로 이동하여 콜스택이 비어질 때까지 대기한다.
* `console.log()` 호출이 종료되면 이벤트 루프에 의해 태스크큐에 있던 이벤트 핸들러가 콜스택으로 push되어 실행된다.

따라서 `get` 함수의 반환 결과를 가지고 후속 처리를 할 수 없다. **비동기로 사용되는 모든 함수에 이와 같은 문제가 발생한다.** 비동기 함수의 처리 결과를 반환하는 경우, 순서가 보장되지 않기 때문에 그 반환 결과를 가지고 **후속 처리를 할 수 없다**. 비동기 함수의 처리 결과에 대한 처리는 비동기 함수의 콜백 함수 내에서 처리해야 한다. 이로 인해 **콜백 헬이 발생한다.**



### 2.2. 에러 처리의 한계

콜백 방식의 비동기 처리가 갖는 문제점 중에서 가장 심각한 것은 에러 처리가 곤란하다는 것이다.

```javascript
try {
    setTimeout(() => {
        throw new Error('Error!');
    }, 1000);
} catch (e) {
    console.log('에러를 캐치하지 못한다..')
    console.log(e);
}
```

`try` 블록 내에서 `setTimeout` 함수가 실행되면 1초 후에 콜백 함수가 실행되고 이 콜백 함수는 예외를 발생시킨다. 하지만 이 예외는 `catch` 블록에서 캐치되지 않는다.

* 비동기 처리 함수의 콜백 함수는 해당 이벤트(ex. timer 함수의 tick 이벤트, XMLHttpRequest의 readystatechange 이벤트 등)가 발생하면 태스크 큐(Task queue)로 이동한 후 콜 스택이 비어졌을 때 콜 스택으로 push되어 실행된다.
* `setTimeout` 함수는 비동기 함수이므로 콜백 함수가 실행될 때까지 기다리지 않고 즉시 종료되어 콜 스택에서 제거된다.
* 이후 tick 이벤트가 발생하면 `setTimeout` 함수의 콜백 함수는 태스크 큐로 이동하여 콜 스택이 비어질 때까지 대기한다.
* `setTimeout` 호출이 종료되어 (콜 스택이 비어진다) `setTimeout` 함수의 콜백함수가 콜 스택으로 push되어 실행된다 (이미 try/catch 문에서 나온 상태이다). 이러한 현상이 발생할 수 있는건, `setTimeout` 의 콜백 함수를 호출한 호출자(caller)가 `setTimeout` 함수가 아니란 뜻이다. 만약 `setTimeout` 함수가 `setTimeout` 함수의 **콜백을 호출한 주체라면 콜스택에 남아있어야 한다.**
* 예외(exception)는 호출자(caller) 방향으로 전파된다. 하지만 `setTimeout` 함수의 콜백 함수를 호출한 것은 `setTimeout` 함수가 아니므로, `setTimeout` 함수의 콜백 함수 내에서 발생시킨 에러는 `catch` 블록에서 잡히지 않으며 그대로 종료된다.

이러한 문제를 극복하기 위해 Promise가 제안되었다. **IE를 제외한** 대부분의 브라우저가 지원하고 있다.



## 3. 프로미스의 생성

프로미스는 **Promise 생성자 함수를 통해 인스턴스화한다.** Promise 생성자 함수는 **비동기 작업을 수행할 콜백 함수를 인자로 전달받는데**, 이 콜백 함수는 **resolve와 reject 함수**를 인자로 전달받는다.

```javascript
// Promise 객체의 생성
const promise = new Promise((resolve, reject) => {
  // 비동기 작업을 수행한다.
  if (/* 비동기 작업 수행 성공 */) {
    resolve('result');
  } else { /* 비동기 작업 수행 실패 */
    reject('failure reason');
  }
});

```

Promise는 비동기 처리가 성공(fulfilled)하였는지 실패(rejected)하였는지 등의 상태 정보를 갖는다.

| 상태          | 의미                                       | 구현                                               |
| ------------- | ------------------------------------------ | -------------------------------------------------- |
| pending       | 비동기 처리가 아직 수행되지 않은 상태      | resolve 또는 reject 함수가 아직 호출되지 않은 상태 |
| **fulfilled** | 비동기 처리가 수행된 상태 (성공)           | resolve 함수가 호출된 상태                         |
| **rejected**  | 비동기 처리가 수행된 상태 (실패)           | reject 함수가 호출된 상태                          |
| settled       | 비동기 처리가 수행된 상태 (성공 또는 실패) | resolve 또는 reject 함수가 호출된 상태             |

* Promise 생성자 함수가 인자로 전달받은 콜백 함수 내부에서 비동기 처리 작업을 수행한다.
* 비동기 처리가 성공하면 resolve 함수를 호출한다. 이때 프로미스는 `fulfilled` 상태가 된다.
* 비동기 처리가 실패하면 reject 함수를 호출한다. 이때 프로미스는 `rejected` 상태가 된다.

```javascript
const promiseAjax = (method, url, payload) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open(method, url);
    xhr.setRequestHeader('Content-type', 'application/json');
    xhr.send(JSON.stringify(payload));

    xhr.onreadystatechange = function () {
      // 서버 응답 완료가 아니면 무시
      if (xhr.readyState !== XMLHttpRequest.DONE) return;

      if (xhr.readyState >= 200 && xhr.status < 400) {
        resolve(xhr.response); // Success!
      } else {
        // reject 메소드를 호출하면서 에러 메시지를 전달
        reject(new Error(xhr.status)); // Failed..
      }
    };
  });
};

```

위 예제처럼 **비동기 함수 내에서 Promise 객체를 생성하고 그 내부에서 비동기 처리를 구현한다.** 

1. Promise 객체 생성, 내부에서 비동기 처리를 구현
2. 비동기 처리 성공/실패 시 `resolve` /`reject`메소드 호출, **인자로 비동기 처리 결과를 전달**
3. 2에서 `resolve`/`reject` 메소드의 인자로 전달한 처리 결과는 Promise 객체의 **후속 처리 메소드로 전달**



## 4. 프로미스의 후속 처리 메소드

* Promise로 구현된 비동기 함수는 **Promise 객체를 반환하여야 한다.**
* Promise로 구현된 비동기 함수(`promiseAjax`)를 호출하는 측(promise consumer)에서는 Promise 객체의 후속 처리 메소드(`then`, `catch`)를 통해 비동기 처리 결과 또는 에러 메시지를 전달받아 처리한다.
* Promise 객체는 상태(fulfilled, rejected 등)를 갖는다. 이 상태에 따라 후속 처리 메소드를 체이닝 방식으로 호출한다. Promise의 **후속 처리 메소드는 아래와 같다.**

#### `then`

* 두 개의 콜백 함수를 인자로 전달 받는다.
* 첫 번째 콜백 함수는 성공(fulfilled, resolve 함수가 호출된 상태)시 호출된다.
* 두 번째 콜백 함수는 실패(rejected, reject 함수가 호출된 상태)시 호출된다.
* **`Promise`를 반환한다.**

#### `catch`

* 예외(비동기 처리에서 발생한 에러와 `then` 메소드에서 발생한 에러)가 발생하면 호출된다.
* `Promise`를 반환한다.



```javascript
const promiseAjax = (method, url, payload) => {
  // promise는 객체
  // new Promise는 객체를 만들어내는 생성자 함수
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open(method, url);
    xhr.setRequestHeader('Content-type', 'application/json');
    xhr.send(JSON.stringify(payload));

    xhr.onreadystatechange = function (e) {
      if (xhr.readyState !== XMLHttpRequest.DONE) return;
	  
      // 성공시 resolve 함수에 원하는 값을 전달
      // 실패시 reject 함수에 error를 전달
      if (xhr.status === 200) {
        resolve(JSON.parse(xhr.responseText));
      } else {
        reject(new Error(xhr.status));
      }
    };
  });
};

// .then/.catch는 promise의 후속처리 함수
// .then은 resolve를 호출
// .catch는 reject를 호출
// .then/.catch는 Promise를 return한다.
// 앞에 있는 프로미스 인스턴스의 처리가 성공하면 .then이 호출된다
promiseAjax('GET', '/todos')
  .then(res => todos = res)
  .then(render, console.error); // 위의 .then이 성공하면(todos에 res가 할당되면), render 함수를 실행, 실패하면 console.error를 실행
```



## 5. 프로미스의 에러 처리

위 예제의 비동기 함수 `promiseAjax`는 Promise 객체를 반환한다. Promise 객체의 후속 처리 메소드를 사용하여 비동기 처리 결과에 대한 후속 처리를 수행한다. 비동기 처리 시 발생한 에러 메시지는 `then` 메소드의 두 번째 콜백 함수로 전달된다. Promise 객체의 후속 처리 메소드 `catch`를 사용하여도 에러를 처리할 수 있다.

```javascript
promiseAjax('GET', '/todos')
  .then(res => todos = res)
  .then(render)
  .catch(console.error);// 위의 후속 처리 메소드.then 중 어느 하나가 에러를 발생하면 catch한다.
```

`catch` 메소드는 에러를 처리한다는 점에서 `then` 메소드의 두 번째 콜백 함수와 유사하지만 미요한 차이가 있다. `then` 메소드의 두 번째 함수는 **비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)만을 캐치한다.** 하지만 `catch` 메소드는 비동기 처리에서 발생한 에러 뿐만 아니라 **`then` 메소드 내부에서 발생한 에러도 캐치한다.** 따라서 에러 처리는 `catch` 메소드를 사용하는 편이 보다 효율적이다.



## 6. 프로미스 체이닝

비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 참수는 호출이 중첩(nested)되어 복잡도가 높아지는 콜백 헬이 발생한다. 프로미스는 **후소 처리 메소드를 체이닝(chaining)하여 여러 개의 프로미스를 연결해 사용할 수 있다.** 이로써 콜백 헬을 해결한다.

Promise 객체를 반환한 비동기 함수는 프로미스 후속 처리 메소드인 `then` 혹은 `catch` 메소드를 사용할 수 있다. 따라서, `then` 메소드가 Promise 객체를 반환하도록 하면 여러 개의 프로미스를 연결하여 사용할 수 있다 (`then` 메소드는 기본적으로 Promise를 반환한다).

```javascript
promiseAjax('GET', url)
  .then(JSON.parse)
  .then(res => todos = res)
  .then(render)
  .catch(console.error);
```



## 7. 프로미스의 정적 메소드

### 7.1 Promise.resolve / Promise.reject

`Promise.resolve`와 `Promise.reject` 메소드는 존재하는 값을 Promise로 래핑하기 위해 사용한다.

정적 메소드 `Promise.resolve` 메소드는 인자로 전달된 값을 resolve하는 Promise를 생성한다.

```javascript
const resolvedPromise = Promise.resolve([1, 2, 3]);
resolvedPromise.then(console.log); // 질문. console.log의 인수로 어떻게 저 배열이 들어가는지??
// resolvedPromise.then(res => console.log(res));

// 위 예제는 아래 예제와 동일하게 동작한다.
const resolvePromise = new Promise(resolve => resolve([1, 2, 3]));
resolvedPromise.then(console.log); // [1, 2, 3]
```

`Promise.reject` 메소드는 인자로 전달된 값을 reject하는 프로미스를 생성한다.

```javascript
const rejectedPromise = Promise.reject(new Error('Error!'));
rejectedPromise.catch(console.log); // Error: Error!

// 위 예제는 아래 예제와 동일하게 동작한다.
const rejectedPromise = new Promise((resolve, reject) => reject(new Error('Error!')));
rejectedPromise.catch(console.log); // Error: Error!
```



### 7.2 Promise.all

### 7.3 Promise.race

