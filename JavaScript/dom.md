# DOM

브라우저의 렌더링 엔진은 HTML 문서를 파싱하여 DOM을 생성한다.

**DOM(Document Object Model)은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메소드를 제공하는 트리 자료 구조이다.**

&nbsp;  

## 1. 노드

### 1.1. HTML 요소와 노드 객체

* HTML 요소는 HTML 문서를 구성하는 개별적인 요소를 의미한다.
* HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환된다.
* 요소의 어트리뷰트는 어트리뷰트 노드로, 요소의 텍스트 컨텐츠는 텍스트 노드로 변환된다.
* DOM은 (HTML 요소들의 중첩 관계를 반영하여) HTML 요소를 객체화한 모든 노드 객체를 포함하는 트리 자료 구조이다.

&nbsp;  

<strong>HTML 요소(HTML element)</strong>는 HTML 문서를 구성하는 개별적인 요소를 의미한다. HTML 요소는 렌더링 엔진에 의해 파싱되어 **DOM을 구성하는 요소 노드 객체로 변환된다.** 이때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로, HTML 요소의 텍스트 컨텐츠는 텍스트 노드로 변환된다.

<img src="https://user-images.githubusercontent.com/32444914/83388414-5f6fd380-a429-11ea-886b-dc85a67d3825.png" width="60%" />

HTML 문서는 HTML 요소들의 집합으로 이루어지며, HTML 요소는 **중첩 관계**를 가진다. 즉, HTML 요소의 컨텐츠 영역(시작 태그와 종료 태그 사이)에는 텍스트 뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이때 HTML 요소 간에는 중첩 관계에 의해 계층적인 부자(parent-child) 관계가 형성된다. 이러한 **HTML 요소 간의 부자 관계를 반영하여 HTML 문서의 구성 요소인 HTML 요소를 객체화한 모든 노드 객체를 트리 자료 구조로 구성**한다.

> **트리 자료 구조**
>
> 트리 자료 구조(tree data structure)는 노드(node)들의 계층 구조로 이루어진다. 즉, 트리 자료 구조는 부모 노드(parent node)와 자식 노드(child node)로 구성되어 노드 간의 계층적 구조(부자, 형제 관계)를 표현하는 비선형 자료 구조를 말한다.
>
> 트리 자료 구조는 하나의 최상위 노드에서 시작한다. 최상위 노드는 부모 노드가 없으며 루트 노드(root node)라 하다. 루트 노드는 0개 이상의 자식 노드를 가진다. 자식 노드가 없는 노드를 리프 노드(leaf node)라 한다.

<img src="https://user-images.githubusercontent.com/32444914/83388997-6814d980-a42a-11ea-8610-76b6a744f945.png" width="60%" />

&nbsp;  

이 노드 객체들로 구성된 트리 자료 구조를 <strong>DOM(Document Object Model)</strong>이라 한다. 노드 객체의 트리로 구조화되어 있기 때문에 DOM을 **DOM 트리**라고 부르기도 한다.

&nbsp;  

### 1.2. 노드 객체의 타입

* 노드 객체는 종류가 있고 상속 구조를 가진다.
* 노드 객체의 종류([노드 타입](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType))는 총 12가지이다. 그 중 중요한 4가지 타입은 아래와 같다.
  * 문서 노드
  * 요소 노드
  * 어트리뷰트 노드
  * 텍스트 노드
* 

예를 들어 다음 HTML 문서를 렌더링 엔진이 파싱한다고 생각해보자.

```html
<!doctype html>
<html>
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
    <script src="appl.js"></script>
  </body>
</html>
```

렌더링 엔진은 위 HTML 문서를 파싱하여 아래와 같은 DOM을 생성한다.

<img src="https://user-images.githubusercontent.com/32444914/83391198-153d2100-a42e-11ea-9daf-887bf7577e3b.png" width="70%" />

> **공백 텍스트 노드**
>
> 정확히 말하자면 위 그림에는 공백 텍스트 노드가 생략되어 있다. HTML 요소 사이의 개행이나 공백은 텍스트 노드가 된다.

&nbsp;  

이처럼 DOM은 노드 객체의 계층적인 구조로 구성된다. 노드 객체는 종류가 있고 상속 구조를 갖는다. 노드 객체는 총 12개의 종류([노드 타입](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType))가 있다. 이 중 중요한 노드 타입은 아래와 같이 4가지이다.

&nbsp;  

**1. 문서 노드**

문서 노드(document node)는 DOM 트리의 최상위에 존재하는 루트 노드로서 **document 객체를 가리킨다.** document 객체는 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체로서 전역 객체 window의 document 프로퍼티에 바인딩되어 있다. 따라서 `window.document` 또는 `document`로 참조할 수 있다.

브라우저 환경의 모든 자바스크립트 코드는 script 태그에 의해 분리되어 있어도 하나의 전역 객체 window를 공유한다. 따라서 모든 자바스크립트 코드는 전역 객체 window의 document 프로퍼티에 바인딩되어 있는 하나의 document 객체를 바라본다. 즉, **HTML 문서 당 document 객체는 유일하다.**

document 객체는 DOM 트리의 루트 노드이므로 DOM 트리의 노드들에 접근하기 위한 진입점(entry point) 역할을 담당한다. 즉, 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다.

&nbsp;  

**2. 요소 노드**

요소 노드(element node)는 HTML 요소를 가리키는 객체이다. 요소 노드는 HTML 요소 간의 중첩에 의해 부자 관계를 가지며 이 부자 관계를 통해 정보를 구조화한다. 따라서 요소 노드는 **문서의 구조를 표현**한다고 할 수 있다.

&nbsp;  

**3. 어트리뷰트 노드**

어트리뷰트 노드(attribute node)는 HTML 요소의 어트리뷰트를 가리키는 객체이다. **어트리뷰트 노드는** 어트리뷰트가 지정된 HTML 요소의 **요소 노드와 형제(sibling) 관계를 가진다.** 따라서 요소 노드에 접근하면 어트리뷰트 노드에 접근하여 어트리뷰트를 참조하거나 변경할 수 있다.

&nbsp;  

**4. 텍스트 노드**

텍스트 노드(text node)는 HTML 요소의 텍스트를 가리키는 객체이다. **텍스트 노드는 요소 노드의 자식 노드**이며 자신의 **자식 노드를 가질 수 없는 리프 노드(leaf node)이다.** 즉, 텍스트 노드는 DOM 트리의 최종단이다. 요소 노드가 문서의 구조를 표현한다면 텍스트 노드는 **문서의 정보를 표현**한다고 할 수 있다.

위 4가지 노드 타입 이외에도 주석을 위한 Comment 노드, DOCTYPE을 위한 DocumentType 노드, 복수의 노드를 생성하여 추가할 때 사용하는 DocumentFragment 노드 등 총 12개의 타입이 있다.

&nbsp;  

### 1.3. 노드 객체의 상속 구조

DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있다. 이를 통해 노드 객체는 자신의 부모 또는 자식을 탐색할 수 있으며 자신의 컨텐츠를 조작할 수도 있다.

DOM을 구성하는 노드 객체는 ECMAScript 사양에 정의된 표준 빌트인 객체(standard built-in object)가 아니라 브라우저 환경에서 추가적으로 제공하는 호스트 객체(host object)이다. 하지만 **노드 객체도 자바스크립트 객체이므로 프로토타입에 의한 상속 구조를 가진다.** 노드 객체의 상속 구조는 아래와 같다.

<img src="https://user-images.githubusercontent.com/32444914/83393073-26d3f800-a431-11ea-8f92-bb2f25b25cdc.png" width="70%" />

위 그림과 같이 모든 노드 객체는 Object, EventTarget, Node 인터페이스를 상속받는다. 추가적으로 문서 노드는 Document, HTMLDocument 인터페이스를 상속받고 어트리뷰트 노드는 Attr, 텍스트 노드는 CharacterData 인터페이스를 각각 상속 받는다.

요소 노드는 Element 인터페이스를 상속받는다. 또한 요소 노드는 추가적으로 HTMLElement와 태그의 종류 별로 세분화된 HTMLHeadElement, HTMLBodyElement 등의 인터페이스를 상속받는다.

