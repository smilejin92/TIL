# 이벤트

## 1. 이벤트 드리븐 프로그래밍

**브라우저는 처리해야 할 특정 사건이 발생하면 이를 감지하여 이벤트(event)를 발생(trigger)시킨다.** 예를 들어 클릭, 키보드 입력, 마우스 이동 등이 일어나면 브라우저는 이를 감지하여 특정한 타입의 이벤트를 발생시킨다.

<strong>이벤트 핸들러</strong>: 이벤트가 발생했을 때 호출될 함수

**이벤트 핸들러 등록**: 이벤트가 발생했을 때 브라우저에게 이벤트 핸들러의 호출을 위임하는 것

예를 들어 사용자가 버튼을 클릭하면 어떤 함수를 호출하고 싶다고 가정해보자. 이때 문제는 **언제 함수를 호출해야 하는가**이다. 사용자가 언제 버튼을 클릭할 지 알 수 없으므로 언제 함수를 호출해야 할지 알 수 없기 때문이다.

이때 브라우저는 사용자의 버튼 클릭을 감지하여 클릭 이벤트를 발생시킬 수 있다. 그리고 특정 버튼 요소에서 클릭 이벤트가 발생하면 특정 함수(이벤트 핸들러)를 호출하도록 브라우저에게 위임(이벤트 핸들러 등록)할 수 있다. 즉, 함수를 언제 호출할 지 알 수 없으므로 개발자가 명시적으로 함수를 호출하는 것이 아니라, **브라우저에게 함수 호출을 위임하는 것이다.**

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      // 사용자가 버튼을 클릭하면 함수를 호출하도록 요청
      $button.onclick = function () {
        console.log('button click');
      };
    </script>
  </body>
</html>
```

위 예제를 살펴보면 버튼 요소 `$button`의 `onclick` 프로퍼티에 함수를 할당하였다. 나중에 설명하겠지만 Window, Document, HTMLElement 타입의 객체는 `onclick`과 같이 이벤트에 대응하는 다양한 이벤트 핸들러 프로퍼티를 가지고 있다. **이벤트 핸들러 프로퍼티에 함수를 할당하면 해당 이벤트가 발생했을 때 할당한 함수가 브라우저에 의해 호출된다.**

이처럼 이벤트와 그에 대응하는 함수를 통해 사용자와 애플리케이션은 상호작용(Interaction)이 가능하게 된다. 이와 같이 프로그램의 흐름을 이벤트 중심으로 제어하는 프로그래밍 방식을 <strong>이벤트 드리븐 프로그래밍(event-driven programming)이라 한다.</strong>

&nbsp;  

## 2. 이벤트 타입

이벤트 타입(event type)은 **이벤트의 종류를 나타내는 문자열**이다. 예를 들어, 이벤트 타입 'click'은 사용자가 마우스 버튼을 클릭하였을 때 발생하는 이벤트를 나타낸다.

이벤트는 약 200여개의 종류가 있다. 이벤트에 대한 상세 목록은 [MDN의 Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)에서 확인할 수 있다.

&nbsp;  

## 3. 이벤트 핸들러 등록

이벤트 핸들러(event handler/listener)는 이벤트가 발생했을 때 **브라우저에 호출을 위임한 함수**이다. 다시 말해, 이벤트가 발생하면 브라우저에 의해 호출될 함수가 이벤트 핸들러이다.

이벤트가 발생했을 때 브라우저에게 이벤트 핸들러의 호출을 위임하는 것을 **이벤트 핸들러 등록**이라 한다. 이벤트 핸들러를 등록하는 방법은 3가지이다.

* 이벤트 핸들러 어트리뷰트
* 이벤트 핸들러 프로퍼티
* `addEventListener` 메소드

&nbsp;  

### 3.1. 이벤트 핸들러 어트리뷰트

**HTML 요소의 어트리뷰트**에는 이벤트에 대응하는 이벤트 핸들러 어트리뷰트가 있다. 이벤트 핸들러 어트리뷰트는 onclick과 같이 on 접두사와 이벤트 타입으로 이루어져 있다. HTML 요소의 이벤트 핸들러 어트리뷰트 값으로 함수 호출문 등의 문(statement)을 할당하면 이벤트 핸들러가 등록된다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button onclick="sayHi('Kim')">Click me!</button>
    <script>
    	function sayHi(name) {
        console.log(`Hi ${name}!`);
      }
    </script>
  </body>
</html>
```

주의할 것은 이벤트 핸들러 어트리뷰트 값으로 **함수 참조가 아닌 함수 호출문 등의 문을 할당한다는 것**이다.

이벤트 핸들러 등록이란, 함수 호출을 브라우저에게 위임하는 것이라 했다. 따라서 이벤트 핸들러를 등록할 때, 콜백 함수와 마찬가지로 **함수 참조**를 등록해야 브라우저가 등록된 함수, 즉 이벤트 핸들러를 호출할 수 있다. 만약 함수 참조가 아니라 함수 호출문을 등록하면 함수 호출문의 평가 결과가 이벤트 핸들러로 등록된다.

하지만 위 예제는 이벤트 핸들러 어트리뷰트 값으로 함수 호출문을 할당했다. 이때 **이벤트 핸들러 어트리뷰트 값은 사실 이벤트 핸들러의 함수 몸체를 의미한다.** 즉, `onclick="sayHi('Kim')"` 어트리뷰트는 파싱되어 아래와 같은 **함수를 생성하여 이벤트 핸들러 프로퍼티에 할당**한다.

```javascript
function onclick(event) {
  sayHi('Kim');
}
```

이처럼 동작하는 이유는 이벤트 핸들러 어트리뷰트 값으로 함수 참조를 할당하면 **이벤트 핸들러에 인수를 전달하기 곤란하기 때문이다.**

