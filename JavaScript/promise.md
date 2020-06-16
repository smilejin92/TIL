# 프로미스

## 1. 비동기 처리를 위한 콜백 패턴의 단점

### 1.1. 콜백 헬

**비동기 함수의 처리 결과(서버의 응답 등)에 대한 후속 처리는 비동기 함수에게 콜백 함수를 전달해서 수행해야 한다.** 아래 예제를 살펴보자.

```javascript
// GET 요청을 위한 비동기 함수
const get = url => {
  const xhr = new XMLHttpRequest();
	xhr.open('GET', url);
	xhr.send();
  
  xhr.onload = () => {
    if (xhr.status === 200) {
      // 서버의 응답 결과를 반환한다.
      return JSON.parse(xhr.response);
    } else {
      return new Error(`${xhr.status} ${xhr.statusText}`);
    }
  };
};

// jsonplaceholder는 Fast REST API를 제공하는 서비스다.
// id가 1인 post를 취득
const post = get('https://jsonplaceholder.typicode.com/posts/1');
console.log(post); // undefined
```

GET 요청을 위한 `get` 함수는 비동기 함수이다. 따라서 비동기 함수 내에서 서버의 응답 결과를 반환하거나 상위 스코프의 변수에 할당하면 기대한 대로 동작하지 않는다.

`xhr.onload` 이벤트 핸들러 프로퍼티에 바인딩한 이벤트 핸들러의 반환문은 `get` 함수의 반환문이 아니다. 만약 `xhr.onload` 이벤트 핸들러를 `get` 함수가 호출할 수 있다면 이벤트 핸들러의 반환값을 `get` 함수가 다시 반환할 수 있겠지만 그럴 수 없다. 따라서 `xhr.onload` 이벤트 핸들러의 반환값은 캐치할 수 없으며, `get` 함수는 그저 undefined를 반환할 뿐이다.

이러한 상황이 발생하는 이유는 `xhr.onload` 이벤트 핸들러는 비동기적으로 실행되기 때문에 서버의 응답을 반환하거나 상위 스코프의 변수에 할당하여도 그 순서가 보장되지 않기 때문이다.

1. get 호출 
   1. xhr 인스턴스 생성 및 요청 초기화
   2. 요청 전송
   3. xhr.onload 이벤트 핸들러 바인딩
   4. return문이 생략되어 undefined를 반환
2. post 변수에 undefined를 할당
3. console.log(post);
4. 콜스택이 비어졌으므로 이벤트 핸들러는 이벤트 루프에 의해  콜스택에 푸시되어 실행

&nbsp;  

> 이벤트 핸들러도 함수이므로 이벤트 핸들러의 평가 -> 이벤트 핸들러의 실행 컨택스트 생성 -> 콜스택에 푸시 -> 이벤트 핸들러의 실행 단계를 거친다.

&nbsp;  

만약 console.log가 호출되기 직전에 load 이벤트가 발생하더라도 xhr.onload 이벤트 핸들러 프로퍼티에 바인딩한 이벤트 핸들러는 결코 console.log보다 먼저 실행되지 않는다. 따라서 `xhr.onload` 이벤트 핸들러 프로퍼티에 바인딩한 이벤트 핸들러가 실행되는 시점에는 콜 스택이 빈 상태이므로 console.log는 이미 종료된 이후이다. 이처럼 비동기 함수인 get이 취득한 서버의 응답 결과는 반환할 수 없고, 상위 스코프의 변수에 할당할 수도 없다.

&nbsp;  

이러한 문제를 해결하기 위해 **비동기 함수에게 콜백 함수를 전달하여 비동기 함수의 처리 결과에 대한 후속 처리를 수행하는 콜백 패턴이 등장했다.** 비동기 함수에 전달한 콜백 함수는 비동기 처리가 미래에 완료되면 호출되도록 구현해서 비동기 함수의 처리 결과를 가지고 처리해야 할 모든 일을 콜백 함수 내부에서 수행한다. 필요에 따라 성공 시 호출될 콜백과 실패 시 호출될 콜백을 전달할 수 있다.

