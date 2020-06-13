# Using Promises

프로미스는 어떠한 비동기 작업의 최종 상태(완료 혹은 실패)를 나타내는 객체이다.

콜백을 함수에 전달하는 방법 대신, 프로미스는 콜백을 연결하여 사용할 수 있는 객체이다.

예를 들어 `createAudioFileAyn`라는 함수가 있다고 가정해보자. `createAudioFileAyncs` 함수는 주어진 설정과 2개의 콜백 함수를 인수로 전달받아 오디오 파일을 비동기적으로 생성한다. 첫 번째 콜백은 오디오 파일 생성에 성공했을 때 호출되고, 두 번째 콜백은 에러가 발생했을 때 호출된다.

```javascript
function successCallback(result) {
  console.log('Audio file ready at URL: ' + result);
}

function failureCallback(error) {
  console.error("Error generating audio file: " + error);
}

createAudioFileAsync(audioSettings, successCallback, failureCallback);
```

&nbsp;  

위 예제는 프로미스 객체를 반환하는 함수에 콜백을 연결하는 방식으로 대체하여 사용할 수 있다. 만약 `createAudioFileAync` 함수가 프로미스 객체를 반환하도록 작성되었다면, 위 예제는 아래와 같이 작성될 수 있다.

```javascript
createAudioFileAsync(audioSetting).then(successCallback, failureCallback);
```

위 예제는 아래 예제와 동치이다.

```javascript
const promise = createAudioFileAsync(audioSettings);
promise.then(successCallback, failureCallback);
```

이러한 방법을 비동기적 함수 호출(asynchronous function call)이라 부른다. 비동기적 함수 호출은 몇가지 장점이 있다.

&nbsp;  

## Guarantees

콜백을 전달하는 "옛날 방식"과는 달리, 프로미스는 몇가지 사항을 보장(guarantee)한다.

* 자바스크립트 이벤트 루프의 현재 실행 중인 태스크가 완료(completion of the current run)되기 전에 콜백은 절대 먼저 호출되지 않는다.
* `then` 메소드로 추가된 콜백은 비동기 작업이 성공 혹은 실패한 이후에 호출된다.
* `then` 메소드를 여러번 호출하여 여러 개의 콜백을 추가할 수 있다. 각 콜백은 이전의 콜백이 실행된 이후에 호출되기 때문에 실행 순서가 보장된다.

프로미스의 장점 중 하나는 체이닝(chaining)이다.

&nbsp;  

## Chaining

프로미스 체인을 통해 두 개 이상의 비동기 작업을 원하는 순서대로 실행할 수 있다. 우선적으로 실행되어야 하는 비동기 작업의 성공 혹은 실패 결과를 그대로 가져와 이후의 비동기 작업에서 사용할 수 있다.

`then` 메소드는 기존의 프로미스 객체와 다른 새로운 프로미스 객체를 반환한다.

```javascript
const promise = doSomething();
const promise2 = doSomething().then(successCallback, failureCallbcak);
```

두 번째 프로미스(`promise2`)는 `doSomething`의 완료 상태와 `then` 메소드에 전달한 `successCallback` 혹은 `failureCallback`의 완료 상태 모두를 나타낸다 . 이때 `then` 메소드에 전달한 콜백은 프로미스를 반환하는 또 다른 비동기 함수일 수 있다. 만약 `then` 메소드에 전달한 콜백이 프로미스를 반환하는 비동기 함수(A)라면, `promise2`에 연결된 콜백들은 A가 반환한 프로미스가 settled 된 이후에 순차적으로 실행된다.

프로미스 체인 상의 각 프로미스는 다른 비동기 작업의 완료 상태를 나타낸다.

과거에는 연속적인 비동기 작업을 수행하기 위해 콜백 패턴을 사용했고, 이는 콜백 헬을 발생시켰다.
```javascript
doSomething(function(result) {
	doSomethingElse(result, function(newResult) {
		doThirdThing(newResult, function(finalResult) {
			console.log('Got the final result: ' + finalResult);
		}, failureCallback);
	}, failureCallback);
}, failureCallback);
```

위 예제의 콜백 헬을 프로미스 객체에 콜백을 연결하여 프로미스 체인을 구성하는 방법으로 대체할 수 있다.
```javascript
doSomething()
.then(result => doSomethingElse(result))
.then(newResult => doThirdThing(newResult))
.then(finalResult => {
	console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);
```

`then` 메소드를 호출할 때 인수(콜백)를 생략할 수 있다. 또한 `catch(failureCallback)`는 `then(null, failureCallback)`의 단축 표현이다.

**중요:** 후속 처리 메소드(`then`, `catch`)의 콜백(ex. `successCallback`, `failureCallback`)이 항상 값을 반환하도록 작성해야한다. 그렇지 않으면 이전의 프로미스의 결과를 이후의 후속 처리 메소드 콜백에서 사용할 수 없다.

&nbsp;  

### Chaining after a catch