결국 **이벤트 핸들러 어트리뷰트 값으로 할당한 문자열은 암묵적으로 정의되는 이벤트 핸들러의 함수 몸체이다.** 따라서 이벤트 핸들러 어트리뷰트 값으로 아래와 같이 여러 개의 문을 할당할 수 있다.

```html
<button onclick="console.log('Hi! '); console.log('Kim');">Click me!</button>

<!--
암묵적으로 아래와 같은 함수(이벤트 핸들러)가 생성되어 이벤트 핸들러 프로퍼티에 할당한다.
function onclick(event) {
	console.log('Hi! ');
	console.log('Kim');
}
-->
```

이벤트 핸들러 어트리뷰트 방식은 오래된 코드에서 간혹 이 방식을 사용한 것이 있기 때문에 알아둘 필요는 있지만 더 이상 사용하지 않는 것이 좋다. HTML과 자바스크립트는 관심사가 다르므로 분리하는 것이 좋다.

단, **CBD**(Component Based Development) 방식의 Angular/React/Svelte/Vue.js와 같은 프레임워크/라이브러리에서는 이벤트 핸들러 어트리뷰트 방식으로 이벤트를 처리한다. CBD에서는 HTML, CSS, 자바스크립트 모두를 뷰(View)를 구성하기 위한 요소로 보기 때문에 관심사가 다르다고 생각하지 않는다.

&nbsp;  

### 3.2. 이벤트 핸들러 프로퍼티 방식

window 객체와 Document, HTMLElement 타입의 **DOM 노드 객체**는 이벤트에 대응하는 이벤트 핸들러 **프로퍼티**를 가지고 있다. 이벤트 핸들러 프로퍼티는 이벤트 핸들러 어트리뷰트와 마찬가지로 on 접두사와 이벤트 타입으로 이루어져 있다(ex. onclick). 이벤트 핸들러 프로퍼티에 함수를 바인딩하면 이벤트 핸들러가 등록된다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      // 이벤트 핸들러 프로퍼티에 이벤트 핸들러를 바인딩
      $button.onclick = function () {
        console.log('button click');
      };
    </script>
  </body>
</html>
```

이벤트 핸들러를 등록하기 위해서는 이벤트를 발생시킬 객체(event target), 이벤트 타입, 이벤트 핸들러를 지정할 필요가 있다.

<img src="https://user-images.githubusercontent.com/32444914/83029685-e7db2680-a06d-11ea-970e-c9c304dcd932.png" width="60%" />

이벤트 핸들러는 대부분의 경우 이벤트를 발생시킬 이벤트 타깃에 직접 바인딩한다. 하지만 이벤트 핸들러는 **전파된 이벤트를 캐치할 DOM 노드 객체**에 바인딩하기도 한다.

앞서 살펴본 **이벤트 핸들러 어트리뷰트 방식도 결국 DOM 노드의 이벤트 핸들러 프로퍼티로 변환되므로 결과적으로 이벤트 핸들러 프로퍼티 방식과 동일하다고 할 수 있다.** 이벤트 핸들러 프로퍼티 방식은 이벤트 핸들러 어트리뷰트 방식의 HTML과 자바스크립트의 **관심사를 분리**할 수 있다는 장점이 있다. 하지만 이벤트 핸들러 프로퍼티에 **하나의 이벤트 핸들러 만을 바인딩할 수 있다**는 단점이 있다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      // 이벤트 핸들러 프로퍼티 방식은 하나의 이벤트에 하나의 이벤트 핸들러만을 바인딩할 수 있다.
      $button.onclick = function () {
        console.log('Button clicked 1');
      };
      
      // 더 나중에 바인딩된 이벤트 핸들러가 등록된다.
      $button.onclick = function () {
        console.log('Button clicked 2');
      };
    </script>
  </body>
</html>
```

&nbsp;  

### 3.3. addEventListener 메소드 방식

DOM Level 2에서 도입된 `EventTarget.prototype.addEventListener` 메소드를 사용하여 이벤트를 등록할 수 있다. 이벤트 핸들러 어트리뷰트와 이벤트 핸들러 프로퍼티 방식은 DOM Level 0부터 제공되었던 방식이다.

<img src="https://user-images.githubusercontent.com/32444914/83031114-24f3e880-a06f-11ea-93ae-764a448e8abf.png" width="80%" />

* 첫번째 매개 변수에는 이벤트 타입(문자열)을 전달한다. 이때 on 접두사는 붙이지 않는다.
* 두번째 매개 변수에는 이벤트 핸들러를 전달한다.
* (옵션) 세번째 매개 변수에는 이벤트를 캐치할 이벤트 전파 단계(캡처링 또는 버블링)를 지정한다.
  * 생략하거나 false를 지정하면 버블링 단계에서 이벤트를 캐치한다.
  * true를 지정하면 캡처링 단계에서 이벤트를 캐치한다.

&nbsp;  

이벤트 핸들러 프로퍼티 방식은 이벤트 핸들러를 프로퍼티에 바인딩하지만, `addEventListener` 메소드에는 이벤트 핸들러를 **인수로 전달**한다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      // addEventListener 메소드 방식
      $button.addEventListener('click', function () {
        console.log('button clicked');
      });
    </script>
  </body>
</html>
```

&nbsp;  

`addEventListener` 메소드 방식은 **이벤트 핸들러 프로퍼티에 바인딩한 이벤트 핸들러에 아무런 영향을 주지 않는다.** 따라서 버튼 요소에서 클릭 이벤트가 발생하면 2개의 이벤트 핸들러가 모두 호출된다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      // 이벤트 핸들러 프로퍼티
      $button.onclick = function () {
        console.log('button clicked 1');
      };
      
      // addEventListener 메소드
      $button.addEventListener('click', function () {
        console.log('button clicked 2');
      });
    </script>
  </body>
</html>
```