예를 들어 input 요소를 파싱하여 객체화한 input 요소 노드 객체는 HTMLInputElement, HTMLElement, Element, Node, EventTarget, Object의 prototype에 바인딩되어 있는 프로토타입 객체를 상속받는다. 즉, input **요소 노드 객체는 프로토타입 체인에 있는 모든 프로토타입의 프로퍼티나 메소드를 상속받아 사용할 수 있다.**

<img src="https://user-images.githubusercontent.com/32444914/83393614-05bfd700-a432-11ea-8c35-e56aeb68daf1.png" width="60%" />

배열이 객체인 동시에 배열인 것처럼, input 요소 노드 객체도 아래와 같이 다양한 특성을 갖는 객체이며 이러한 특성을 나타내는 기능을 상속 관계를 통해 구분하여 제공한다.

| input 요소 노드 객체의 특성                                  | 프로토타입을 제공하는 객체 |
| ------------------------------------------------------------ | -------------------------- |
| 객체                                                         | Object                     |
| 이벤트를 발생시키는 객체                                     | EventTarget                |
| 트리 자료 구조의 노드 객체                                   | Node                       |
| 브라우저가 렌더링할 수 있는 웹 문서의 요소(HTML, XML, SVG)를 표현하는 객체 | Element                    |
| 웹 문서의 요소 중에서 HTML 요소를 표현하는 객체              | HTMLElement                |
| HTML 요소 중 input 요소를 표현하는 객체                      | HTMLInputElement           |

노드 객체의 상속 구조는 개발자 도구의 Elements 패널 하단의 Properties 패널에서 확인할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/83394177-13c22780-a433-11ea-8e0f-6949796ac75d.png" width="80%" />

노드 객체는 공통적인 기능도 있지만 **노드 객체의 종류에 따라 고유한 기능**도 갖는다. 예를 들어, 모든 노드 객체는 공통적으로 이벤트를 발생시킨다. 이벤트에 관련된 기능은 EventTarget 인터페이스가 제공한다.

또한 모든 노드 객체는 트리 자료 구조의 노드로서 공통적으로 트리 탐색 기능이나 노드 정보 제공 기능이 필요하다. 이같은 노드 관련 기능은 Node 인터페이스가 제공한다.

HTML 요소가 객체화된 요소 노드 객체는 HTML 요소가 갖는 공통적인 기능도 있다. 예를 들어 input 요소 노드 객체와 div 요소 노드 객체는 모두 HTML 요소의 스타일을 나타내는 style 프로퍼티가 있다. 이같이 HTML 요소가 가지는 공통적인 기능은 HTMLElement 인터페이스가 제공한다.

하지만 요소 노드 객체는 HTML 요소의 종류에 따라 고유한 기능도 있다. 예를 들어 input 요소 노드 객체는 value 프로퍼티가 필요하지만, div 요소 노드는 value 프로퍼티가 필요하지 않다. 따라서 필요한 기능을 제공하는 인터페이스(HTMLInputElement, HTMLDivElement 등)가 HTML 요소의 종류에 따라 각각 다르다.

이처럼 노드 객체는 공통된 기능일수록 프로토타입 체인의 상위에, 개별적인 고유 기능일수록 프로토타입 체인의 하위에 프로토타입 체인을 구축하여 노드 객체에 필요한 기능(프로퍼티와 메소드)을 상속 구조를 통해 가진다.

이와 같이 **DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류에 따라 상속을 통해 자신에 필요한 기능, 즉 프로퍼티와 메소드의 집합인 DOM API(Application Programming Interface)를 제공한다. DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다.** 

&nbsp;  

## 2. 요소 노드 취득

HTML의 구조나 내용 또는 스타일 등을 동적으로 조작하려면 먼저 요소 노드를 취득해야 한다. 텍스트 노드나  어트리뷰트 노드를 조작하고자 할 때도 마찬가지다.

예를 들어, HTML 문서 내의 h1 요소의 텍스트를 변경하고 싶은 경우 먼저 DOM 트리 내에 존재하는 h1 요소 노드를 취득할 필요가 있다. 그리고 취득한 요소 노드의 자식 노드인 텍스트 노드를 변경하면 해당 h1 요소의 텍스트가 변경된다.

이처럼 요소 노드의 취득은 HTML 요소를 조작하는 시작점이다. 이를 위해 DOM은 요소 노드를 취득할 수 있는 다양한 메소드를 제공한다.

&nbsp;  

### 2.1. id를 이용한 요소 노드 취득

<strong>`Document.prototype.getElementbyId(id)`</strong>

* 인수로 전달한 id 어트리뷰트 값을 가지는 하나의 요소 노드를 탐색하여 반환
* Document.prototype의 프로퍼티이므로 반드시 문서 노드 document를 통해 호출
* HTML 문서 내에 중복된 id 값을 가지는 요소가 여러 개 존재할 경우 첫번째 요소 노드만 반환
* 인수로 전달된 id 값을 가지는 요소가 없는 경우 null을 반환

&nbsp;  


**주의 사항**

id 값은 HTML 문서 내에서 유일한 값이어야 하며 class 어트리뷰트와는 달리 공백 문자로 구분하여 여러 개의 값을 가질 수 없다. 단, HTML 문서 내에 중복된 id 값을 가지는 요소가 여러 개 존재하더라도 어떠한 에러도 발생하지 않는다.

HTML 요소에 id 어트리뷰트를 부여하면 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과(side effect)가 있다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo"></div>
    <script>
    	// id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당
      console.log(foo); // <div id="foo"></div>
      
      // 암묵적 전역으로 생성된 전역 프로퍼티는 삭제되지만 전역 변수는 삭제되지 않는다.
      delete foo;
      console.log(foo); // <div id="foo"></div>
    </script>
  </body>
</html>
```

단, id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 이 전역 변수에 노드 객체가 재할당되지 않는다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo"></div>
    <script>
    	let foo = 1;
      // id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 노드 객체가 재할당되지 않는다.
      	console.log(foo); // 1
    </script>
  </body>
</html>
```

&nbsp;  

### 2.2. 태그 이름을 이용한 요소 노드 취득

<strong>`Document.prototye.getElementsByTagName(tagName)`</strong>

<strong>`Element.prototype.getElementsByTagName(tagName)`</strong>

* 인수로 전달한 태그 이름을 갖는 **모든 요소 노드를 탐색하여 반환**
* 여러 개의 요소 노드 객체를 가지는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환
* HTMLCollection 객체는 유사 배열 객체이자 이터러블이다.
* `Document.prototype.getElementsByTagName` 메소드는 문서 노드(document)를 통해 호출하며 HTML 문서 전체에서 요소 노드를 탐색하여 반환
* `Element.prototype.getElementsByTagName` 메소드는 특정 요소 노드를 통해 호출하며 특정 요소 노드 범위 내의 요소 노드를 탐색하여 반환
* 만약 인수로 전달된 태그 이름을 가지는 요소가 존재하지 않는 경우, 빈 HTMLCollection 객체를 반환

&nbsp;  

### 2.3. class를 이용한 요소 노드 취득

<strong>`Document.prototype.getElementsByClassName(className)`</strong>

<strong>`Element.prototype.getElementsByClassName(className)`</strong>

* 인수로 전달한 class 어트리뷰트 값을 가지는 모든 요소 노드를 탐색하여 반환
* 인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class를 지정할 수 있다.
* 여러 개의 요소 노드 객체를 가지는 DOM 콜렉션 객체인 HTMLCollection 객체를 반환
* `Document.prototype.getElementsByClassName` 메소드는 문서 노드(document)를 통해 호출하며 HTML 문서 전체에서 요소 노드를 탐색하여 반환
* `Element.prototype.getElementsByClassName(className)` 메소드는 특정 요소 노드를 통해 호출하며 특정 요소 노드 범위 내의 요소 노드를 탐색하여 반환
* 만약 인수로 전달된 class 값을 가지는 요소가 존재하지 않는 경우, 빈 HTMLCollection 객체를 반환

&nbsp;  

### 2.4. CSS 선택자를 이용한 요소 노드 취득

<strong>`Document.prototype.querySelector(cssSelector)`</strong>

<strong>`Element.prototype.querySelector(cssSelector)`</strong>