`catch` 메소드도 프로미스를 반환하기 때문에 `catch` 메소드(작업 실패) 이후에 체이닝을 이어나갈 수 있다. 이러한 특징은 비동기 작업에 실패한 이후 새로운 작업을 수행하는 데 매우 유용하다.

```javascript
new Promise((resolve, reject) => {
  console.log('1. Initial');
  resolve();
  // reject();
  // resolve(혹은 reject)가 호출된 이후에 reject(혹은 resolve)가 호출되어도 프로미스의 상태는 변하지 않는다.
})
.then(() => {
  console.log('2. previous promise resolved')
  throw new Error('Something failed')
	// 에러가 throw되어 이 곳에 오기 전 catch 메소드로 넘어간다.
  console.log('Do this');
})
.catch(() => {
  console.log('3. previous promise rejected')
  console.error('Do This');
})
.then(() => {
  console.log('4. previous promise resolved');
  console.log('Do this, no matter what happend before');
});
```

&nbsp;  

## Error Propagation

이전 콜백 헬 예제를 보면 `failureCallback` 콜백이 3번 전달된 것을 확인할 수 있다. 그에 비해 프로미스 체인에서는 `failureCallback` 콜백은 `catch` 메소드에 단 한번 전달된다.

```javascript
doSomething()
.then(result => doSomethingElse(result))
.then(newResult => doThirdThing(newResult))
.then(finalResult => {
	console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);
```

만약 예외(ex. 에러)가 발생하면, 브라우저는 프로미스 체인에서 `catch` 메소드 혹은 `onRejected` 콜백을 찾아서 실행한다. 위 예제의 코드를 동기적 코드로 모델링하여 표현하면 아래와 같다.

```javascript
try {
  const result = syncDoSomething();
  const newResult = syncDoSomethingElse(result);
  const finalResult = syncDoThirdThing(newResult);
  console.log(`Got the final result: ${finalResult}`);
} catch(error) {
  failureCallback(error);
}
```

&nbsp;  

프로미스는 던져진(thrown) 예외를 포함한 모든 에러를 캐치함으로써 콜백 헬을 발생시키는 근본적인 문제를 해결한다.

&nbsp;  

## Creating a Promise around an old callback API

몇가지 API는 아직도 성공 혹은 실패시 실행할 콜백을 전달 받는 방법으로 동작한다. 대표적인 예로 `setTimeout` 함수가 있다.

```javascript
setTimeout(() => saySomething('10 sec passed'), 10 * 1000);
```

위 코드의 문제점은 만약 `setTimeout` 함수에 전달된 콜백이 에러를 발생하면 해당 에러를 캐치할 수 있는 코드가 없다는 것이다.

`setTimeout` 함수를 프로미스로 감싸서 이러한 문제를 해결할 수 있다.

```javascript
const wait = ms => new Promises(resolve => setTimeout(resolve, ms));

wait(10*1000)
  .then(() => saySomething('10 sec'))
  ..catch(failureCallback);
```

프로미스 생성자 함수는 작성자가 직접 프로미스를 resolve 혹은 reject 할 수 있는 executor 함수를 인수로 전달 받는다. `setTimeout` 함수 자체는 실패할 일이 없으므로 위 예제에서 reject는 생략하였다.

&nbsp;  

## Timing

이미 resolve된 프로미스 객체라도 `then` 메소드에 전달된 콜백은 절대 동기적으로 호출되지 않는다.

```javascript
Promise.resolve().then(() => console.log(2));
console.log(1);
// 1 2
```

후속 처리 메소드(`then`, `catch`)에 전달된 콜백은 즉시 실행되는 것이 아니라, 마이크로태스크 큐에 푸시된다. 즉, 이벤트 루프는 콜스택이 비어지면 일반 태스크 큐가 아닌 마이크로태스크 큐에 있는 콜백 함수나 이벤트 핸들러를 가져와 실행한다.

```javascript
const wait = ms => new Promise(resolve => setTimeout(resolve, ms));

wait(0).then(() => console.log(4));
Promise.resolve()
  .then(() => console.log(2))
  .then(() => console.log(3));
console.log(1); // 1 2 3 4
```

&nbsp;  

## Nesting

프로미스 체인의 중첩(neting)은 `catch`문의 스코프를 제한하기 위한 제어 구조이다. 특히 중첩된 `catch`문은 자신의 스코프를 포함한 하위 스코프에서 발생하는 실패(에러)만은 캐치한다. 중첩 구조 밖의 에러는 캐치하지 않는다. 이러한 방법은 에러의 범위를 좁힐 수 있다.

```javascript
Promise.resolve()
.then(() => Promise.reject()
  .then(() => console.log('여긴 안들어옵니다.'))
	.catch(() => console.log('1. Nested Error!')))
.then(() => console.log('2. Outer Success'))
.catch(() => console.log('중첩 catch에서 잡힌 에러는 안잡는다'));
```

&nbsp;  

## Promise rejection events

## Composition

## Common mistakes

## When promises and tasks collide