```javascript
// GET 요청을 위한 비동기 함수
const get = (url, onSuccess, onFailure) => {
  const xhr = new XMLHttpRequest();
	xhr.open('GET', url);
	xhr.send();
  
  xhr.onload = () => {
    if (xhr.status === 200) {
      // 서버의 응답을 콜백 함수에 인수로 전달하면서 호출하여 응답에 대한 후속 처리를 한다.
      onSuccess(JSON.parse(xhr.response));
    } else {
      // 에러 정보를 콜백 함수에 인수로 전달하면서 호출하여 에러 처리를 한다.
      onFailure(xhr.status);
    }
  };
};

// id가 1인 post를 취득
// 서버의 응답에 대한 후속 처리를 위해 콜백 함수를 비동기 함수인 get에 전달한다.
get('https://jsonplaceholder.typicode.com/posts/1', console.log, console.error);
/*
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere ...",
  "body": "quia et suscipit ..."
}
*/
```

&nbsp;  

만약 비동기 함수의 처리 결과를 가지고 또 다른 비동기 함수를 호출해야 한다면, 함수 호출이 중첩되어 복잡도가 높아지는 현상이 발생하는데 이를 <strong>콜백 헬(callback hell)</strong>이라 한다. 다음 예제를 살펴보자.

```javascript
const url = 'https://jsonplaceholder.typicode.com';

// 1. id가 1인 post의 userId를 취득
get(`${url}/posts/1`, ({ userId }) => {
  console.log(userId); // 1

  // 2. userId를 사용하여 user 정보를 취득
  get(`${url}/users/${userId}`, userInfo => {
    console.log(userInfo); // // {id: 1, name: "Leanne Graham", username: "Bret",...}
  }, console.error);
}, console.error);
```

위 예제를 살펴보면 GET 요청을 통해 서버로부터 응답(id가 1인 post)을 취득하고 이 데이터를 사용하여 또 다른 GET 요청을 한다. 이와 같이 작성된 이유는 태스크를 순차적으로 실행하기 위함이지만, 가독성을 나쁘게 하며 실수를 유발하는 원인이 된다.

&nbsp;  

### 1.2. 에러 처리의 한계

**비동기 처리를 위한 콜백 패턴의 문제점 중 가장 심각한 것은 에러 처리가 곤란하다는 것이다.** 다음 예제를 살펴보자.

```javascript
try {
  setTimeout(() => { throw new Error('Error'); }, 1000);
} catch (e) {
  // 에러를 캐치하지 못한다.
  console.error('캐리한 에러', e);
}
```

try 블록 내에서 호출한 setTimeout 함수는 1초 후 콜백 함수를 실행시키고, 이 콜백 함수는 에러를 throw한다. 하지만 이 에러는 catch 블록에서 잡을 수 없다. 그 이유는 아래와 같다.

* setTimeout이 호출되면 setTimeout 함수의 실행 컨텍스트가 생성되어 콜 스택에 푸시되고 실행된다.
* setTimeout은 비동기 함수이므로 콜백 함수가 호출되는 것을 기다리지 않고 즉시 종료되어 콜 스택에서 제거된다.
* 이후 타이머가 만료되면 setTimeout 함수의 콜백은 태스크 큐로 푸시되고 콜 스택이 비어졌을 때 이벤트 루프에 의해 콜 스택으로 푸시되어 실행된다.

setTimeout의 콜백이 콜 스택에 푸시되어 실행될 때, setTimeout 함수는 이미 콜 스택에서 제거된 상태이다. 이것은 **setTimeout 함수의 콜백을 호출한 것이 setTimeout 함수가 아니라는 것이다.** setTimeout 함수의 콜백의 호출자(caller)가 setTimeout 함수라면, 콜 스택의 콜백 함수 실행 컨텍스트 하위에는 setTimeout 실행 컨텍스트가 존재해야 한다. 따라서 setTimeout 함수의 콜백 함수가 발생시킨 에러는 catch 블록에서 캐치되지 않는다.

지금까지 살펴본 비동기 처리를 위한 콜백 패턴의 콜백 헬이나 에러 처리의 한계를 극복하기 위해 ES6에서 프로미스(Promise)가 도입되었다.

&nbsp;  

## 2. 프로미스의 생성

프로미스는 Promise 생성자 함수를 통해 인스턴스화한다. Promise 생성자 함수는 비동기 처리를 수행할 콜백 함수를 인자로 전달받는데, 이 콜백 함수는 resolve와 reject 함수를 인수로 전달 받는다.

```javascript
// Promise 객체 생성
const promise = new Promise((resolve, reject) => {
  // Promise 함수의 콜백 함수 내부에서 비동기 처리를 수행한다.
  if (/* 비동기 처리 성공 */) {
    resolve('result');
  } else { // 비동기 처리 실패
    reject('failure reason');
  }
});
```