&nbsp;  

`addEventListener` 메소드는 하나 이상의 이벤트 핸들러를 등록할 수 있다. 이때 이벤트 핸들러는 등록된 순서대로 호출된다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      // addEventListener 메소드는 동일한 요소에서 발생한 동일한 이벤트에 대해
      // 하나 이상의 이벤트 핸들러를 등록할 수 있다.
      $button.addEventListener('click', function() {
        console.log('button clicked 1');
      });
      
      $button.addEventListener('click', function () {
        console.log('button clicked 2');
      });
    </script>
  </body>
</html>
```

&nbsp;  

단, `addEventListener` 메소드를 통해 **참조가 동일한 이벤트 핸들러를 중복 등록하면 하나의 이벤트 핸들러만 등록된다.**

```html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      const handleClick = () => console.log('button click');
      
      // 참조가 동일한 이벤트 핸들러를 중복 등록하면 하나의 핸들러만 등록된다.
      $button.addEventListener('click', handleClick);
      $button.addEventListener('click', handleClick);
    </script>
  </body>
</html>
```

&nbsp;  

## 4. 이벤트 핸들러 제거

`addEventListener` 메소드로 등록한 이벤트 핸들러를 제거하려면 `Event.prototype.removeEventListener` 메소드를 사용한다. `removeEventListener` 메소드에 전달할 인수는 `addEventListener` 메소드와 동일하다. 단, `addEventListener` 메소드에 전달한 인수와 일치하지 않으면 이벤트 핸들러가 제거되지 않는다.

```html
<!DOCTYPE>
<html>
  <body>
    <button>Click me!</button>
  
    <script>
      const $button = document.querySelector('button');
      
      const handleClick = () => console.log('button clicked');
      
      $button.addEventListener('click', handleClick);
      $button.removeEventListener('click', handleClick, true); // 제거 실패
      $button.removeEventListener('click', handleClick); // 제거 성공
    </script>
  </body>
</html>
```

`removeEventListener`에 전달한 이벤트 핸들러는 `addEventListener`를 통해 등록한 이벤트 핸들러와 동일한 참조를 가진 함수여야 한다. 따라서 아래와 같이 무명 함수 리터럴로 등록한 이벤트 핸들러는 제거할 수 없다. 이벤트 핸들러를 제거하려면 이벤트 핸들러의 참조를 변수나 자료구조에 저장하고 있어야 한다.

```javascript
// 이벤트 핸들러를 참조할 수 없으므로 제거할 수 없다.
$button.addEventListener('click', () => console.log('button clicked'));
```

단, 이벤트 핸들러 내부에서 `removeEvenetListener`를 사용하여 자신을 제거하는 방법은 가능하다. 이때 이벤트 핸들러는 **단 한번만 호출**된다.

```javascript
$button.addEventListener('click', function handleClick() {
  console.log('button clicked');
  $button.removeEventListener('click', handleClick);
});
```

&nbsp;  

이벤트 핸들러 프로퍼티 방식으로 등록한 이벤트 핸들러는 `removeEventListener`로 제거할 수 없다. 이벤트 핸들러 프로퍼티 방식으로 등록한 이벤트 핸들러를 제거하려면 이벤트 핸들러 프로퍼티에 `null`을 할당한다.

```html
<!doctype html>
<html>
  <body>
    <button>Click me!</button>
    
    <script>
    	const $button = document.querySelector('button');
      
      // 이벤트 핸들러 등록
      $button.onclick = function () {
        console.log('button clicked');
      };
      
      // 이벤트 핸들러 제거
      $button.onclick = null;
    </script>
  </body>
</html>
```

&nbsp;  

## 5. 이벤트 객체

이벤트가 발생하면 **이벤트에 관련한 다양한 정보를 담고 있는 이벤트 객체**가 동적으로 생성된다. 생성된 이벤트 객체는 **이벤트 핸들러의 첫번째 매개 변수에게 전달된다.**

```html
<!doctype>
<html>
  <body>
    <button>Click me!</button>
    <script>
    	const $button = document.querySelector('button');
      
      $button.onclick = function (e) {
        console.log(e); // 이벤트 객체를 출력
      };
    </script>
  </body>
</html>
```

클릭 이벤트에 의해 생성된 이벤트 객체는 이벤트 핸들러의 첫번째 매개 변수 `e`에 암묵적으로 전달된다. 이는 브라우저가 이벤트 핸들러를 호출할 때 이벤트 객체를 인수로 전달하기 때문이다. 따라서 이벤트 객체를 전달 받으려면 이벤트 핸들러 매개 변수 목록에 이벤트 객체를 전달받을 매개 변수를 명시적으로 선언해야한다.

&nbsp;  

### 5.1. 이벤트 객체의 상속 구조

이벤트가 발생하면 **발생한 이벤트의 타입에 따라** 다양한 타입의 **이벤트 객체가 생성**된다. 이벤트 객체는 아래와 같은 상속 구조를 가진다.

<img src="https://user-images.githubusercontent.com/32444914/83104020-dd16a500-a0f2-11ea-9731-b4de3aef60f8.png" width="80%" />

위 그림의 Event, UIEvent, MouseEvent 등은 모두 생성자 함수이다. 따라서 아래와 같이 이벤트 객체를 생성할 수 있다.

```html
<!doctype html>
<html>
  <body>
    <script>
    	// Event 생성자 함수를 호출하여 foo 이벤트 타입의 Event 객체 생성
      let e = new Event('foo');
      
      // FocusEvent 생성자 함수를 호출하여 focus 이벤트 타입의 FocusEvent 객체 생성
      e = new FocusEvent('focus');
      
      // MouseEvent 생성자 함수를 호출하여 click 이벤트 타입의 MouseEvent 객체 생성
      e = new MouseEvent('click');
      
      // KeyboardEvent 생성자 함수를 호출하여 keyup 이벤트 타입의 KeyboardEvent 객체 생성
      e = new KeyboardEvent('keyup');
      
      // InputEvent 생성자 함수를 호출하여 change 이벤트 타입의 InputEvent 객체 생성
      e = new InputEvent('change');
    </script>
  </body>
