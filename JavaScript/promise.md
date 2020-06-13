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

따라서 `then` 메소드에 전달된 인수가 함수가 아니거나, 전달된 인수가 아예 없어도 에러가 발생하지 않는다. 이러한 경우 `then` 메소드가 반환하는 새로운 프로미스 객체는 이전 프로미스 객체의 상태와 성공 값/실패 이유를 그대로 갖는다.

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