&nbsp;  

Promise 생성자 함수가 인수로 전달받은 콜백 함수 내부에서 비동기 처리를 수행한다. 이때 비동기 처리가 성공하면 콜백 함수의 인수로 전달받은 resolve 함수를 호출하고, 비동기 처리가 실패하면 reject 함수를 호출한다. 앞서 살펴보았던 비동기 함수 get을 프로미스로 구현해보자.

```javascript
// GET 요청을 위한 비동기 함수
const get = url => {
	return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.send();
    
    xhr.onload = () => {
    	if (xhr.status === 200) {
        resolve(JSON.parse(xhr.response));
      } else {
        reject(new Error(xhr.status));
      }
    };
  });
};

// get 함수는 Promise 객체를 반환한다.
const promiseGet = get('https://jsonplaceholder.typicode.com/posts/1');
```

위 예제의 get 함수는 Promise로 구현된 비동기 함수이다. get 함수는 Promise 객체를 생성하고 반환한다. 비동기 처리는 Promise 생성자 함수가 인수로 전달받은 콜백 함수 내부에서 수행한다. **만약 비동기 처리에 성공하면 비동기 처리 결과를 resolve 함수에 인수로 전달하면서 호출하고, 비동기 처리에 실패하면 에러를 reject 함수에 인수로 전달하면서 호출한다.**

&nbsp;  

Promise 객체는 비동기 처리가 성공했는지 또는 실패했는지 등의 상태 정보를 갖는다.

| 상태      | 의미                                                         | 구현                                               |
| --------- | ------------------------------------------------------------ | -------------------------------------------------- |
| pending   | 비동기 처리가 아직 수행되지 않은 상태                        | resolve 또는 reject 함수가 아직 호출되지 않은 상태 |
| fulfilled | 비동기 처리가 수행된 상태 (성공)                             | resolve 함수가 호출된 상태                         |
| rejected  | 비동기 처리가 수행된 상태 (실패)                             | reject 함수가 호출된 상태                          |
| settled   | fulfilled 또는 rejected와 상관 없이 pending이 아닌 상태. 즉, 비동기 처리가 수행된 상태 | resolve 또는 reject 함수가 호출된 상태             |

Promise 객체의 상태 정보는 resolve 또는 reject 함수를 호출하는 것으로 결정된다. resolve 또는 reject 함수를 호출할 때 전달한 **비동기 처리 결과 또는 에러는 Promise 객체의 후속 처리 메소드에게 전달된다.**

&nbsp;  

## 3. 프로미스의 후속 처리 메소드

프로미스로 구현된 비동기 함수(ex. 위 예제의 `get` 함수)는 Promise 객체를 반환해야 한다. 프로미스로 구현된 비동기 함수를 호출하는 측(promise consumer)은 Promise 객체의 후속 처리 메소드 `then`, `catch`, `finally`를 통해 비동기 처리 결과 또는 에러 메시지를 전달받아 후속 처리를 수행한다. **모든 후속 처리 메소드 또한 비동기식으로 동작한다.**

Promise 객체는 비동기 처리가 성공(fulfilled) 했는지 또는 실패(rejected)했는지 등의 상태 정보를 가진다고 했다. 이 상태 정보에 따라 후속 처리 메소드를 **체이닝 방식**으로 호출 한다. 프로미스의 후속 처리 메소드는 다음과 같다.

&nbsp;  

**`Promise.prototype.then`**

```javascript
p.then(onFulfilled[, onRejected]);

p.then(value => {
  // fulfillment
}, reason => {
  // rejection
});
```

| 매개 변수          | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| (옵션) onFulfilled | * 프로미스가 fulfilled되면 호출되는 함수.<br />* 하나의 인수(fulfillment value)를 전달 받는다.<br />* 만약 함수가 아니면, 내부적으로 "Identity" 함수로 대체된다.<br />* "Identity" 함수는 fulfillment value를 반환한다. |
| (옵션) onRejected  | * 프로미스가 rejected되면 호출되는 함수.<br />* 하나의 인수(rejection reason)을 전달 받는다.<br />* 만약 함수가 아니면, 내부적으로 "Thrower" 함수로 대체된다.<br />* "Thrower" 함수는 에러(rejection reason)를 throw한다. |

`then` 메소드에 전달된 인수가 함수가 아니거나, 전달된 인수가 자체가 없어도 에러가 발생하지 않는다. 이러한 경우 `then` 메소드는 이전 프로미스 객체의 상태와 성공 값/실패 이유를 그대로 갖는 새로운 프로미스 객체를 반환한다.