* 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 탐색하여 반환
* 만약 인수로 전달한 CSS 선택자를 만족하는 요소 노드가 여러 개인 경우, 첫번째 요소 노드만 반환
* 인수로 전달한 CSS 선택자를 만족시키는 요소가 존재하지 않는 경우, null을 반환
* `Document.prototype.querySelector` 메소드는 문서 노드(document)를 통해 호출하며 HTML 문서 전체에서 요소 노드를 탐색하여 반환
* `Element.prototype.querySelector` 메소드는 특정 요소 노드 범위 내의 요소 노드를 탐색하여 반환
* 인수로 전달한 CSS 선택자가 문법에 맞지 않는 경우, DOMException 에러가 발생한다.

&nbsp;  

<strong>`Document.prototype.querySelectorAll(cssSelector)`</strong>

<strong>`Element.prototype.querySelectorAll(cssSelector)`</strong>

* 인수로 전달한 CSS 선택자를 만족하는 모든 요소 노드를 탐색하여 반환
* 여러 개의 요소 노드 객체를 가지는 DOM 컬렉션 객체인 NodeList 객체를 반환
* 인수로 전달된 CSS 선택자를 만족시키는 요소가 존재하지 않는 경우, 빈 NodeList 객체를 반환
* `Document.prototype.querySelectorAll` 메소드는 문서 노드(document)를 통해 호출하며 HTML 문서 전체에서 요소 노드를 탐색하여 반환
* `Element.prototype.querySelectorAll` 메소드는 특정 요소 노드 범위 내의 요소 노드를 탐색하여 반환
* 인수로 전달한 CSS 선택자가 문법에 맞지 않는 경우, DOMException 에러가 발생한다.

&nbsp;  

### 2.5. 요소 노드 취득 가능 여부 확인

<strong>`Element.prototype.matches(cssSelector)`</strong>

* 인수로 전달된 CSS 선택자에 의해 특정 요소 노드를 탐색 가능한지 확인
* 이벤트 위임에 사용

&nbsp;  

### 2.6. HTMLCollection과 NodeList

HTMLCollection과 NodeList는 DOM API가 **여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체**이다. **HTMLCollection과 NodeList는 모두 유사 배열 객체이자 이터러블이다.** 따라서 for...of 문으로 순회할 수 있으며 스프레드 문법을 사용해 간단히 배열로 변환할 수 있다.

HTMLCollection과 NodeList의 중요한 특징은 **노드 객체의 상태 변화를 실시간으로 반영하는 살아있는(live) 객체**라는 것이다. HTMLCollection은 언제나 live 객체로 동작한다. 단, NodeList는 대부분의 경우 노드 객체의 상태를 정적으로 유지하는 non-live 객체로 동작하지만, 경우에 따라 live 객체로 동작할 때가 있다(ex. childNodes 프로퍼티).

따라서 **노드 객체의 상태 변경과 상관 없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList를 배열로 변환하여 사용하는 것이 좋다.** HTMLCollection과 NodeList 객체가 메소드를 제공하기는 하지만, 배열만큼 다양한 기능을 제공하지는 않는다(ex. 고차 함수).

HTMLCollection과 NodeList는 모두 유사 배열 객체이며 이터러블이다. 따라서 스프레드 무법을 사용하여 간단히 배열로 변환할 수 있다.

&nbsp;  

## 3. 노드 탐색

요소 노드를 취득한 다음, 취득한 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식 등을 탐색(traversing)해야 할 때가 있다. 아래 예제를 살펴보자.

```html
<ul id="fruits">
  <li class="apple">apple</li>
  <li class="banana">banana</li>
  <li class="orange">orange</li>
</ul>
```

ul#fruits 요소는 3개의 자식 요소를 가진다. 이때 먼저 ul#fruits 요소 노드를 취득한 다음, 자식 노드를 모두 탐색하거나 첫번째 자식 노드 또는 마지막 자식 노드 만을 탐색할 수 있다.

li.banana 요소는 2개의 형제 요소와 부모 요소를 가진다. 이때 먼저 li.banana 요소 노드를 취득한 다음, 형제 노드를 탐색하거나 부모 노드를 탐색할 수 있다.

이처럼 DOM 트리 상의 노드를 탐색할 수 있도록 Node, Element 인터페이스는 **트리 탐색 프로퍼티**를 제공한다.

<img src="https://user-images.githubusercontent.com/32444914/83405180-f008dc80-a446-11ea-96a6-3c8258e254b8.png" width="70%" />

DOM 트리를 구성하는 노드로서 갖추어야 할 트리 노드 탐색 프로퍼티인 parentNode, previousSibling, firstChild, childNodes 등은 Node.prototype이 제공하고 프로퍼티 키에 Element가 포함된 previousElementSibling, nextElementSibling, children은 Element.prototype이 제공하는 프로퍼티이다.

노드 탐색 프로퍼티는 모두 **접근자 프로퍼티**이다. 단, setter 없이 getter만 존재하여 참조만 가능한 읽기 전용 프로퍼티이다. 읽기 전용 접근자 프로퍼티에 값을 할당하면 아무런 에러 없이 무시된다.

<img src="https://user-images.githubusercontent.com/32444914/83409975-71b13800-a450-11ea-975d-e8754454f498.png" width="60%" />

&nbsp;  

### 3.1. 공백 텍스트 노드

**HTML 요소 사이의 개행이나 공백은 텍스트 노드를 생성한다.**

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
  </body>
