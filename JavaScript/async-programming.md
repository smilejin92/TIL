# 비동기 프로그래밍

URI vs. URL

웹(www) vs. 인터넷

Host로 DNS에 가서 Host와 1:1 맵핑되어 있는 IP 취득

## 1. 동기식 처리 모델과 비동기식 처리 모델

실행 컨텍스트에서 살펴본 바와 같이 함수를 호출하면 함수 코드가 평가되어 함수의 실행 컨텍스트가 생성된다. 이때 생성된 함수의 실행 컨텍스트는 실행 컨텍스트 스택(콜 스택)에 푸시되고 함수 코드가 실행된다. 함수 코드의 실행이 종료하면 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 pop되어 제거된다.

함수가 호출된 순서대로 실행되는 이유는 함수가 호출된 순서대로 함수 실행 컨텍스트가 실행 컨텍스트 스택에 푸시되기 때문이다.

**자바스크립트 엔진은 단 하나의 실행 컨텍스트 스택을 가진다.** 이는 함수를 실행할 수 있는 창구가 단 하나이며, 동시에 2개 이상의 함수를 실행할 수 없다는 것을 의미한다. 실행 컨텍스트의 최상위 스택(running execution context)을 제외한 모든 실행 컨텍스트는 <strong>실행 대기 중인 태스크(task)</strong>들이다. 대기 중인 태스크들은 현재 실행 중인 실행 컨텍스트가 pop되어 실행 컨텍스트 스택에서 제거되면, 비로소 실행되기 시작한다.

이처럼 자바스크립트 엔진은 한 번에 하나의 태스크만 실행할 수 있는 <strong>싱글 스레드(single thread)</strong> 방식으로 동작한다. 싱글 스레드 방식은 한번에 하나의 태스크만 실행할 수 있기 때문에 처리에 시간이 걸리는 태스크를 실행하는 경우 <strong>블로킹(blocking, 작업 중단)</strong>이 발생한다.

예를 들어, `setTimeout` 함수와 유사하게 일정 시간이 경과한 이후 콜백 함수를 호출하는 `sleep` 함수를 구현해 보자.

```javascript
function sleep(callback, delay) {
  const delayUntil = Date.now() + delay;
  
  while (Date.now() < delayUntil);
  callback();
}

function foo() {
  console.log('foo');
}

function bar() {
  console.log('bar');
}

// 일정 시간이 경과한 이후에 콜백 함수 foo를 호출하므로 다음에 호출될 bar가 블로킹된다.
sleep(foo, 3 * 1000);
bar();
// (3초 경과후) foo -> bar
```

위 예제처럼 현재 실행중인 태스크가 종료할 때까지 다음 실행될 태스크가 대기하는 방식을 <strong>동기식 처리 모델(synchronous processing model)</strong>이라고 한다. 동기식 처리 모델은 **태스크를 순차적으로 하나씩 처리하는 방식**이다.

동기식 처리 모델은 태스크의 처리 순서가 보장된다는 장점이 있다. 하지만 앞선 태스크가 종료할 때까지 이후 태스크들이 블로킹되는 단점이 있다. 위 예제의 `sleep` 함수는 3초간 대기하다가 인수로 전달받은 콜백 함수 `foo`를 호출한다. 따라서 `sleep` 함수가 종료된 이후 실행될 태스크인 `bar` 함수는 3초 이상 블로킹된다.

<img src="https://user-images.githubusercontent.com/32444914/84345384-2cc39900-abe8-11ea-9b77-36c0daf7e3bb.png" width="70%" />

&nbsp;  

위 예제를 타이머 함수인 `setTimeout`을 사용하여 수정해 보자.
```javascript
function foo() {
	console.log('foo');
}

function bar() {
	console.log('bar');
}

// 타이머 함수 setTimeout은 일정 시간이 경과한 이후 콜백 함수(foo)를 호출한다.
// 타이머 함수 setTimout은 bar 함수를 블로킹하지 않는다.
setTimeout(foo, 3 * 1000);
bar();
// bar -> (3초 경과 후) foo
```

타이머 함수 `setTimeout`은 앞서 살펴본 `sleep` 함수와 유사하게 일정 시간이 경과한 이후 콜백 함수를 호출하지만, `setTimeout` 이후의 태스크를 블로킹하지 않고 곧바로 실행한다. 이처럼 현재 실행중인 태스크가 종료되지 않은 상태라 하더라도 다음 태스크를 곧바로 실행하는 방식을 <strong>비동기식 처리 모델(synchronous processing model)</strong>이라고 한다.

<img src="https://user-images.githubusercontent.com/32444914/84345643-d60a8f00-abe8-11ea-9b8f-caeda08a09b7.png" width="70%" />

비동기식 처리 모델은 블로킹이 발생하지 않는다는 장점이 있지만, 태스크의 처리 순서가 보장되지 않는 단점이 있다.

따라서 비동기 처리 과정에서 순차적인 처리가 필요한 경우 일반적으로 콜백 패턴을 사용했다. 하지만 비동기 처리를 위한 콜백 패턴은 콜백 헬을 발생시켜 가독성을 떨어트리고, 비동기 처리 중 발생한 에러의 예외 처리가 곤란하며, 여러 개의 비동기 처리를 한번에 처리하는 것도 한계가 있다.

타이머 함수인 `setTimeout`과 `setInterval`, HTTP 요청은 비동기식 처리 모델로 동작한다. **비동기식 처리 모델은 자바스크립트에 동시성(concurrency)을 부여한다. 동시성은 이벤트 루프로 구현된다.**

&nbsp;  

## 2. 이벤트 루프와 동시성




