&nbsp;  

프로미스가 fulfilled 혹은 rejected되면, 후속 처리 메소드에 전달된 콜백 함수(`onFulfilled` 혹은 `onRejected`)가 **비동기적으로 호출된다.** 콜백 함수의 동작에 따라 후속 처리 메소드가 반환하는 프로미스 객체의 상태가 달라진다. 단, **`then` 메소드는 언제나 프로미스 객체를 반환한다.**

| 콜백 함수의 동작                 | then이 반환하는 Promise 객체                                 |
| -------------------------------- | ------------------------------------------------------------ |
| 값(value)를 반환                 | 콜백 함수가 반환한 값을 resolve한 프로미스                   |
| 아무 것도 반환하지 않음          | undefined를 resolve한 프로미스                               |
| 에러를 throw                     | 콜백 함수가 throw한 에러를 reject한 프로미스                 |
| 이미 fulfilled된 프로미스를 반환 | 콜백 함수가 반환한 프로미스의 fulfillment value로 fulfilled된 프로미스 |
| 이미 rejected된 프로미스를 반환  | 콜백 함수가 반환한 프로미스의 reject reason으로 rejected된 프로미스 |
| pending 상태의 프로미스를 반환   | 콜백 함수가 반환한 프로미스의 성공/실패 상태에 따라 성공/실패된 프로미스. `then`이 반환하는 프로미스의 resolve 값은 콜백 함수가 반환한 프로미스의 resolve 값과 동일하다. |

&nbsp;  

**`Promise.prototype.catch`**

```javascript
p.catch(onRejected);

p.catch(function (reason) {
  // rejection
});
```

| 매개 변수  | 설명                                                         |
| ---------- | ------------------------------------------------------------ |
| onRejected | * 프로미스가 rejected되면 호출되는 함수.<br />* 하나의 인수(rejection reason)를 전달 받는다.<br />* 만약 onRejected가 에러를 throw하거나, 이미 rejected 프로미스를 반환하면 catch가 반환하는 프로미스는 rejected 상태를 가진다. 그 외의 경우 catch 반환하는 프로미스는 resolved 상태를 가진다.<br />* 만약 함수가 아니면, 내부적으로 "Thrower" 함수로 대체된다.<br />* "Thrower" 함수는 에러(rejection reason)를 throw한다. |

**반환 값:** 프로미스 객체. `catch`는 내부적으로 `Promise.prototype.then` 메소드를 호출한다. 이때 `then` 메소드에 전달되는 첫 번째 인수(onFulfilled)로 undefined가 전달되고, 두 번째 인수(onRejected)에 `catch` 메소드에 전달한 콜백이 전달된다.

&nbsp;  

`catch` 메소드는 프로미스 체인에서 발생한 에러를 핸들링하기 위해 사용된다. `catch` 메소드는 프로미스 객체를 반환하기 때문에 프로미스 체이닝을 이어서 사용할 수 있다.

&nbsp;  

**`Promise.prototype.finally`**

* `finally` 메소드는 한 개의 콜백 함수를 인수로 전달 받는다.
* `finally` 메소드의 콜백 함수는 프로미스의 성공 또는 실패와 상관없이 무조건 한 번 호출된다.
* `finally` 메소드는 프로미스의 상태와 상관없이 공통적으로 수행해야할 후속 처리에 사용된다.
* `finally` 메소드도 `then` / `catch` 메소드와 마찬가지로 언제나 Promise 객체를 반환한다.
* `finally` 메소드는 2020년 5월 TC39 프로세스의 stage 4에 제안되어 있다. IE를 제외한 대부분의 브라우저에서 지원하고 있다.

```javascript
new Promise(() => {})
  .finally(() => console.log('finally')); // finally
```

&nbsp;  

프로미스로 구현한 비동기 함수 `get`을 사용해 후속 처리를 구현해보자.

```javascript
const get = url => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.sned();
    
    xhr.onload = () => {
      if (xhr.status === 200) {
        resolve(JSON.parse(xhr.response));
      } else {
        reject(new Error(xhr.status));
      }
    };
  });
};

get('https://jsonplaceholder.typicode.com/posts/1')
  .then(post => console.log(post))
  .catch(error => console.error(error))
  .finally(() => console.log('Good Bye'));
```

&nbsp;  