</html>
```

텍스트 에디터에서 HTML 문서에 엔터 키를 입력하면 개행 문자가 추가된다. 위 HTML 문서에도 개행 문자가 포함되어 있다. 위 HTML 문서는 마싱되어 아래와 같은 DOM을 생성한다.

<img src="https://user-images.githubusercontent.com/32444914/83410213-eab08f80-a450-11ea-81c6-19a41d5b5faf.png" width="70%" />

이처럼 개행이나 공백은 텍스트 노드를 생성한다. 따라서 노드 탐색 시에는 개행이나 공백 문자가 생성한 텍스트 노드에 주의해야 한다.

&nbsp;  

### 3.2. 자식 노드 탐색

자식 노드를 탐색하기 위해서는 아래와 같은 노드 탐색 프로퍼티를 사용한다.

| 프로퍼티                            | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| Node.prototype.childNodes           | 자식 노드를 모두 탐색하여 DOM 컬렉션 객체인 NodeList에 담아 반환한다. **childNodes 프로퍼티가 반환한 NodeList에는 텍스트 노드 또는 요소 노드가 포함되어 있다.** |
| Element.prototype.children          | 자식 요소 노드 만을 모두 탐색하여 DOM 컬렉션 객체인 HTMLCollection에 담아 반환한다. **children 프로퍼티가 반환한 HTMLCollection에는 텍스트 노드는 포함되지 않고 요소 노드만이 포함되어 있다.** |
| Node.prototype.firstChild           | 첫번째 자식 노드를 반환한다. 반환된 노드는 텍스트 노드 또는 요소 노드이다. |
| Node.prototype.lastChild            | 마지막 자식 노드를 반환한다. 반한된 노드는 텍스트 노드 또는 요소 노드이다. |
| Element.prototype.firstElementChild | 첫번째 자식 노드를 반환한다. 요소 노드만을 반환한다.         |
| Element.prototype.lastElementChild  | 마지막 자식 노드를 반환한다. 요소 노드만을 반환한다.         |

&nbsp;  

### 3.3. 자식 노드 존재 확인

| 프로퍼티                            | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| Node.prototype.hasChildNodes        | 자식 노드의 존재 여부를 불리언으로 반환한다. childNodes 프로퍼티와 마찬가지로 텍스트 노드를 포함하여 자식 노드의 존재를 확인한다. |
| Element.prototype.children.length   | 요소 노드인 자식 노드가 존재하는지 children 프로퍼티(유사 배열 객체)의 길이를 확인한다. children은 DOM 콜렉션 객체인 HTMLCollection 객체이다. |
| Element.prototype.childElementCount | 요소 노드인 자식 노드의 수를 나타내는 프로퍼티               |

&nbsp;  

### 3.4. 텍스트 노드 탐색

요소 노드의 텍스트 노드는 요소 노드의 자식 노드이다. 따라서 요소 노드의 텍스트 노드는 firstChild 프로퍼티로 접근할 수 있다.

&nbsp;  

### 3.5. 부모 노드 탐색

부모 노드를 탐색하기 위해서는 `Node.prototype.parentNode` 프로퍼티를 사용한다. 텍스트 노드는 DOM 트리의 최종단 노드인 리프 노드(leaf node)이므로 탐색한 부모 노드가 텍스트 노드인 경우는 없다.

&nbsp;  

### 3.6. 형제 노드 탐색

같은 부모 노드를 갖는 형제 노드를 탐색하기 위해서는 아래와 같은 노드 탐색 프로퍼티를 사용한다. 단, **어트리뷰트 노드는 요소 노드의 형제 노드이지만, 같은 부모 노드를 갖는 형제 노드가 아니기 때문에 반환되지 않는다.** 즉, 아래 프로퍼티는 텍스트 노드 또는 요소 노드만 반환한다.

| 프로퍼티                                 | 설명                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| Node.prototype.previousSibling           | 같은 부모 노드를 갖는 형제 노드 중 이전 형제 노드를 탐색하여 반환한다. 텍스트 노드 또는 요소 노드가 반환된다. |
| Node.prototype.nextSibling               | 같은 부모 노드를 갖는 형제 노드 중 다음 형제 노드를 탐색하여 반환한다. 텍스트 노드 또는 요소 노드가 반환된다. |
| Element.prototype.previousElementSibling | 같은 부모 노드를 갖는 형제 요소 노드 중 이전 형제 요소 노드를 탐색하여 반환한다. |
| Element.prototype.nextElementSibling     | 같은 부모 노드를 갖는 형제 요소 노드 중 다음 형제 요소 노드를 탐색하여 반환한다. |

&nbsp;  

## 4. 노드 정보 취득

노드 객체에 대한 정보를 확인하려면 아래와 같은 노드 정보 프로퍼티를 사용한다.

| 프로퍼티                | 설명                                                         |
| ----------------------- | ------------------------------------------------------------ |
| Node.prototype.nodeType | 노드 객체의 종류를 나타내는 상수를 반환한다. 노드 타입 상수는 Node에 정의되어 있다. |
| Node.prototype.nodeName | 노드의 이름을 문자열로 반환한다.                             |

&nbsp;  

## 5. 요소 노드의 텍스트 조작

### 5.1. nodeValue

`Node.prototype.nodeValue` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티이다. 따라서 nodeValue 프로퍼티는 참조와 할당 모두 가능하다.

노드의 nodeValue 프로퍼티를 참조하면 **노드의 값을 반환**한다. 이때 텍스트 노드가 아닌 노드(문서 노드 혹은 요소 노드)의 nodeValue 프로퍼티를 참조하면 null을 반환한다. 텍스트 노드의 nodeValue 프로퍼티를 참조할 때만 텍스트 노드의 값, 즉 텍스트를 반환한다.

텍스트 노드의 nodeValue 프로퍼티에 값을 할당하면 텍스트를 변경할 수 있다. 이를 통해 요소 노드의 텍스트를 변경하려면 아래와 같은 처리가 필요하다.

1. 텍스트를 변경할 요소 노드를 취득한 다음, 취득한 요소 노드의 텍스트 노드를 탐색한다. 텍스트 노드는 요소 노드의 자식 노드이므로 firstChild 프로퍼티를 사용하여 탐색한다.
2. nodeValue 프로퍼티를 사용하여 탐색한 텍스트 노드의 값을 변경한다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello</div>
    <script>
    	// 1. div#foo 요소의 텍스트 노드 취득
      const $textNode = document.getElementById('foo').firstChild;
      
      // 2. 텍스트 노드의 텍스트 변경.
      $textNode.nodeValue = 'World';
      
      console.log($textNode.nodeValue); // World
    </script>
  </body>
</html>
```

&nbsp;  

### 5.2. textContent

`Node.prototype.textContent`는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 취득하거나 변경한다.

요소 노드의 textContent 프로퍼티를 참조하면 요소 노드의 컨텐츠 영역(시작 태그와 종료 태그 사이)내의 텍스트를 모두 반환한다. 이때 HTML 마크업은 무시된다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello <span>world!</span></div>
    <script>
    	// div#foo 요소의 텍스트를 모두 취득
      // HTML 마크업은 무시된다.
      console.log(document.getElementById('foo').textContent);
      // Hellow world!
    </script>
  </body>
</html>
```

<img src="https://user-images.githubusercontent.com/32444914/83415196-b2617f00-a459-11ea-8bad-13c3f65b3849.png" width="70%" />

만약 요소 노드의 컨텐츠 영역에 다른 요소 노드가 없고 텍스트만 존재한다면 firstChild.nodeValue와 textContent 프로퍼티는 같은 결과를 반환한다. 따라서 이 경우, textContent 프로퍼티를 사용하는 것이 좋다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello</div>
    <script>
    	const $foo = document.getElementById('foo');
      
      // 요소 노드의 컨텐츠 영역에 다른 요소 노드가 없고 텍스트만 존재한다면
      // firstChild.nodeValue와 textContent는 같은 결과를 반환한다.
      console.log($foo.textContent === $foo.firstChild.nodeValue); // true
    </script>
  </body>
</html>
```

**만약 요소 노드의 textContent 프로퍼티에 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열이 텍스트로 추가된다.** 이때 할당한 문자열에 HTML 마크업이 포함되어 있더라도 문자열 그대로 인식되어 텍스트로 취급된다. 즉, HTML 마크업이 파싱되지 않는다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello <span>world!</span></div>
    <script>
    	// div#foo 요소의 모든 자식 노드가 제거되고 할당한 문자열이 텍스트로 추가된다.
      document.getElementById('foo').textContent = 'Hi <span>there!</span>';
    </script>
  </body>
</html>
```

<img src="https://user-images.githubusercontent.com/32444914/83415795-a629f180-a45a-11ea-9c59-c4048856f351.png" width="70%" />

&nbsp;  

## 6. DOM 조작

DOM 조작(DOM manipulation)은 **새로운 노드를 생성하여 DOM에 추가하거나 기존 노드를 삭제 또는 교체하는 것**을 말한다. DOM 조작에 의해 DOM에 새로운 노드가 추가되거나 삭제되면 **리플로우와 리페인트가 발생하는 원인**이 되므로 성능에 영향을 준다. 따라서 복잡한 컨텐츠를 다루는 DOM 조작은 성능 최적화를 위해 주의해서 다루어야 한다.

&nbsp;  

### 6.1. innerHTML

`Element.prototype.innerHTML` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 **요소 노드의 HTML 마크업을 취득하거나 변경**한다. 요소 노드의 innerHTML 프로퍼티를 참조하면 요소 노드의 컨텐츠 영역(시작 태그와 종료 태그 사이) 내에 포함된 모든 HTML 마크업을 문자열로 반환한다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello <span>world!</span></div>
    <script>
    	// div#foo 요소의 컨텐츠 영역 내의 HTML 마크업을 취득
      console.log(document.getElementById('foo').innerHTML);
      // Hello <span>world!</span>
    </script>
  </body>
</html>
```

앞서 살펴본 textContent 프로퍼티를 참조하면 HTML 마크업을 무시하고 텍스트만 반환하지만, innerHTML 프로퍼티는 HTML 마크업을 그대로 반환한다.

<img src="https://user-images.githubusercontent.com/32444914/83422253-37ea2c80-a464-11ea-8a25-3cf283fb17aa.png" width="70%" />

요소 노드의 innerHTML 프로퍼티에 문자열을 할당하면 요소 노드의 자식 노드가 모두 제거되고 할당한 문자열에 포함되어 있는 HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영된다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello <span>world!</span></div>
    <script>
    	// HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영된다.
      document.getElemenetById('foo').innerHTML = 'Hi <span>there!</span>';
    </script>
  </body>
