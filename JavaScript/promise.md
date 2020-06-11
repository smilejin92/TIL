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

Promise 객체의 상태 정보는 resolve 또는 reject 함수를 호출하는 것으로 결정된다. resolve 또는 reject 함수를 호출할 때 전달한 비동기 처리 결과 또는 에러는 Promise 객체의 후속 처리 메소드에게 전달된다.

&nbsp;  



