## 4. 프로미스의 에러 처리

위 예제의 비동기 함수 `get`은 Promise 객체를 반환한다. 비동기 처리 결과에 대한 후속 처리는 Promise 객체가 제공하는 후속 처리 메소드 `then`, `catch`, `finally`를 사용하여 수행한다. 비동기 처리 시에 발생한 에러는 `then` 메소드의 두 번째 콜백 함수로 처리할 수 있다.

```javascript
const wrongUrl = 'https://jsonplaceholder.typicode.com/XXX/1';

// 부적절한 URL이 지정되었기 때문에 에러가 발생한다.
get(wrongUrl)
  .then(res => console.log(res), err => console.error(err)); // Error: 404
```

&nbsp;  

비동기 처리 시에 발생한 에러는 Promise 객체의 후속 처리 메소드 `catch`를 사용하여 처리할 수도 있다.

```javascript
const wrongUrl = 'https://jsonplaceholder.typicode.com/XXX/1';

// 부적절한 URL이 지정되었기 때문에 에러가 발생한다.
get(wrongUrl)
  .then(res => console.log(res))
  .catch(err => console.error(err)); // Error: 404
```

&nbsp;  

`catch` 메소드를 호출하면 내부적으로 `then` 메소드를 호출한다. 위 예제는 내부적으로 다음과 같이 처리된다.

```javascript
const wrongUrl = 'https://jsonplaceholder.typicode.com/XXX/1';

// 부적절한 URL이 지정되었기 때문에 에러가 발생한다.
get(wrongUrl)
  .then(res => console.log(res))
  .then(undefined, err => console.error(err)); // Error: 404
```

&nbsp;  

`catch` 메소드는 에러를 처리한다는 점에서 `then` 메소드의 두 번째 콜백 함수와 동일하지만 미묘한 차이가 있다. **`then` 메소드의 두 번째 콜백 함수는 비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)만을 캐치한다. 즉, `then` 메소드 내부의 에러를 캐치하지 못한다.**

```javascript
get('https://jsonplaceholder.typicode.com/todos/1')
  .then(res => console.xxx(res), err => console.error(err));
  // 두 번째 콜백 함수는 첫 번째 콜백 함수에서 발생한 에러를 캐치하지 못한다.
```

하지만 `catch` 메소드는 비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)와 `then` 메소드 내부에서 발생한 에러도 캐치한다.

```javascript
get('https://jsonplaceholder.typicode.com/todos/1')
  .then(res => console.xxx(res))
  .catch(err => console.error(err));
  // TypeError: console.xxx is not a function
```

따라서 에러 처리는 `catch` 메소드를 사용하는 편이 보다 효율적이다. 또한 `then` 메소드에 두 번째 콜백 함수를 전달하는 것보다 `catch` 메소드를 사용하는 것이 가독성이 더 좋다.

&nbsp;  

## 5. 프로미스 체이닝

비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 비동기 함수의 호출이 중첩(nesting)되어 복잡도가 높아지는 콜백 헬이 발생한다. Promise 객체를 반환한 비동기 함수는 프로미스 후속 처리 메소드인 `then`, `catch`, `finally` 메소드를 사용할 수 있다. 이 후속 처리 메소드는 모두 Promise 객체를 반환한다. 따라서 후속 처리 메소드를 체이닝하여 호출할 수 있다. 이로써 콜백 헬을 해결한다.

```javascript
const url = 'https://jsonplaceholder.typicode.com';

get(`${url}/posts/1`)
  .then(({ userId }) => get(`${url}/users/${userId}`))
  .then(userInfo => console.log(userInfo))
  .catch(err => console.error(err));

// 콜백 헬
/*
get(`${url}/posts/1`, ({ userId }) => {
	get(`${url}/users/${userId}`, userInfo => {
    console.log(userInfo);
  });
});
*/
```

&nbsp;  

## 6. 프로미스의 정적 메소드

Promise는 주로 생성자 함수로 사용되지만, 함수도 객체이므로 메소드를 가질 수 있다. Promise 객체는 5가지 정적 메소드를 제공한다.

&nbsp;  

### 6.1. Promise.resolve / Promise.reject

`Promise.resolve`와 `Promise.reject` 메소드는 이미 존재하는 값을 래핑하여 Promise 객체를 생성하기 위해 사용한다.

정적 메소드 `Promise.resolve` 메소드는 인자로 전달된 값을 resolve하는 Promise 객체를 생성한다.

