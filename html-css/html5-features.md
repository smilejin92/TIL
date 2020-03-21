# 새로운 표준 HTML5

## HTML4.01, XHTML1.0과 HTML5의 차이점

### 1. 새롭게 등장한 컨텐츠 모델 (Content Models)

명확한 정보 구조 설계 및 구성을 위해 카테고리를 정의하여 각 요소별로 비슷한 성격을 가지고 있는 것 끼리 그룹화하였는데, 이를 HTML5 컨텐츠 모델이라고 한다. **하나의 요소가 여러 그룹에 속해 있을 수도 있고, 그렇지 않을 수도 있다.**

#### 컨텐츠 모델의 카테고리

* Sectioning Root
* Metadata Content
* Flow Content
* Sectionoing Content
* Heading Content
* Phrasing Content
* Embedded Content
* Interactive Content
* Palpable Content
* Script-supporting Elements
* Transparent Content

![content-venn](https://user-images.githubusercontent.com/32444914/77064698-5626bb80-6a23-11ea-8113-f751e09ddb20.png)

(이미지 출처: https://www.w3.org/TR/2011/WD-html5-20110525/content-models.html)

##### Sectioning Root

섹셔닝 루트에 속하는 요소는 `<section>`이나 `<article>` 요소와 같이 장이나 절과 같은 계층 구조로 구분되지 않고 독립적인 컨텐츠로 분리되기 때문에 아웃라인에 영향을 주지 않는다.

`<blockquote>`, `<body>`, `<detail>`, `<fieldset>`, `<figure>`, `<td>`

---

##### Metadata Content

메타데이터는 문서의 정보를 포함하는 메타데이터, 스타일 표현을 위한 `<style>` 요소, 행동을 설정하는 `<script>` 요소들을 나타낸다. 웹 브라우저에 직접적으로 표시되지 않으며 문서(document)와 문서 간의 관계를 설정한다.

`<base>`, `<link>`, `<meta>`, `<noscript>`, `<script>`, `<style>`, `<title>`

---

##### Flow Content

문서 본문에 해당하는 body 요소에 들어가는 대부분의 요소들이 플로우 컨텐츠 모델에 속한다. 이 중에서 `<area>`, `<link>`, `<meta>`, `<style>` 요소는 조건부로 플로우 컨텐츠가 된다.

`<a>`, `<article>`, `<aside>`, `<button>`, `<data>`, `<datalist>`, `<dialog>`, `<embed>`, `<fieldset>`, `<figure>`, `<footer>`, `<form>`, `<h1>` 등

([flow content 목록](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories))

---

##### Sectioning Content

섹셔닝 컨텐츠는 **대부분 HTML5에서 새롭게 추가된 요소들**이며, 제목과 그 내용을 포함한 범위를 지정하는 컨텐츠를 나타낸다. **모든 섹셔닝 컨텐츠는** 헤딩과 아웃라인을 가진다.

`<article>`, `<aside>`, `<nav>`, `<section>`

---

##### Heading Content

헤딩 컨텐치는 섹션의 제목을 나타낸다. 문서의 아웃라인을 고려하여 사용해야한다.

`<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`

---

##### Phrasing Content

프레이징 컨텐츠는 **문서의 텍스트**를 나타내며, 그 텍스트를 문단 내부 레벨로 마크업하는 요소들이다. 즉, **프레이징 컨텐츠가 모여 문단을 구성한다**. `<a>` 요소와 같은 일부 요소들은 텍스트가 아닌 다른 컨텐츠를 포함하지 않는다는 전제하에 조건부로 프레이징 컨텐츠가 되기도 한다.

프레이징 컨텐츠는 텍스트 이외에 임베디드 컨텐츠를 포함할 수 있다.

`<a>`, `<audio>`, `<button>`, `<code>`, `<embed>`, `<i>`, `<iframe>` 등

([phrasing content 목록](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories))

---

##### Embedded Content

문서 안에 외부 자원(외부 리소스) 또는 HTML이 아닌 다른 언어로 표현되는 컨텐츠를 말한다. 외부 자원에는 이미지, 동영상, 플러그인, iframe 컨텐츠 등이 있고, 다른 언어로 된 컨텐츠에는 수학 공식을 표현하는 MathML과 SVG 등이 있다.

`<audio>`, `<canvas>`, `<embed>`, `<iframe>`, `<img>`, `<math>`, `<object>`, `<svg>`, `<video>`

---

##### Interactive Content

인터랙티브 컨텐츠는 사용자가 어떤 기능을 조작할 수 있는 (상호 작용할 수 있는) 컨텐츠를 말한다. `<audio>`, `<img>`, `<input>`, `<object>`, `<video>` 요소는 이러한 특성을 바탕으로 조건부 인터랙티브 컨텐츠가 되기도 한다.

`<a>`, `<audio>` (controls 속성이 있는경우), `<button>`, `<details>`, `<iframe>`, `<img>` 등

([interactive content 목록](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories))

---

##### Palpable Content

팰퍼블 컨텐츠는 기존 컨텐츠 모델에 새롭게 추가된 개념으로 구체적으로 보여지고 이해할 수 있는 컨텐츠 요소를 말한다. 팰퍼블 컨텐츠는 최소한 하나 이상의 요소가 존재해야 하고 이때 해당 요소는 숨김 상태여서는 안된다.

`<a>`, `<abbr>`, `<address>`, `<article>`, `<aside>`, `<button>`, `<ul>` (하나 이상의 `<li>` 요소를 포함하고 있을 경우), `<video>` 등

([palpable content 목록](https://gerardnico.com/web/html/palpable))

---

##### Script-supporting Elements

스크립트 지원 요소는 요소 자체가 어떤 정보를 표현하지는 않지만 사용자에 대한 기능 등에 해당하는 스크립트를 지원하는 데 사용된다.

`<script>`

---

### 2. 아웃라인 알고리즘 (Outline Algorithm)

HTML5에서는 정보 구조를 명확히 할 수 있도록 **아웃라인 알고리즘**이라는 개념이 도입되었다. 아웃라인 알고리즘은 웹 페이지의 정보 구조를 판별할 수 있는 개념으로, **책의 목차**와 비슷하다.

HTML5에서 추가된 많은 요소들은 대부분 아웃라인 알고리즘과 관련이 있으며, 그 중에서도 **직접적으로 아웃라인을 구성하는 요소에는 헤딩 컨텐츠, 섹셔닝 컨텐츠 그리고 섹셔닝 루트 요소** 등이 있다.

### 3. HTML5의 API

HTML5의 커다란 변화 중 하나로는 다양한 API의 추가를 들 수 있다. HTML5에서는 자바스크립트 기술을 좀 더 편하리하게 이용할 수 있도록 다양한 API를 지원하고 있으며 HTML5에 추가된 대표적인 API는 아래와 같다.

* **오프라인 웹 구현을 위한 API**
  * Web Storage - 브라우저에 데이터를 저장하기 위한 공간으로, 쿠키와 비교했을 때 크기 제한과 유효 기간이 없고, 데이터가 서버로 전송되지 않으며, JavaScript 객체를 저장할 수 있다는 장점이 있다.
  * Web SQL Database / Indexed Database - 클라이언트에서 관리되는 데이터베이스를 제어할 수 있는 API로 구성되어 있다.
  * Application Cache - 웹 애플리케이션을 오프라인에서 사용하는 데 필요한 리소스(html, css, js, image 등)를 클라이언트 쪽에 캐싱하기 위한 기능
* **실시간 커뮤니케이션 API**
  * Web Workers - 메인 스레드(UI)와 독립적인 백그라운드 프로세스로 처리되는 스크립트를 말한다. 이를 활용하면 웹 브라우저 내에서 자바스크립트로 멀티스레드 프로그램을 구현할 수 있다.
  * Web Socket - 클라이언트 <-> 서버 간 양방향 전이중 통신을 구현한 Web Socket 프로토콜을 이용할 수 있는 API이다.
  * Notifications - 운영 체제로부터 독립적인 플랫폼 수준의 알림 메시지를 보여주는 API
* **파일/하드웨어 접근 API**
  * File API (Desktop Drag-in / out)
  * Geolocation
  * Device Orientation - 단말기의 센서를 이용하여 현재 방향과 기울기와 같은 정보를 구할 수 있는 API
  * Speech Input - 단말기의 마이크를 이용하여 음성을 입력 받은 후 문자로 바꿔주는 새로운 입력 방식
* **GUI를 위한 API**
  * Drag & drop

([HTML5 Web API 목록](https://developer.mozilla.org/en-US/docs/Web/API))

## 참고 자료

* [HTML5 Markup](https://github.com/seulbinim/PDF/blob/master/HTML5.pdf)
* [Nicôme - The Data Blog](https://gerardnico.com/web/html/palpable)
* [Content categories](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)
* [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)

