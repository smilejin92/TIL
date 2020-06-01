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



