```javascript
// 배열을 resolve하는 Promise 객체 생성
const resolvedPromise = Promise.resolve([1, 2, 3]);
resolvedPromise.then(console.log); // [1, 2, 3]
```

위 예제는 다음 예제와 동일하게 동작한다.

```javascript
const resolvedPromise = new Promise(resolve => resolve([1, 2, 3]));
resolvedPromise.then(console.log);
```

&nbsp;  

`Promise.reject` 메소드는 인자로 전달된 값을 reject하는 Promise 객체를 생성한다.

```javascript
// 에러 객체를 reject하는 Promise 객체를 생성
const rejectedPromise = Promise.reject(new Error('Error!'));
rejectedPromise.catch(console.log); // Error: Error!
```

위 예제는 다음 예제와 동일하게 동작한다.

```javascript
const rejectedPromise = new Promise((_, reject) => reject(new Error('Error!')));
rejectedPromise.catch(console.log); // Error: Error!
```

&nbsp;  

### 6.2. Promise.all

`Promise.all` 메소드는 **Promise 객체를 요소로 가지는 배열 등의 이터러블을 인자로 전달받는다.** 그리고 전달받은 모든 Promise 객체를 모두 <strong>연속적으로 처리</strong>하고, 그 처리 결과를 resolve하는 새로운 프로미스를 반환한다.

```javascript
Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 3000)),
  new Promise(resolve => setTimeout(() => resolve(2), 2000)),
  new Promise(resolve => setTimeout(() => resolve(3), 1000))
]).then(conosle.log) // [1, 2, 3]
  .catch(console.error);
```

위 예제의 `Promise.all` 메소드는 3개의 Promise 객체를 요소로 가지는 배열을 전달받았다. 각각의 Promise 객체는 다음과 같이 동작한다.

* 첫 번째 Promise 객체는 3초 후 1을 resolve하여 처리 결과를 반환한다.
* 두 번째 Promise 객체는 2초 후 2를 resolve하여 처리 결과를 반환한다.
* 세 번째 Promise 객체는 1초 후 3을 resolve하여 처리 결과를 반환한다.

`Promise.all` 메소드는 전달받은 모든 Promise 객체를 연속적으로 처리한다. `Promise.all`은 배열 내 모든 Promise 객체의 resolve 또는 첫 번째 reject를 기다린다.

모든 Promise 객체의 처리가 성공하면 모든 Promise 객체가 resolve한 처리 결과를 배열에 담아 resolve하는 새로운 Promise 객체를 반환한다. 이때 첫 번째 Promise 객체가 가장 나중에 처리되어도, `Promise.all` 메소드가 반환하는 Promise 객체는 첫 번째 Promise 객체가 resolve한 처리 결과부터 차례대로 배열에 담에 그 배열을 resolve하는 새로운 Promise 객체를 반환한다. 즉, **처리 순서가 보장된다.**

Promise 객체의 처리가 하나라도 실패하면 가장 먼저 실패한 Promise 객체가 reject한 에러를 reject하는 새로운 Promise 객체를 **즉시 반환한다.**

```javascript
Promise.all([
	new Promise((_, reject) => setTimeout(() => reject(new Error('Error 1')), 3000)),
  new Promise((_, reject) => setTimeout(() => reject(new Error('Error 2')), 2000)),
  new Promise((_, reject) => setTimeout(() => reject(new Error('Error 3')), 1000))
]).then(console.log)
  .catch(console.error); // Error: Error 3
```

위 예제의 경우 세 번째 Promise 객체가 가장 먼저 실패하므로 세 번째 Promise 객체가 reject한 에러가 catch 메소드로 전달된다.

&nbsp;  

`Promise.all` 메소드는 인수로 전달받은 이터러블의 요소가 Promise 객체가 아닌 경우, `Promise.resolve` 메소드를 통해 Promise 객체로 래핑한다.

```javascript
Promise.all([
	1, // Promise.resolve(1)
	2, // Promise.resolve(2)
	3 // Promise.resolve(3)
]).then(console.log) // [1, 2, 3]
  .catch(console.error);
```

&nbsp;  

### 6.3. Promise.race

`Promise.race` 메소드는 `Promise.all` 메소드와 동일하게 Promise 객체를 요소로 가지는 배열 등의 이터러블을 인자로 전달받는다. `Promise.race` 메소드는 `Promise.all` 메소드처럼 모든 Promise 객체를 연속적으로 처리하는 것이 아니라, **가장 먼저 처리된 Promise 객체가 resolve한 처리 결과를 resolve하는 새로운 Promise 객체를 반환한다.**