</html>
```

<img src="https://user-images.githubusercontent.com/32444914/83422638-ca8acb80-a464-11ea-8940-b21cd6d0b1d6.png" width="70%" />

이처럼 innerHTML 프로퍼티를 사용하면 HTML 마크업 문자열로 간단히 DOM 조작이 가능하다.

요소 노드의 innerHTML 프로퍼티에 할당한 HTML 마크업 문자열은 렌더링 엔진에 의해 파싱되어 요소 노드의 자식으로 DOM에 반영된다. 이때 사용자로부터 입력 받은 데이터(untrusted input data)를 그대로 innerHTML 프로퍼티에 할당하는 것은 <strong>크로스 사이트 스크립팅 공격(XSS: Cross-Site Scripting Attacks)</strong>에 취약하므로 위험하다. HTML 마크업 내에 자바스크립트 악성 코드가 포함되어 있다면 파싱 과정에서 그대로 실행될 가능성이 있기 때문이다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello</div>
    <script>
    	// innerHTML로 스크립트 태그를 삽입하여 자바스크립트가 실행되도록 한다.
      // HTML5는 innerHTML 프로퍼티로 삽입된 script 요소 내의 자바스크립트 코드를 실행하지 않는다.
      document.getElementById('foo').innerHTML = `<script>alert('XSS!')</script>`;
    </script>
  </body>
</html>
```

HTML5는 innerHTML 프로퍼티로 삽입된 script 요소 내의 자바스크립트 코드를 실행하지 않는다. 따라서 HTML5를 지원하는 브라우저에서 위 예제는 동작하지 않는다. 하지만 script 요소 없이도 크로스 사이트 스크립팅 공격은 가능하다. 아래의 간단한 크로스 사이트 스크립팅 공격은 모던 브라우저에서도 동작한다.

```html
<!doctype html>
<html>
  <body>
    <div id="foo">Hello</div>
    <script>
    	document.getElementById('foo').innerHTML = `<img src="x" onerror="alert('XSS')">`;
    </script>
  </body>
</html>
```

이처럼 innerHTML 프로퍼티를 사용한 DOM 조작은 구현이 간단하고 직관적이라는 장점이 있지만, XSS 공격에 취약한 단점도 있다.

