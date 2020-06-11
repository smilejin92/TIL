# 프로미스

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

* `then` 메소드는 두 개의 콜백 함수를 인수로 전달 받는다.
* 첫 번째 콜백 함수는 프로미스가 fulfilled 상태(resolve 함수가 호출된 상태)가 되면 호출된다.
* 두 번째 콜백 함수는 프로미스가 rejected 상태(reject 함수가 호출된 상태)가 되면 호출된다.
* `then` 메소드는 언제나 Promise 객체를 반환한다.
* `then` 메소드의 콜백 함수가 Promise 객체가 아닌 값을 반환하면 그 값을 resolve 또는 reject하여 Promise 객체를 반환한다.(??????????? 이렇게 해서 then 메소드는 언제나 Promise 객체를 반환하는건지?)

```javascript
// fulfilled
new Promise(resolve => resolve('fulfilled'))
  .then(v => console.log(v), e => console.error(e)); // fulfilled

// rejected
new Promise((_, reject) => reject(new Error('rejected')))
  .then(v => console.log(v), e => console.error(e)); // Error: rejected
```

&nbsp;  

**`Promise.prototype.catch`**

* `catch` 메소드는 한 개의 콜백 함수를 인수로 전달 받는다.
* `catch` 메소드의 콜백 함수는 예외(비동기 처리에서 발생한 에러와 `then` 메소드에서 발생한 에러)가 발생하면 호출된다.

```javascript
// rejected
new Promise((_, reject) => reject(new Error('rejected')))
  .catch(e => console.log(e)); // Error: rejected
```

`catch` 메소드는 `then(undefined, onRejected)`와 동일하게 동작한다. 따라서 `then` 메소드와 마찬가지로 언제나 Promise 객체를 반환한다.

```javascript
// rejected
new Promise((_, reject) => reject(new Error('rejected')))
  .then(undefined, e => console.log(e)); // Error: rejected
```

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



