</html>
```

이처럼 이벤트가 발생하면 생성되는 이벤트 객체도 생성자 함수에 의해 생성되며, 생성자 함수와 더불어 생성되는 프로토타입으로 구성된 프로토타입 체인의 일원이 된다. 예를 들어, click 이벤트가 발생하면 생성되는 MouseEvent 타입의 이벤트 객체는 아래와 같은 프로토타입 체인의 일원이 된다.

<img src="https://user-images.githubusercontent.com/32444914/83104478-c9b80980-a0f3-11ea-8979-c0ffe3bbbad7.png" width="70%" />

이벤트 중 일부는 사용자 행위에 의해 생성된 것이고, 일부는 자바스크립트 코드에 의해 인위적으로 생성된 것이다. 예를 들어, MouseEvent는 사용자가 마우스를 클릭하거나 이동했을 때 발생하는 이벤트이고, CustomEvent는 자바스크립트 코드에 의해 인위적으로 생성한 이벤트이다.

Event 인터페이스는 DOM 내에서 발생한 이벤트를 나타낸다. **Event 인터페이스**에는 모든 이벤트 객체의 **공통 프로퍼티**가 정의되어 있고, FocusEvent, MouseEvent, KeyboardEvent, WheelEvent와 같은 **하위 인터페이스**에는 이벤트 타입에 따라 **고유한 프로퍼티가** 정의되어 있다. 

```html
<!doctype html>
<html>
  <body>
    <input type="text" />
    <input type="checkbox" />
    <button>Click me!</button>
    
    <script>
    	const $input = document.querySelector('input[type=text]');
      const $checkbox = document.querySelector('input[type=checkbox]');
      const $button = document.querySelector('button');
      
      // load 이벤트가 발생하면 Event 타입의 이벤트 객체가 생성된다.
      window.onload = console.log;
      
      // change 이벤트가 발생하면 Event 타입의 이벤트 객체가 생성된다.
      $checkbox.onload = console.log;
      
      // focus 이벤트가 발생하면 FocusEvent 타입의 이벤트 객체가 생성된다.
      $input.onfocus = console.log;
      
      // input 이벤트가 발생하면 InputEvent 타입의 이벤트 객체가 생성된다.
      $input.oninput = console.log;
      
      // keyup 이벤트가 발생하면 KeyboardEvent 타입의 이벤트 객체가 생성된다.
      $input.onkeyup = console.log;
      
      // click 이벤트가 발생하면 MouseEvent 타입의 이벤트 객체가 생성된다.
      $button.onclick = console.log;
    </script>
  </body>
</html>
```

<img src="https://user-images.githubusercontent.com/32444914/83105731-274d5580-a0f6-11ea-8507-a40b4bcec73a.png" width="80%" />

&nbsp;  

### 5.2. 이벤트 객체의 공통 프로퍼티

Event 인터페이스(`Event.prototype`)에 정의되어 있는 이벤트 관련 프로퍼티는 UIEvent, CustomEvent, MouseEvent 등 모든 파생 이벤트 객체에 상속된다. 즉, Event 인터페이스의 모든 이벤트 객체의 공통 프로퍼티를 파생 이벤트 객체에 상속한다. 이벤트 객체의 공통 프로퍼티는 아래와 같다.

| 프로퍼티         | 설명                                                         | 타입          |
| ---------------- | ------------------------------------------------------------ | ------------- |
| type             | 이벤트 타입                                                  | 문자열        |
| target           | 이벤트를 발생시킨 DOM 요소                                   | DOM 요소 노드 |
| currentTarget    | 이벤트 핸들러가 바인딩된 DOM 요소                            | DOM 요소 노드 |
| eventPhase       | 이벤트 전파 단계<br />0: 이벤트 없음<br />1: 캡처링 단계<br />2: 타깃 단계<br />3: 버블링 단계 | 숫자          |
| bubbles          | 이벤트를 버블링으로 전파하는지에 대한 여부                   | 불리언        |
| cancelable       | preventDefault 메소드를 사용하여 이벤트의 기본 동작을 취소할 수 있는지에 대한 여부 | 불리언        |
| defaultPrevented | preventDefault 메소드를 호출하여 이벤트를 취소하였는지에 대한 여부 | 불리언        |
| isTrusted        | 사용자의 행위에 의해 발생한 이벤트인지에 대한 여부           | 불리언        |
| timeStamp        | 현재 문서가 생성되고 이벤트가 발생하기까지 경과한 millisecond | 숫자          |

&nbsp;  

### 5.3. 마우스 정보 취득

click, dbclick, mousedown, mouseup, mousemove, mouseenter, mouseleave 이벤트가 발생하면 생성되는 MouseEvent 타입의 이벤트 객체는 아래와 같은 고유 프로퍼티를 가진다.

**마우스 포인터의 좌표 정보를 나타내는 프로퍼티**

* screenX / screenY
* clientX / clientY
* pageX / pageY
* offsetX / offsetY

**버튼 정보를 나타내는 프로퍼티**

* altKey
* ctrlKey
* shiftKey
* button

&nbsp;  

### 5.4. 키보드 정보 취득

keydown, keyup, keypress 이벤트가 발생하면 생성되는 KeyboardEvent 타입의 이벤트 객체는 아래와 같은 고유 프로퍼티를 가진다.

* altKey
* ctrlKey
* shiftKey
* metaKey
* key
* keyCode

&nbsp;  

## 6. 이벤트 전파

DOM 트리 상에 존재하는 DOM 요소 노드에서 발생한 이벤트는 DOM 트리를 통해 전파된다. 이를 이벤트 전파(event propagation)라고 한다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
  </body>
</html>
```