```javascript
Promise.race([
  new Promise(resolve => setTimeout(() => resolve(1), 3000)),
  new Promise(resolve => setTimeout(() => resolve(2), 2000)),
  new Promise(resolve => setTimeout(() => resolve(3), 1000))
]).then(conosle.log) // 3
  .catch(console.error);
```

&nbsp;  

에러가 발생한 경우는 `Promise.all` 메소드와 동일하게 처리된다. 즉, `Promise.race` 메소드에 전달된 Promise 객체의 처리가 하나라도 실패하면 가장 먼저 실패한 Promise 객체가 reject한 에러를 reject하는 새로운 Promise 객체를 **즉시 반환한다.**

```javascript
Promise.race([
	new Promise((_, reject) => setTimeout(() => reject(new Error('Error 1')), 3000)),
  new Promise((_, reject) => setTimeout(() => reject(new Error('Error 2')), 2000)),
  new Promise((_, reject) => setTimeout(() => reject(new Error('Error 3')), 1000))
]).then(console.log)
  .catch(console.error); // Error: Error 3
```

&nbsp;  

### 6.4. Promise.allSettled

`Promise.allSettled` 메소드는 Promise 객체를 요소로 가지는 배열 등의 이터러블을 인자로 전달받는다. 그리고 전달받은 모든 Promise 객체를 모두 연속적으로 처리하고 그 처리 결과를 배열로 반환한다.

```javascript
Promise.allSettled([
  new Promise(resolve => setTimeout(() => resolve(1), 2000)),
  new Promise((_, reject) => setTimeout(() => reject(new Error('Error!')), 1000))
]).then(console.log);
/*
[
	{status: "fulfilled", value: 1},
	{status: "rejected", reason: Error: Error! at <anonymous>:3:60}
]
*/
```

`Promise.allSettled` 메소드가 반환한 배열에는 fulfilled 또는 rejected 상태와 상관없이 인수로 전달받은 모든 Promise 객체들의 처리 결과가 담겨 있다.

