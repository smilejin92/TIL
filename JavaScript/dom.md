# DOM

브라우저의 렌더링 엔진은 HTML 문서를 파싱하여 DOM을 생성한다.

**DOM(Document Object Model)은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메소드를 제공하는 트리 자료 구조이다.**

&nbsp;  

## 1. 노드

### 1.1. HTML 요소와 노드 객체

<strong>HTML 요소(HTML element)</strong>는 HTML 문서를 구성하는 **개별적인 요소**를 의미한다. HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환된다. 이때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로, HTML 요소의 텍스트 컨텐츠는 텍스트 노드로 변환된다.

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

이처럼 DOM은 노드 객체의 계층적인 구조로 구성된다. 노드 객체는 종류가 있고 상속 구조를 갖는다. 노드 객체는 총 12개의 종류(노트 타입)가 있다. 이 중 중요한 노드 타입은 아래와 같이 4가지이다.

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





