`ul` 요소의 두번째 자식 요소인 `li` 요소를 클릭하면, 클릭 이벤트가 발생한다. 이때 생성된 **이벤트 객체**는 이벤트를 발생시킨 DOM 요소인 <strong>이벤트 타깃(event target)</strong>을 중심으로 DOM 트리를 통해 전파된다. 이벤트 객체가 전파되는 방향에 따라 아래와 같이 3단계로 구분할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/83134867-f08c3500-a11f-11ea-8527-21b3279bada6.png" width="60%" />

1. 캡처링 단계(capturing phase): 이벤트가 상위 요소에서 하위 요소 방향으로 전파
2. 타깃 단계(target phase): 이벤트가 이벤트 타깃에 도달
3. 버블링 단계(bubbling phase): 이벤트가 하위 요소에서 상위 요소 방향으로 전파

&nbsp;  

이처럼 DOM 트리를 통해 전파되는 이벤트는 이벤트 타깃은 물론 상위 DOM 요소에서도 캐치할 수 있다. 예를 들어, 위 예제의 `ul` 요소에 이벤트 핸들러를 바인딩하면 자신이 발생시킨 이벤트 뿐만 아니라, 하위 요소에서 발생한 이벤트까지 캐치할 수 있다. 하위 요소에서 발생한 이벤트는 버블링되기 때문이다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li id="apple">apple</li>
      <li id="banana">banana</li>
      <li id="orange">orange</li>
    </ul>
    
    <script>
    	const $ul = document.querySelector('ul');
      
      // $ul 요소에 바인딩된 이벤트 핸들러는 버블링 단계의 이벤트를 캐치한다.
      // 따라서 이벤트 핸들러는 $ul 요소와 $ul 요소의 하위 요소에서 발생하여
      // 버블링되는 이벤트를 모두 캐치할 수 있다.
      $ul.onclick = e => {
        console.log(`이벤트 단계: ${e.eventPhase}`);
        console.log(`이벤트 타깃 : ${e.target.nodeName}#${e.target.id}`);
      };
    </script>
  </body>
</html>
```

이벤트 핸들러 어트리뷰트/프로퍼티 방식으로 등록한 이벤트 핸들러는 타깃 단계와 버블링 단계의 이벤트만을 캐치할 수 있다. 하지만 `addEventListener` 메소드 방식으로 등록한 이벤트 핸들러는 버블링 또는 **캡처링** 단계의 이벤트를 선별적으로 캐치할 수 있다. 캡처링 단계의 이벤트를 캐치하려면 `addEventListener`의 세번째 인수로 true를 전달하여 이벤트 핸들러를 등록하면된다.

버블링 단계 또는 캡처링 단계의 모든 이벤트는 이벤트 패스(이벤트가 통과하는 DOM 트리 상의 경로)에 위치한 모든 DOM 요소에서 캐치할 수 있다. 이벤트 패스는 `Event.prototype.composedPath` 메소드로 확인할 수 있다.

&nbsp;  

## 7. 이벤트 위임

이벤트 위임(Event delegation)은 **다수의 하위 요소에 각각 이벤트 핸들러를 등록하는 대신 하나의 상위 요소에 이벤트 핸들러를 등록하는 방법을 말한다.** 하위 요소에서 발생한 이벤트는 버블링 단계에서 부모 요소 방향으로 전파된다. 따라서 상위 요소는 하위 요소에서 발생한 이벤트를 캐치할 수 있다.

아래 예제는 클릭된 `li` 요소에 `active` CSS 클래스를 토글하는 예제이다.

```html
<!doctype html>
<html>
  <head>
  	<style>
      #fruit {
        display: flex;
        list-style: none;
        padding: 0;
      }
      
      #fruits li {
        width: 100px;
        cursor: pointer;
      }
      
      #fruits .active {
        color: red;
        text-decoration: underline;
      }
    </style>
  </head>
  <body>
    <ul id="fruits">
      <li id="apple" class="active">apple</li>
      <li id="banana">banana</li>
      <li id="orange">orange</li>
    </ul>
    
    <script>
    	const $fruits = document.querySelector('#fruits');
      
      // 이벤트 위임: 상위 요소(ul#fruits)는 하위 요소의 이벤트를 캐치할 수 있다.
      $fruits.onclick = ({ target }) => {
        if (!target.matches('#fruits li')) return;
        
        [...$fruits.children].forEach($fruit => {
          $fruit.classList.toggle('active', $fruit === target)
        });
      };
    </script>
  </body>