모든 Promise 객체의 처리 결과를 나타내는 배열의 요소는 각 Promise 객체의 상태(fulfilled/rejected를 나타내는 status 프로퍼티와, 처리 결과 / 에러를 나타내는 value / reason 프로퍼티를 가진다.

`Promise.allSettled` 메소드는 2020년 5월 TC39 프로세스의 stage 4에 제안되어 있다. IE를 제외한 대부분의 브라우저에서 지원한다.

&nbsp;  

## 7. 마이크로태스크 큐

다음 예제를 살펴보고 어떤 순서로 로그가 출력될지 생각해보자.

```javascript
setTimeout(() => console.log(1), 0);

Promise.resolve()
	.then(() => console.log(2))
	.then(() => console.log(3));
```

프로미스의 후속 처리 메소드도 비동기식으로 동작하므로 1, 2, 3 순으로 출력될 것처럼 보이지만, 2, 3, 1 순으로 출력된다. 그 이유는 **프로미스의 후속 처리 메소드의 콜백 함수는 태스크 큐가 아니라 마이크로태스크 큐에 저장되기 때문이다.**

마이크로태스크 큐는 태스크 큐와는 별도의 큐이다. 마이크로태스크 큐는 프로미스의 후속 처리 메소드의 콜백 함수가 일시 저장된다. 그 외의 비동기 처리 함수의 콜백 함수나 이벤트 핸들러는 태스크 큐에 일시 저장된다. 콜백 함수나 이벤트 핸들러를 일시 저장하는 점에서 태스크 큐와 동일하지만, **마이크로태스크 큐는 태스크 큐보다 우선 순위가 높다.**

즉, 이벤트 루프는 콜 스택이 비면 먼저 마이크로태스크 큐에서 대기하고 있는 콜백 함수나 이벤트 핸들러를 가져와 실행한다. 이후 마이크로태스크 큐가 비면 태스크 큐에서 대기하고 있는 콜백 함수나 이벤트 핸들러를 가져와 실행한다.

&nbsp;  

## 8. fetch

fetch 함수는 XMLHttpRequest 객체와 마찬가지로 HTTP 요청 전송 기능을 제공하는 클라이언트 사이드 Web API이다. fetch 함수는 XMLHttpRequest 객체보다 사용법이 간단하고 프로미스를 지원하기 때문에 비동기 처리를 위한 콜백 패턴의 단점에서 자유롭다. fetch 함수는 비교적 최근에 추가된 Web API로서 IE를 제외한 대부분의 브라우저에서 제공하고 있다.

&nbsp;  

fetch 함수에는 HTTP 요청을 전송할 URL과 HTTP 요청 헤더, 페이로드 등을 설정한 객체를 전달한다.

```javascript
const promise = fetch(url, [, options]);
```

&nbsp;  

**fetch 함수는 HTTP 응답을 나타내는 Response 객체를 래핑한 Promise 객체를 반환한다.** fetch 함수로 GET 요청을 전송해 보자. fetch 함수에 첫 번째 인수로 HTTP 요청을 전송할 URL만을 전달하면 GET 요청을 전송한다.

```javascript
fetch('https://jsonplaceholder.typicode.com/todos/1')
	.then(response => console.log(response));
```

&nbsp;  

fetch 함수는 HTTP 응답을 나타내는 Response 객체를 래핑한 프로미스를 반환하므로, 후속 처리 메소드 then을 통해 프로미스가 resolve한 Response 객체를 전달받을 수 있다. Response 객체는 HTTP 응답을 나타내는 다양한 프로퍼티를 제공한다.

<img src="https://user-images.githubusercontent.com/32444914/84765307-0186e280-b00a-11ea-908c-c627f0dd38b7.png" width="80%" />

&nbsp;  

`Response.prototype`에는 Response 객체에 포함되어 있는 HTTP 응답 몸체(body)를 위한 다양한 메소드를 제공한다. 예를 들어, fetch 함수가 반환한 프로미스가 래핑하고 있는 HTTP 응답 몸체를 취득하려면 `Response.prototype.json` 메소드를 사용한다. `Response.prototype.json` 메소드는 Response 객체에서 HTTP 응답 몸체(response.body)를 취득하여 역직렬화(`JSON.parse`)한다.

```javascript
fetch('https://jsonplaceholder.typicode.com/todos/1')
	// reponse는 HTTP 응답을 나타내는 Response 객체이다.
	// json 메소드를 사용하여 Response 객체에서 HTTP 응답 몸체를 취득하여 역직렬화한다.
	.then(response => response.json())
	// json은 역직렬화된 HTTP 응답 몸체이다.
	.then(json => console.log(json));
	// {userId: 1, id: 1, title: "delectus aut autem", completed: false}
```

&nbsp;  

fetch 함수를 통해 HTTP 요청을 전송해보자. fetch 함수에 첫 번째 인수로 HTTP 요청을 전송할 URL과 두 번째 인수로 HTTP 요청 메소드, HTTP 요청 헤더, 페이로드 등을 설정한 객체를 전달한다.

```javascript
const request = {
	get(url) {
		return fetch(url);
	},
	post(url, paylaod) {
    return fetch(url, {
			method: 'POST',
			headers: { 'content-type': 'application/json' },
			body: JSON.stringify(payload)
    });
	},
  patch(url, payload) {
    return fetch(url, {
      method: 'PATCH',
      headers: { 'content-type': 'application/json' },
      body: JSON.stringify(payload)
    });
  },
  remove(url) {
    return fetch(url, { method: 'DELETE' });
  }
};
```

**1. GET 요청**

```javascript
request.get('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
	.then(todos => console.log(todos))
	.catch(err => console.error(err));
// {userId: 1, id: 1, title: "delectus aut autem", completed: false}
```

**2. POST 요청**

```javascript
request.post('https://jsonplaceholder.typicode.com/todos', {
  userId: 1,
  title: 'JavaScript',
  completed: false
}).then(response => response.json())
	.then(todos => console.log(todos))
	.catch(err => console.error(err));
// {userId: 1, title: "JavaScript", completed: false, id: 201}
```

**3. PATCH 요청**

```javascript
request.patch('https://jsonplaceholder.typicode.com/todos/1', {
  completed: true
}).then(response => response.json())
	.then(todos => console.log(todos))
	.catch(err => console.error(err));
// {userId: 1, id: 1, title: "delectus aut autem", completed: true}
```

**4. DELETE 요청**

```javascript
request.remove('https://jsonplaceholder.typicode.com/todos/1')
	.then(response => response.json())
	.then(todos => console.log(todos))
	.catch(err => console.error(err));
```

&nbsp;  

## 출처

* [poiemaweb.com - 프로미스](https://poiemaweb.com/fastcampus/promise)