> **HTML 새니티제이션(HTML sanitization)**
>
> HTML 새니티제이션 사용자로부터 입력 받은 데이터(untrusted input data)에 의해 발생할 수 있는 XSS 공격을 예방하기 위해 잠재적 위험을 제거하는 기능을 말한다. [DOMPurify](https://github.com/cure53/DOMPurify) 라이브러리는 이러한 기능을 제공하는 라이브러리다. DOMPurify는 아래와 같이 잠재적 위험을 내포한 HTML 마크업을 살균(sanitize)하여 잠재적 위험을 제거한다.
>
> `DOMPurify.sanitize('<img src=x onerror=alert(1) />'); // <img src="x" />`

&nbsp;  

innerHTML 프로퍼티의 또 다른 단점은 **기존의 노드를 제거하고 다시 파싱을 수행**하여 DOM을 변경한다는 것이다. 아래 예제를 살펴보자.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
    </ul>
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // 노드 추가
      $fruits.innerHTML += `<li class="banana">Banana</li>`;
    </script>
  </body>
</html>
```

위 예제는 ul#fruits 요소에 자식 요소 li.banana를 추가한다. 이때 ul#fruits 요소의 자식 요소 li.apple은 변경이 없으므로 다시 생성할 필요가 없다. 다만 새롭게 추가할 li.banana 노드만을 생성하여 DOM에 반영하면 된다. 위 코드를 얼핏 보면 그렇게 동작할 것 처럼 보이지만 **자식 노드를 모두 제거**하고 새롭게 자식 노드 li.apple과 li.banana를 생성하여 DOM에 반영한다. 이는 효율적이지 않다.

innerHTML 프로퍼티의 또 다른 단점은 새로운 요소를 삽입할 위치를 지정할 수 없다는 것이다. 아래 예제를 살펴보자.

```html
<ul id="fruits">
  <li class="apple">Apple</li>
  <li class="orange">Orange</li>
</ul>
```

li.apple 요소와 li.orange 요소 사이에 새로운 요소를 삽입하고 싶은 경우, innerHTML 프로퍼티를 사용하면 위치를 지정할 수 없다. 이처럼 innerHTML 프로퍼티는 복잡하지 않은 요소를 새롭게 추가할 때 유용하지만 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입해야 할 때는 사용하지 않는 것이 좋다.

&nbsp;  

### 6.2. insertAdjacentHTML 메소드

`Element.prototype.insertAdjacentHTML` 메소드는 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입한다.

```javascript
Element.prototype.insertAdjacentHTML(position, DOMString)
```

`insertAdjacentHTML` 메소드는 두번째 인수로 전달한 HTML 마크업 문자열(DOMString)을 파싱하고 그 결과로 생성된 노드를 첫번째 인수로 전달한 위치(position)에 삽입하여 DOM에 반영한다. 첫번째 인수로 전달할 수 있는 문자열은 'beforebegin', 'afterbegin', 'beforeend', 'afterend' 4가지이다.

<img src="https://user-images.githubusercontent.com/32444914/83483487-b931d580-a4dd-11ea-9914-0a70a880bd52.png" width="70%" />

```html
<!doctype html>
<html>
  <body>
    <!-- beforebegin -->
    <div id="foo">
      <!-- afterbegin -->
    	text
      <!-- beforeend -->
    </div>
    <!-- afterend -->
    
    <script>
    	 const $foo = document.getElementById('foo');
      
      $foo.insertAdjacentHTML('beforebegin', '<p>beforebegin</p>');
    </script>
  </body>
</html>
```

`insertAdjacentHTML` 메소드는 기존 요소에는 영향을 주지 않고 새롭게 삽입될 요소만을 파싱하여 DOM에 반영하므로 기존의 자식 노드를 모두 제거하고 다시 자식 노드를 생성하여 DOM에 반영하는 innerHTML 프로퍼티보다 효율적이고 빠르다.

단, innerHTML 프로퍼티와 마찬가지로 insertAdjacentHTML 메소드는 HTML 마크업 문자열을 파싱하므로 XSS 공격에 취약하다는 점은 동일하다.

&nbsp;  

### 6.3. 노드 생성과 추가

DOM은 노드를 직접 생성 / 삽입 / 삭제 / 치환하는 메소드도 제공한다. 아래 예제를 살펴보자.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li>Apple</li>
    </ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // 1. 요소 노드 생성
      const $li = document.createElement('li');
      
      // 2. 텍스트 노드 생성
      const textNode = document.createTextNode('Banana');
      
      // 3. 텍스트 노드를 요소 노드의 자식 노드로 추가
      // 요소 노드에 자식 노드가 하나도 없는 경우 텍스트 노드를 생성하여 요소 노드의
      // 자식 노드로 텍스트 노드를 추가하는 것보다 textcContent 프로퍼티를
      // 사용하는 편이 보다 간편하다. 단, 요소 노드의 textContent 프로퍼티에
      // 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열이
      // 텍스트로 추가되므로 주의가 필요하다.
      $li.appendChild(textNode);
      
      // 4. 요소 노드를 DOM에 추가
      $fruits.appendChild($li);
    </script>
  </body>
</html>
```

위 예제는 새로운 요소 노드를 생성하고 텍스트를 추가한 다음, DOM에 추가한다.

&nbsp;  

### 6.3. 노드 생성과 추가

### 6.4. 복수의 노드 생성과 추가

DocumentFragment 노드는 문서, 요소, 어트리뷰트, 텍스트 노드와 같은 노드 객체의 일종으로 부모 노드가 없으며 기존 DOM과는 별도 존재한다는 특징이 있다. DocumentFragment 노드는 컨테이너 요소와 같이 자식 노드들의 부모 노드로서 별도의 서브 DOM을 구성하여 기존 DOM에 추가하기 위한 용도로 사용한다.

DocumentFragment 노드는 기존 DOM과는 별도로 존재하므로 DocumentFragment 노드에 자식 노드를 추가하여도 기존 DOM에는 어떠한 변경도 발생하지 않는다. 또한 DocumentFragment 노드를 DOM에 추가하면 자신의 자식 노드만 DOM에 추가한다.

<img src="https://user-images.githubusercontent.com/32444914/83490628-57786800-a4eb-11ea-9c04-0cd11123d4c0.png" width="70%" />

`Document.prototype.createDocumentFragment` 메소드는 비어 있는 DocumentFragment 노드를 생성하여 반환한다. 아래 예제를 살펴보자.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits"></ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // DocumentFragment 노드 생성
      const $fragment = document.createDocumentFragment();
      
      ['Apple', 'Banana', 'Orange'].forEach(text => {
        // 1. 요소 노드 생성
        const $li = document.createElement('li');
        
        // 2. 텍스트 노드 생성
        const $textNode = document.createTextNode(text);
        
        // 3. 텍스트 노드를 요소 노드의 자식 노드로 추가
        $li.appendChild($textNode);
        
        // 4. 요소 노드를 DocumentFragment 노드의 자식 노드로 추가
        $fragment.appendChild($li);
      });
      
      // 5. DocumentFragment 노드를 DOM에 추가
      $fruits.appendChild($fragment);
    </script>
  </body>
</html>
```

먼저 DocumentFragment 노드를 생성하고 DOM에 추가할 요소 노드를 DocumentFragment 노드에 자식 노드로 추가한 다음, DocumentFragment 노드를 기존 DOM에 추가한다.

이때 실제로 DOM 변경이 발생하는 것은 DocumentFragment 노드를 DOM에 추가 한번 뿐이다. 따라서 여러 개의 요소 노드를 DOM에 추가하는 경우, DocumentFragment 노드를 사용하는 것이 보다 효율적이다.

&nbsp;  

### 6.5. 노드 삽입

#### 6.5.1. 마지막 노드로 추가

`Node.prototype.appendChild` 메소드는 인수로 전달받은 노드를 자신을 호출한 노드의 마지막 자식 노드로 DOM에 추가한다. 이때 노드를 추가할 위치를 지정할 수 없고 언제나 마지막 자식 노드로 추가한다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
    	<li>Apple</li>
      <li>Banana</li>
    </ul>
    
    <script>
    	// 요소 노드 생성
      const $li = document.createElement('li');
      
      // 텍스트 노드를 $li 노드의 마지막 자식 노드로 추가
      $li.appendchild(document.createTextNode('Orange'));
      
      // $li 노드를 ul#fruits 요소의 마지막 자식 노드로 추가
      document.getElementById('fruits').appendChilld($li);
    </script>
  </body>
</html>
```

&nbsp;  

#### 6.5.2. 지정한 위치에 노드 삽입

`Node.prototype.insertBefore(newNode, childNode)` 메소드는 첫번째 인수로 전달받은 노드를 두번째 인수로 전달받은 노드 앞에 삽입한다.

두번째 인수로 전달받은 노드는 반드시 `insertBefore` 메소드를 호출한 노드의 자식 노드이어야 한다. 그렇지 않으면 DOMException 에러가 발생한다.

두번째 인수로 전달받은 노드가 null이면 `insertBefore` 메소드를 호출한 노드의 마지막 자식 노드로 추가된다. 즉, `appendChild` 메소드 처럼 동작한다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li>Apple</li>
      <li>Banana</li>
    </ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // 요소 노드 생성
      const $li = document.createElement('li');
      
      // 텍스트 노드를 $li 노드의 마지막 자식 노드로 추가
      $li.appendChild(document.createTextNode('Orange'));
      
      // $li 노드를 $fruits의 마지막 자식 요소 앞에 삽입
      $fruits.insertBefore($li, $fruits.lastElementChild);
      // Apple - Orange - Banana
    </script>
  </body>
</html>
```

&nbsp;  

### 6.6. 노드 이동

DOM에 이미 존재하는 노드를 `appendChild` 또는 `insertBefore` 메소드를 사용하여 DOM에 추가하면 **현재 위치에서 노드를 제거하고 새로운 위치에 노드를 추가한다**. 즉, 노드가 이동한다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li>Apple</li>
      <li>Banana</li>
      <li>Orange</li>
    </ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // 이미 존재하는 노드를 취득
      const [$apple, $banana] = $fruits.children;
      
      // 이미 존재하는 $apple 요소를 $fruits 요소의 마지막 노드로 이동
      $fruits.appendChild($apple); // Banana - Orange - Apple
      
      // 이미 존재하는 $banana 요소를 $fruits 요소의 마지막 자식 노드 앞으로 이동
      $fruits.insertBefore($banana, $fruits.lastElementChild);
      // Orange - Banana - Apple
    </script>
  </body>
</html>
```

&nbsp;  

### 6.7. 노드 복사

`Node.prototype.cloneNode([deep: true | false])` 메소드는 **노드 자신의 사본을 생성**하여 반환한다. 매개 변수 deep에 true를 전달하면 노드 자신을 깊은 복사(deep copy)하여 모든 자손 노드가 포함된 사본을 생성하고, false를 전달하거나 생략하면 노드 자신을 얕은 복사(shallow copy)하여 노드 자신만의 사본을 생성한다. 얖은 복사로 생성된 요소 노드는 자손 노드를 복사하지 않으므로 텍스트 노드도 없다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li>Apple</li>
    </ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      const $apple = $fruits.firstElementChild;
      
      // $apple 요소를 얕은 복사하여 사본 생성. 텍스트 노드가 없는 사본이 생성된다.
      const $shallowClone = $apple.cloneNode(); // <li></li>
      
      // $apple 요소를 깊은 복사하여 사본 모든 자손 노드가 포함된 사본 생성
      const $deepClone = $apple.cloneNode(true); // <li>Apple</li>
    </script>
  </body>
</html>
```

&nbsp;  

### 6.8. 노드 교체

`Node.prototype.replaceChild(newChild, oldChild)` 메소드는 자신을 호출한 노드의 자식 노드(oldChild)를 다른 노드(newChild)로 교체한다. 즉, replaceChild 메소드는 부모 노드의 자식인 oldChild 노드를 newChild 노드로 교체한다. 이때 oldChild 노드는 DOM에서 제거된다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li>Apple</li>
    </ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // 기존 노드를 치환할 요소 노드
      const $newChild = document.createElement('li');
      $newChild.textContent = 'Banana';
      
      // $fruits 요소의 첫번째 요소를 $newChild로 교체
      $fruits.replaceChild($newChild, $fruits.firstElementChild);
    </script>
  </body>
</html>
```

&nbsp;  

### 6.9. 노드 삭제

`Node.prototype.removeChild(child)` 메소드는 매개 변수 child에 전달한 노드를 DOM에서 삭제한다. 매개 변수 child에게 전달한 노드는 `removeChild` 메소드를 호출한 노드의 자식 노드이어야 한다.

```html
<!doctype html>
<html>
  <body>
    <ul id="fruits">
      <li>Apple</li>
      <li>Banana</li>
    </ul>
    
    <script>
    	const $fruits = document.getElementById('fruits');
      
      // $fruits 요소의 마지막 요소를 DOM에서 삭제
      $fruits.removeChild($fruits.lastElementChild);
    </script>
  </body>
</html>
```

&nbsp;  

## 7. 어트리뷰트

### 7.1. 어트리뷰트 노드와 attributes 프로퍼티

HTML 문서의 구성 요소인 HTML 요소는 여러 개의 어트리뷰트(attributes, 속성)를 가질 수 있다.

```html
<input id="user" type="text" value="smilejin92" />
```

[글로벌 어트리뷰트](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)와 [이벤트 핸들러 어트리뷰트](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)는 모든 HTML 요소에서 공통적으로 사용할 수 있지만, 특정 HTML 요소에만 한정적으로 사용 가능한 어트리뷰트도 있다. 예를 들어, `type`, `value`, `checked` 어트리뷰트는 input 요소에만 사용할 수 있다.

HTML 문서가 파싱될 때, **HTML 요소의 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드 객체의 형제 노드로 추가된다.** 이때 HTML 어트리뷰트 당 하나의 어트이뷰트 노드가 생성된다. 즉, 위 input 요소는 3개의 어트리뷰트가 있으므로 3개의 어트리뷰트 노드가 생성된다.

이때 모든 어트리뷰트 노드의 참조는 유사 배열 객체이자 이터러블인 NamedNodeMap 객체에 담겨서 요소 노드의 attributes 프로퍼티에 저장된다.

<img src="https://user-images.githubusercontent.com/32444914/83506263-e55f4d80-a501-11ea-9a39-e8646cef2f18.png" width="80%" />

따라서 요소 노드의 모든 어트리뷰트 노드는 요소 노드의 `Element.prototype.attribtues` 프로퍼티로 취득할 수 있다. **attributes 프로퍼티는 getter만 존재하는 읽기 전용 접근자 프로퍼티이며 요소 노드의 모든 어트리뷰트 노드의 참조가 담긴 NamedNodeMap 객체를 반환**한다.

```html
<!doctype html>
<html>
  <body>
    <input id="user" type="text" value="smilejin92">
    <script>
    	const { attributes } = document.getElementById('user');
      console.log(attributes); // NamedNodeMap
      
      // 어트리뷰트 값 취득
      console.log(attributes.id.value); // user
      console.log(attributes.type.value); // text
      console.log(attributes.value.value); // smilejin92
    </script>
  </body>
</html>
```

&nbsp;  

### 7.2. HTML 어트리뷰트 조작

요소 노드의 attributes 프로퍼티는 getter만 존재하는 읽기 전용 접근자 프로퍼티이므로 HTML 어트리뷰트 값을 취득할 순 있지만 변경 할 순 없다. 또한 attributes 프로퍼티를 통해야만 HTML 어트리뷰트 값을 취득할 수 있기 때문에 불편하다.

`Element.prototype.getAttribute / setAttribute` 메소드를 사용하면 attributes 프로퍼티를 통하지 않고 요소 노드에서 메소드를 통해 직접 HTML 어트리뷰트 값을 취득하거나 변경할 수 있다.

```html
<!doctype html>
<html>
  <body>
    <input id="user" type="text" value="smilejin92">
    
    <script>
    	const $input = document.getElementById('user');
      
      // value 어트리뷰트 값 취득
      const inputValue = $input.getAttribute('value'); // smilejin92
      
      // value 어트리뷰트 값 변경
      $input.setAttribtue('value', 'foo'); // smilejin92 -> foo
    </script>
  </body>
</html>
```

&nbsp;  

HTML 어트리뷰트의 존재 여부를 확인하려면 `Element.prototype.hasAttribute(attributeName)` 메소드를 사용하고, HTML 어트리뷰트를 삭제하려면 `Element.prototype.removeAttribute(attributeName)` 메소드를 사용한다.

```html
<!doctype html>
<html>
  <body>
    <input id="user" type="text" value="smileji92">
    <script>
    	const $input = document.getElementById('user');
      
      // id 어트리뷰트 존재 확인
      if ($input.hasAttribute('id')) {
        // id 어트리뷰트 삭제
        $input.removeAttribute('id');
      }
    </script>
  </body>
</html>
```

&nbsp;  

### 7.3. HTML 어트리뷰트 vs. DOM 프로퍼티

요소 노드 객체에는 HTML 어트리뷰트에 대응하는 DOM 프로퍼티가 존재한다. 이 DOM 프로퍼티들은 HTML 어트리뷰트 값을 **초기값**으로 가지고 있다.

예를 들어 `<input id="user" type="text" value="smilejin92">` 요소가 파싱되어 생성된 요소 노드 객체는 id, type, value 어트리뷰트에 대응하는 id, type, value 프로퍼티가 존재한다. 이 DOM 프로퍼티들은 HTML 어트리뷰트의 값을 초기값으로 가지고 있다.

<img src="https://user-images.githubusercontent.com/32444914/83509933-286fef80-a507-11ea-91a2-71bf3ecac7fa.png" width="80%" />

DOM 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티이다. 따라서 DOM 프로퍼티는 참조와 변경이 가능하다.

```html
<!doctype html>
<html>
  <body>
    <input id="user" type="text" value="smilejin92">
    
    <script>
      const $input = document.getElementById('user');
      
    	// 요소 노드의 value 프로퍼티 값 변경
      $input.value = 'foo';
      
      // 요소 노드의 value 프로퍼티 값 참조
      console.log($input.value); // foo
    </script>
  </body>
</html>
```

이처럼 HTML 어트리뷰트는 아래와 같이 중복 관리되고 있는 것처럼 보인다.

1. 요소 노드의 attributes 프로퍼티에서 관리하는 어트리뷰트 노드
2. HTML 어트리뷰트에 대응하는 요소 노드의 프로퍼티(DOM 프로퍼티)

**HTML 어트리뷰트의 역할은 HTML 요소의 초기 상태를 지정하는 것이다. 즉, HTML 어트리뷰트 값은 HTML 요소의 초기 상태를 의미하며 이는 변하지 않는다.**

예를 들어 `<input id="user" type="text" value="smilejin92">` 요소의 value 어트리뷰트는 input 요소의 입력 필드에 표시할 초기값을 지정한다. 즉, input 요소가 렌더링되면 입력 필드에 초기값으로 지정한 value 어트리뷰트 값 "smilejin92"가 표시된다.

이때 input 요소의 value 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드의 attributes 프로퍼티에 저장된다. **이와는 별도로 value 어트리뷰트의 값은 요소 노드의 value 프로퍼티에 초기값으로 할당된다.**

input 요소의 요소 노드가 생성되어 첫 렌더링이 끝난 시점까지 어트리뷰트 노드의 어트리뷰트 값과 요소 노드의 value 프로퍼티에 초기값으로 할당된 값은 HTML 어트리뷰트 값과 동일하다.

```html
<!doctype html>
<html>
  <body>
    <input id="user" type="text" value="smilejin92">
    
    <script>
    	const $input = document.getElementById('user');
      
      // attributes 프로퍼티에 저장된 value 어트리뷰트 값
      console.log($input.getAttribute('value')); // smilejin92
      
      // 요소 노드의 프로퍼티에 저장된 value 프로퍼티
      console.log($input.value); // smilejin92
    </script>
  </body>
</html>
```

하지만 초기 렌더링 이후 사용자가 input 요소에 무언가를 입력하기 시작하면 상황이 달라진다.

**요소 노드는 상태(state)를 가지고 있다**. 예를 들어 input 요소는 사용자가 입력 필드에 입력한 값을 상태로 가지고 있으며, checkbox 요소는 사용자가 입력 필드에 입력한 체크 여부를 상태로 가지고 있다. input 요소나 checkbox 요소가 가지고 있는 상태는 사용자의 입력에 의해 변화하는 살아있는 것이다.

사용자가 input 요소의 입력 필드에 "foo"라는 값을 입력한 경우를 생각해보자. 이때 input 요소 노드는 사용자의 입력에 의해 변경된 최신 상태("foo")를 관리해야 하는 것은 물론, HTML 어트리뷰트로 지정한 초기 상태("smilejin92")도 관리해야 한다. 초기 상태 값을 관리하지 않으면 웹페이지를 처음 표시하거나 새로고침할 때 표시할 수 없다.

&nbsp;  

#### 7.3.1. 어트리뷰트 노드는 초기 상태를 관리한다

**HTML 어트리뷰트로 지정한 HTML 요소의 초기 상태는 어트리뷰트 노드에서 관리한다.**

&nbsp;  

#### 7.3.2. DOM 프로퍼티는 최신 상태를 관리한다.

**사용자가 입력한 최신 상태는 HTML 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티가 관리한다. DOM 프로퍼티는 사용자의 입력에 의한 상태 변화에 반응하여 언제나 최신 상태를 유지한다.**

&nbsp;  

#### 7.3.3. HTML 어트리뷰트와 DOM 프로퍼티의 대응 관계

대부분의 HTML 어트리뷰트 값은 HTML 어트리뷰트 이름과 동일한 DOM 프로퍼티 키로 참조할 수 있다. 단, 아래와 같이 HTML 어트리뷰트와 DOM 프로퍼티가 언제나 1:1로 대응하는 것은 아니며 HTML 어트리뷰트 이름과 DOM 프로퍼티 키가 반드시 일치하는 것도 아니다.

* id 어트리뷰트와 id 프로퍼티는 1:1 대응하며 동일한 값으로 연동한다.
* input 요소의 value 어트리뷰트는 value 프로퍼티와 1:1 대응한다. 하지만 value 어트리뷰트는 초기 상태를, value 프로퍼티는 최신 상태를 가진다.
* class 어트리뷰트는 className, classList 프로퍼티와 대응한다.
* for 어트리뷰트는 htmlFor 프로퍼티와 대응한다.
* td 요소의 colspan 어트리뷰트는 대응하는 프로퍼티가 존재하지 않는다.
* textContent 프로퍼티는 대응하는 어트리뷰트가 존재하지 않는다.
* 어트리뷰트 이름은 대소문자를 구별하지 않지만, 프로퍼티 키는 카멜 케이스를 따른다(ex. maxlength -> maxLength)

&nbsp;  

#### 7.3.4. DOM 프로퍼티 값의 타입

getAttribute 메소드로 취득한 어트리뷰트 값은 언제나 문자열이다. 하지만 **DOM 프로퍼티로 취득한 상태 값은 문자열이 아닐 수도 있다.** 예를 들어 checkbox 요소의 checked 어트리뷰트 값은 문자열이지만 checked 프로퍼티 값은 불리언 타입이다.

&nbsp;  

## 8. 스타일

### 8.1. 인라인 스타일 조작

`HTMLElement.prototype.style` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 **인라인 스타일(inline style)을 취득하거나 변경**한다.

```html
<!doctype html>
<html>
  <body>
    <div style="color: red">Hello World</div>
    <script>
    	const $div = document.querySelector('div');
      
      // 인라인 스타일 취득
      console.log($div.style); // CSSStyleDeclaration { 0: "color", ... }
      
      // 인라인 스타일 변경
      $div.style.color = 'blue';
      $div.style.width = '100px';
    </script>
  </body>
</html>
```

style 프로퍼티는 CSSStyleDeclaration 타입의 객체를 반환한다. CSSStyleDeclaration 객체는 CSS 프로퍼티에 대응하는 다양한 프로퍼티를 가지고 있으며, 이 프로퍼티에 값을 할당하면 해당 **CSS 프로퍼티가 인라인 스타일로 HTML 요소에 추가된다.**

CSS 프로퍼티는 케밥 케이스를 따른다. 이에 대응하는 CSSStyleDeclaration 객체의 프로퍼티는 카멜 케이스를 따른다. 예를 들어 CSS 프로퍼티 `background-color`에 대응하는 CSSStyleDeclaration 객체의 프로퍼티 `backgroundColor`이다.

```javascript
$div.style.backgroundColor = 'blue';
```

케밥 케이스의 CSS 프로퍼티를 그대로 사용하려면 객체의 마침표 표기법 대신 대괄호 표기법을 사용한다.

```javascript
$div.style['background-color'] = 'blue';
```

단위 지정이 필요한 CSS 프로퍼티의 값은 반드시 단위를 지정하여야 한다. 예를 들어 `px`, `em`, `%` 등의 크기 단위가 필요한 width 프로퍼티에 값을 할당할 때 단위를 생략하면 해당 CSS 프로퍼티는 적용되지 않는다.

```javascript
$div.style.width = '100px';
```

&nbsp;  

### 8.2. 클래스 조작

스타일 시트(CSS 파일) 또는 style 요소에 class로 스타일을 미리 정의한 다음, **HTML 요소의 class 어트리뷰트 값을 변경**하여 HTML 요소의 스타일을 변경할 수도 있다.

(질문. DOM 프로퍼티는 최신 상태를, HTML 어트리뷰트 노드는 초기값을 가지고 있다고 했는데 왜 className 혹은 classList 같은 DOM 프로퍼티를 변경하면 어트리뷰트 노드의 값도 변하는지?)

이때 HTML 요소의 class 어트리뷰트를 조작하려면, class 어트리뷰트에 대응하는 요소 노드의 프로퍼티를 사용한다. class 어트리뷰트에 대응하는 요소 노드의 프로퍼티는 class(자바스크립트에서 class는 예약어)가 아니라 className과 classList이다.

&nbsp;  

#### 8.2.1. className

`Element.prototype.className` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 **요소 노드의 class 어트리뷰트 값을 취득하거나 변경**한다.

요소 노드의 className 프로퍼티를 참조하면 class 어트리뷰트 값을 문자열로 반환하고, 요소 노드의 className 프로퍼티에 문자열을 할당하면 class 어트리뷰트 값을 할당한 문자열로 변경한다.

```html
<!doctype html>
<html>
  <head>
    <style>
      .box {
        width: 100px;
        height: 100px;
        background-color: skyblue;
      }
      
      .red { color: red; }
      .blue { color: blue; }
    </style>
  </head>
  <body>
    <div class="box red">Hello World</div>
    <script>
    	const $box = document.querySelector('.box');
      
      // class 어트리뷰트 값 취득
      console.log($box.className); // 'box red'
      // console.log($box.getAttribute('class')); // 'box red'
      
      // class 어트리뷰트 값 변경 (red를 blue로 변경)
      $box.className = $box.className.replace('red', 'blue');
      // $box.setAttribute('class', 'box blue');
    </script>
  </body>
</html>
```

className 프로퍼티는 문자열을 반환하므로 공백으로 구분된 여러 개의 클래스를 반환하는 경우, 다루기가 불편하다.

&nbsp;  

#### 8.2.2. classList

`Element.prototype.classList` 프로퍼티는 **class 어트리뷰트 값을 담은 DOMTokenList 객체를 반환**한다.

```html
<!doctype html>
<html>
  <head>
    <style>
      .box {
        width: 100px;
        height: 100px;
        background-color: skyblue;
      }
      
      .red { color: red; }
      .blue { color: blue; }
    </style>
  </head>
  <body>
    <div class="box red">Hello World</div>
    <script>
    	const $box = document.querySelector('.box');
      
      // class 어트리뷰트 값 취득
      console.log($box.classList);
      // DOMTokenList(2) [length: 2, value: "box blue", 0: "box", 1: "blue"]
      
      // class 어트리뷰트 값 변경 (red를 blue로 변경)
      $box.className = $box.className.replace('red', 'blue');
    </script>
  </body>
</html>
```

DOMTokenList 객체는 공백 문자로 구분된 토큰들로 구성된 컬렉션 객체로서 유사 배열 객체이자 이터러블이다. DOMTokenList 객체는 아래와 같이 유용한 메소드를 제공한다.

**`add(...className)`**

인수로 전달한 1개 이상의 문자열을 class 어트리뷰트에 추가한다.

```javascript
$box.classList.add('class-x', 'class-y'); // class="box red class-x class-y"
```



**`remove(...className)`**

인수로 전달한 1개 이상의 문자열을 class 어트리뷰트에서 삭제한다.

```javascript
$box.classList.remove('class-x', 'class-y'); // class="box red"
```



**`item(index)`**

인수로 전달한 index에 해당하는 문자열을 class 어트리뷰트에서 반환한다.

```javascript
$box.classList.item(1); // red
```



**`contains(className)`**

인수로 전달한 문자열에 해당하는 클래스가 class 어트리뷰트에 포함되어 있는지 확인한다.

```javascript
$box.classList.contains('red'); // true
```



**`replace(oldClassName, newClassName)`**

class 어트리뷰트에서 첫번째 인수로 전달한 문자열을 두번째 인수로 전달한 문자열로 변경한다.

```javascript
$box.classList.replace('red', 'blue'); // class="box blue"
```



**`toggle(className)`**

class 어트리뷰트에 인수로 전달한 문자열이 존재하면 삭제하고, 존재하지 않으면 추가한다.

```javascript
$box.classList.toggle('class-x'); // class="box blue class-x"
$box.classList.toggle('class-y'); // class="box blue"
```

2번째 인수로 **조건식**을 전달할 수 있다. 이때 조건식의 평가 결과가 true이면 class 어트리뷰트에 강제로 1번째 인수로 전달받은 문자열을 추가하고, false이면 강제로 제거한다.

```javascript
// 강제로 'red' 추가
$box.classList.toggle('red', true);

// 강제로 'red' 제거
$box.classList.toggle('red', false);
```

&nbsp;  

### 8.3. 요소에 적용되어 있는 CSS 스타일 참조

요소의 인라인 스타일을 포함한 모든 CSS 스타일을 참조해야 할 경우, `window.getComputedStyle(elem)` 메소드를 사용한다.

&nbsp;  

## 9. DOM 표준

HTML과 DOM 표준은 W3C와 WHATWG 두 단체가 나름대로 협력하며 공통된 표준을 만들어 왔다.

하지만 최근 두 단체가 서로 다른 결과물을 내놓기 시작했다. 별개의 HTML과 DOM 표준을 만드는 것은 이롭지 않으므로 2018년 4월부터 구글, 애플, 마이크로소프트, 모질라 네 주류 브라우저 벤더가 주도하는 WHATWG이 단일 표준을 내놓기로 두 단체가 합의했다.

DOM은 DOM Level 1 ~ DOM Level 4까지 4개의 레벨(버전)이 있다.

&nbsp;  

## 참고 자료

* [poiemaweb.com - DOM](https://poiemaweb.com/fastcampus/dom)