</html>
```

이벤트 위임을 통해 하위 요소에서 발생한 이벤트를 처리할 때 주의할 것은 상위 요소에 이벤트 핸들러를 등록하기 때문에 **이벤트 타깃(이벤트를 실제로 발생시킨 DOM 요소)과 currentTarget(이벤트 핸들러가 바인딩되어 있는 DOM 요소)가 다를 수 있다는 것**이다. 따라서 이벤트에 반응이 필요한 요소에 한정하여 이벤트 핸들러가 실행되도록 이벤트 타깃을 검사할 필요가 있다.

**포커스 이벤트 focus, blur는 이벤트가 버블링되지 않는다.** 따라서 하위 요소에서 focus, blur 이벤트를 발생시키는 경우, 이벤트 위임을 사용할 수 없다.

```html
<!doctype html>
<html>
  <body>
    <div class="container">
      <input type="text">
    </div>
    
    <script>
    	const $container = document.querySelector('.container');
      
      // input 이벤트는 버블링되므로 상위 요소에 이벤트 위임을 할 수 있다.
      $container.addEventListener('input', e => {
        console.log(e); // InputEvent { ... }
      });
      
      // focus 이벤트는 버블링되지 않으므로 상위 요소에 이벤트 위임을 할 수 없다.
      $container.addEventListener('focus', e => {
        console.log(e); // 절대로 이벤트가 발생하지 않는다.
      });
      
      // blur 이벤트는 버블링되지 않으므로 상위 요소에 이벤트 위임을 할 수 없다.
      $container.addEventListener('blur', e => {
        console.log(e); // 절대로 이벤트가 발생하지 않는다.
      });
    </script>
  </body>
</html>
```

&nbsp;  

## 8. 기본 동작의 변경

### 8.1. 기본 동작 중단

DOM 요소마다 기본 동작이 있다. 예를 들어, a 요소를 클릭하면 href 어트리뷰트에 지정된 링크로 이동하고, checkbox 또는 radio 요소를 클릭하면 체크 또는 해제된다.

이벤트 객체의 `preventDefault` 메소드는 이러한 DOM 요소의 기본 동작을 중단시킨다.

```html
<!doctype html>
<html>
  <body>
    <a href="https://www.google.com">go</a>
    <input type="checkbox">
    <script>
      document.querySelector('a').onclick = e => {
        // a 요소의 기본 동작을 중단한다.
        e.preventDefault();
      };
      
      document.querySelector('input[type=check]').onchange = e => {
      	// checkbox 요소의 기본 동작을 중단한다.
        e.preventDefault();
      };
    </script>
  </body>
</html>
```

&nbsp;  

### 8.2. 이벤트 전파 방지

이벤트 객체의 `stopPropagation` 메소드는 이벤트 전파를 중지시킨다. 아래 예제를 살펴보자.

```html
<!doctype html>
<html>
  <body>
    <div class="container">
      <button>Click me</button>
    </div>
    
    <script>
      // 버튼 요소에 click 이벤트 핸들러를 등록한 후 이벤트 전파를 중지시켰다.
      document.querySelector('button').onclick = e => {
        console.log('button');
        e.stopPropagation();
      };
      
      // 컨테이너 요소에 click 이벤트 핸들러를 등록했지만 이벤트를 캐치할 수 없다.
    	document.querySelector('.container').onclick = () => {
        console.log('div');
      };
    </script>
  </body>
</html>
```

이처럼 상위 요소와 하위 요소의 이벤트를 별도로 처리하기 위해 이벤트의 전파를 중지시키기도 한다.

&nbsp;  

## 9. 이벤트 핸들러 내부의 this

### 9.1. 이벤트 핸들러 어트리뷰트

이벤트 핸들러 어트리뷰트 방식의 경우, 이벤트 핸들러 내부의 this는 전역 객체 window를 가리킨다.

```html
<!doctype html>
<html>
  <body>
    <button onclick="handleClick()">Click me</button>
    <script>
      function handleClick() {
        console.log(this); // window
      }
    </script>
  </body>
</html>
```

질문. 위 코드는 아래 코드와 동치인가?

```html
<!doctype html>
<html>
  <body>
    <!-- <button onclick="console.log(this);">Click me</button -->
    <button>Click me</button>
    <script>
      document.querySelector('button').onclick = function () {
        handleClick(); // 일반 함수로 호출되어 this는 전역 객체 window를 가리킨다.
      };
      
      function handleClick() {
        console.log(this);
      }
    </script>
  </body>
</html>
```

&nbsp;  

### 9.2. 이벤트 핸들로 프로퍼티와 addEventListener 메소드

이벤트 핸들러 프로퍼티 방식과 addEventListener 메소드 방식 모두 이벤트 핸들러 내부의 this는 이벤트를 바인딩한 DOM 요소(currentTarget)를 가리킨다. 

```html
<!doctype html>
<html>
  <body>
    <button class="btn1">Button 1</button>
    <button class="btn2">Button 2</button>
    
    <script>
    	const $button1 = document.querySelector('.btn1');
      const $button2 = document.querySelector('.btn2');
      
      // 이벤트 핸들러 프로퍼티
      $button1.onclick = function (e) {
        console.log(this); // $button1
        console.log(e.currentTarget); // $button1
      };
      
      // addEventListener 메소드
      $button2.addEventListener('click', function (e) {
        console.log(this); // $button2
        console.log(e.currentTarget); // $button2
      });
    </script>
  </body>
</html>
```

화살표 함수로 정의한 이벤트 핸들러 내부의 this는 상위 컨텍스트의 this를 가리킨다. 화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다.

```html
<!doctype html>
<html>
  <body>
    <button class="btn1">Button 1</button>
    <button class="btn2">Button 2</button>
    
    <script>
    	const $button1 = document.querySelector('.btn1');
      const $button2 = document.querySelector('.btn2');
      
      // 이벤트 핸들러 프로퍼티
      $button1.onclick = e => {
        console.log(this); // window
        console.log(e.currentTarget); // $button1
      };
      
      // addEventListener 메소드
      $button2.addEventListener('click', e => {
        console.log(this); // window
        console.log(e.currentTarget); // $button2
      });
    </script>
  </body>
</html>
```

&nbsp;  

클래스에서 이벤트 핸들러를 바인딩하는 경우, this에 주의해야 한다. 아래 예제는 이벤트 핸들러 프로퍼티 방식을 사용하고 있으나 addEventListener 메소드 방식을 사용하는 경우와 동일하다.

```html
<!doctype html>
<html>
  <body>
    <button class="btn">Click me</button>
    <script>
    	class App {
        constructor() {
          this.$button = document.querySelector('.btn');
          this.$button.onclick = this.sayHi;
          // sayHi 메소드를 이벤트 핸들러로 등록
          // 이벤트 핸들러 sayHi 내부의 this는 인스턴스가 아닌
          // DOM 요소(this.$button)를 가리킨다.
        }
        
        sayHi() {
          // 문맥상 이곳의 this는 인스턴스이다.
          console.log(this);
        }
      }
      
      new App();
    </script>
  </body>
</html>
```

위 예제의 `sayHi` 메소드 내부의  this는 클래스가 생성할 인스턴스를 가리키지 않고 `$button`을 가리킨다. 때문에 `sayHi` 메소드를 이벤트 핸들러 프로퍼티에 바인딩할 때 `bind` 메소드를 사용해 this(인스턴스)를 전달하여 `sayHi` 메소드 내부의 this가 인스턴스를 가리키도록 해야한다.

```html
<!doctype html>
<html>
  <body>
    <button class="btn">Click me</button>
    <script>
    	class App {
        constructor() {
          this.$button = document.querySelector('.btn');
          
          // sayHi 메소드 내부의 this가 인스턴스를 가리키도록 한다.
          this.$button.onclick = this.sayHi.bind(this);
        }
        
        sayHi() {
          console.log(this);
        }
      }
      
      new App();
    </script>
  </body>
</html>
```

또는 클래스 필드에 할당한 화살표 함수를 이벤트 핸들러로 등록하면, 이벤트 핸들러 내부의 this가 인스턴스를 가리키도록 할 수도 있다. 하지만 이때 이벤트 핸들러 `sayHi`는 프로토타입 메소드가 아닌 인스턴스 메소드가 된다.

```html
<!doctype html>
<html>
  <body>
    <button class="btn">Click me</button>
    <script>
    	class App {
        
        constructor() {
          this.$button = document.querySelector('.btn');
          this.$button.onclick = this.sayHi;
        }
        
        // sayHi는 인스턴스 메소드이며 화살표 함수로 정의되었다.
        // 화살표 함수 내부의 this는 자신이 정의된 위치의 this를 따른다.
        sayHi = () =>  {
          // 문맥상 이곳의 this는 인스턴스이다.
          console.log(this);
        }
      }
      
      new App();
    </script>
  </body>
</html>
```

&nbsp;  

## 10. 이벤트 핸들러에 인수 전달

함수에게 인수를 전달하려면 함수를 호출할 때 전달해야 한다. 이벤트 핸들러 어트리뷰트 방식은 함수 호출문을 사용할 수 있기 때문에 인수를 전달할 수 있지만, 이벤트 핸들러 프로퍼티와 addEventListener 메소드를 사용하는 경우, 브라우저가 이벤트 핸들러를 호출하기 때문에 함수 호출문이 아닌 함수 자체를 등록해야 한다. 따라서 인수를 전달할 수 없다.

그러나 인수를 전달할 방법이 전혀 없는 것은 아니다. 아래 예제와 같이 이벤트 핸들러 내부에서 함수를 호출하면서 인수를 전달할 수 있다.

```html
<!doctype html>
<html>
  <body>
    <button>Click me</button>
    <script>
    	const $button = document.querySelector('button');
      const sayHi = name => {
        console.log(name);
      };
      
      $button.onclick = e => {
        console.log(e.target);
        sayHi('Jin');
      };
    </script>
  </body>
</html>
```

또는 이벤트 핸들러를 반환하는 함수를 호출하면서 인수를 전달할 수도 있다.

```html
<!doctype html>
<html>
  <body>
    <button>Click me</button>
    <script>
    	const $button = document.querySelector('button');
      const sayHi = name => e => {
        console.log(e.target);
        console.log(name);
      };
      
      $button.onclick = sayHi('Jin');
    </script>
  </body>
</html>
```

`sayHi` 함수는 함수를 반환한다. 따라서 `$button.onclick`에는 결국 `sayHi` 함수가 반환한 함수가 바인딩된다.

&nbsp;  

## 11. 커스텀 이벤트

### 11.1. 커스텀 이벤트 생성

이벤트 객체의 상속 구조에서 살펴본 바와 같이, **이벤트 객체는** Event, UIEvent, MouseEvent와 같은 생성자 함수로 생성할 수 있다.

이벤트가 발생하면 생성되는 이벤트 객체는 이벤트의 종류에 따라 이벤트 타입이 결정되지만 Event, UIEvent, MouseEvent와 같은 생성자 함수로 이벤트 객체를 생성하는 경우, 이벤트 타입을 명시적으로 지정할 수 있다. 이를 통해 [이벤트 타입](https://developer.mozilla.org/en-US/docs/Web/Events)에서 살펴본 이벤트 타입 이외의 이벤트를 생성할 수 있다. 이를 **커스텀 이벤트**라 한다.

이벤트 생성자 함수의 인수로 전달하는 이벤트 타입은 기존 이벤트 타입을 사용할 수 있다.

```javascript
// KeyboardEvent 생성자 함수로 keyup 이벤트 타입의 커스텀 이벤트 객체를 생성
const keyboardEvent = new KeyboardEvent('keyup');
console.log(keyboardEvent.type); // keyup
```

생성된 **커스텀 이벤트 객체는 버블링되지 않으며 취소할 수도 없다**. 즉, bubbles와 cancelable 프로퍼티의 값이 false로 기본 설정된다.

```javascript
// MouseEvent 생성자 함수로 click 이벤트 타입의 커스텀 이벤트 객체를 생성
const customEvent = new MouseEvent('click');
console.log(customEvent.type); // click
console.log(customEvent.bubbles); // false
console.log(customEvent.cancelable); // false
```

또는 임의 문자열을 사용하여 기존의 이벤트 타입이 아닌 **새로운 이벤트 타입을 지정**할 수도 있다. 이 경우, 일반적으로 CustomEvent 이벤트 생성자 함수를 사용한다 (커스텀 이벤트 디스패치).

```javascript
// CustomEvent 생성자 함수로 foo 이벤트 타입의 커스텀 이벤트 객체를 생성
const customEvent = new CustomEvent('foo');
console.log(customEvent.type); // foo
```

bubbles 또는 cancelable 프로퍼티를 true로 설정하려면 이벤트 생성자 함수의 두번째 인수로 bubbles 또는 cancelable 프로퍼티를 가진 객체를 전달한다.

```javascript
// MouseEvent 생성자 함수로 click 이벤트 타입의 커스텀 이벤트 객체를 생성
const customEvent = new MouseEvent('click', {
  bubbles: true,
  cancelable: true
});

console.log(customEvent.bubbles); // true
console.log(customEvent.cancelable); // true
```

bubbles 또는 cancelable 프로퍼티뿐만 아니라 이벤트 생성자 함수에 따라 생성된 이벤트의 특성에 맞는 프로퍼티를 설정할 수 있다.

```javascript
// MouseEvent 생성자 함수로 click 이벤트 타입의 커스텀 이벤트 객체를 생성
const mouseEvent = new MouseEvent('click', {
  bubbles: true,
  cancelable: true,
  clientX: 50,
  clientY: 100
});

console.log(mouseEvent.clientX); // 50
console.log(mouseEvent.clientY); // 100
```

이벤트 **생성자 함수로 생성한 커스텀 이벤트는 isTrusted 프로퍼티의 값이 언제나 false**이다. 커스텀 이벤트가 아닌 사용자의 행위에 의해 생성된 이벤트 객체의 isTrusted 프로퍼티 값은 언제나 true이다.

```javascript
// InputEvent 생성자 함수로 foo 이벤트 타입의 커스텀 이벤트 객체를 생성
const customEvent = new InputEvent('foo');
console.log(customEvent.isTrusted); // false
```

&nbsp;  

### 11.2. 커스텀 이벤트 디스패치

생성된 커스텀 이벤트는 dispatchEvent 메소드로 디스패치(이벤트를 발생시키는 행위)할 수 있다.

```html
<!doctype html>
<html>
  <body>
    <button class="btn">Click me</button>
    <script>
    	const $button = document.querySelector('.btn');
      
      // 커스텀 이벤트 생성
      const customEvent = new MouseEvent('click');
      
      // click 커스텀 이벤트 핸들러 등록
      // 커스텀 이벤트를 디스패치하기 이전에 이벤트 핸들러를 등록해야 한다.
      $button.addEventListener('click', e => {
        console.log(e);
        e.target.textContent = 'Clicked!';
      });
      
      // 커스텀 이벤트 디스패치(동기적)
      $button.dispatchEvent(customEvent);
    </script>
  </body>
</html>
```

일반적으로 이벤트는 비동기적으로 발생하지만, <strong>`dispatchEvent` 메소드는 커스텀 이벤트를 동기적으로 발생시킨다.</strong> 따라서  `dispatchEvent` 메소드로 이벤트를 디스패치하기 전에 커스텀 이벤트를 처리할 이벤트 핸들러를 등록해야 한다.

기존의 이벤트 타입이 아닌 새로운 이벤트 타입을 지정하여 이벤트 객체를 생성한 경우, 일반적으로  `CustomEvent` 이벤트 생성자 함수를 사용한다.

```javascript
// CustomEvent 생성자 함수로 foo 이벤트 타입의 커스텀 이벤트 객체 생성
const customEvent = new CustomEvnet('foo');
console.log(customEvent.type); // foo
```

이때 **CustomEvent 이벤트 생성자 함수에는 2번째 인수로 이벤트와 함께 전달하고 싶은 정보를 담은 `detail` 프로퍼티를 포함하는 객체를 전달할 수 있다.** 이 정보는 이벤트 객체의 `detail` 프로퍼티에 담겨 전달된다.

```html
<!doctype html>
<html>
  <body>
    <button class="btn">Click me</button>
    <script>
    	const $button = document.querySelector('.btn');
      
      // CustomEvent 생성자 함수로 foo 이벤트 타입의 커스텀 이벤트 객체를 생성
      const customEvent = new CustomEvent('foo', {
        detail: { message: 'Hello' } // 이벤트와 함께 전달하고 싶은 정보
      });
      
      // click 커스텀 이벤트 핸들러 등록
      // 커스텀 이벤트를 디스패치하기 이전에 이벤트 핸들러를 등록해야 한다.
      $button.addEventListener('foo', e => {
        // e.detail에는 CustomEvent 함수의 두번째 인수로 전달한 정보가 담겨 있다.
        e.target.textContent = e.detail.message;
      });
      
      // 커스텀 이벤트 디스패치
      $button.dispatchEvent(customEvent);
    </script>
  </body>
</html>
```

기존의 이벤트 타입이 아닌 새로운 이벤트 타입을 지정하여 커스텀 이벤트 객체를 생성한 경우, 이벤트 핸들러 등록은 반드시 `addEventListener` 메소드를 사용해야 한다. 새로운 이벤트 타입(ex. `foo`) 에 대한 이벤트 핸들러 어트리뷰트 / 프로퍼티가 존재하지 않기 때문이다 (ex. `onfoo`).

&nbsp;  

## 참고 자료

* [poiemaweb.com - 이벤트](https://poiemaweb.com/fastcampus/event)



















