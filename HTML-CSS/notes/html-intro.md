# HTML5 개요

### 웹의 역사

- **HTML (HyperText Markup Language)** : the standard markup language for documents designed to be displayed in a web browser
- **인터넷** : 전세계를 연결하고 있는 국제 정보통신망
- **www (World Wide Web)** : 인터넷에 연결된 컴퓨터를 통해 사람들이 정보를 공유할 수 있는 정보공간

---

### 인터넷의 시작

* 미국 국방성에서 시작
* **ARPA (Advanced Research Projects Agency)** 창설
* 1969년 현재 웹의 모태가 되는 ARPNET 개발
* 현재 우리가 웹 브라우저로 보고있는 웹을 **팀 버너스리**가 개발 (hyperlink)

---

### 제 1차 웹 브라우저 전쟁

* 1993년 미국 일리노이 공과대학의 연구기관 NCSA에서 최초의 GUI 웹 브라우저인 **모자이크**를 발표
* 모자이크 핵심 개발자 **마크 안데르센**은 이후 **넷스케이프 커뮤니케이션** 설립, 넷스케이프 브라우저 발표

![](https://d2bs8hqp6qvsw6.cloudfront.net/article/images/750x750/dimg/netscape-3.jpg)

* 하지만 Microsoft의 **인터넷 익스플로러**의 점유율을 따라잡지 못한 채 붕괴

---

### 플러그인

* 웹 표준을 지정하는 **W3C**는 빠른 속도로 발전하는 웹에 대응하지 못함
* 이에 불만을 느끼던 기업들은 **플러그인**을 개발
* **플러그인** : 웹 브라우저와 연동되는 특정 프로그램을 사용자 PC에 추가로 설치해 웹 브라우저 기능을 확장하는 방법 (ex. **ActiveX**, **Adobe Flash**)

---

### 웹 2.0 시대

* 사용자가 함께 새로운 컨텐츠를 창조하는 시대 (ex. Youtube, Wikipedia)
* 2000년대 초반 ActiveX를 기반으로 기업의 **Web Application** 제작

![](https://amp.businessinsider.com/images/57f4127457540c22128b494a-750-377.png)

* Flash를 기반으로 애니메이션 제작 (ex. 졸라맨)

---

### WHATWG

* 인터넷 익스플로러 (IE)는 W3C의 표준 웹 브라우저가 됨
* 하지만 모든 웹 사이트에 플러그인 (ex. ActiveX)이 들어가면서 웹 사이트들이 무거워짐
* 이에 IE를 제외한 웹 브라우저 제공 기업 (ex. Apple, Mozilla, Opera)은 새로운 웹 표준 기관 **WHATWG**를 설립, 새로운 웹 표준으로 **Web Application 1.0** 작성
* 이후 W3C는 Web Application 1.0을 HTML5 표준으로 변경, WHATWG와 **HTML W/G** 결성

---

### 제 2차 웹 브라우저 전쟁

* 2010년 전후로 Microsoft와 W3C가 함께한 웹 표준 XHTML 2.0이 붕괴
* 다른 웹 브라우저는 모두 최신 표준을 지원하는데, IE는 지원하지 못하는 **역현상** 발생
* Mozilla, Chrome, Opera 등 모든 웹 브라우저가 빠른 속도로 업데이트 (2019 기준 Chrome 승)
* 2016년 1월, Microsoft는 IE 10 이하의 버전 지원을 중단

---

### HTML5를 공부해야하는 이유

* 스마트폰 시대가 되며 다양한 OS 등장 -> 각 디바이스 OS에 맞는 프로그램을 따로 개발해야함
* 웹에서 동작하는 프로그램은 예외 -> 모든 디바이스에서 사용 가능
* HTML5를 활용하면 Web을 넘어 Desktop 앱까지 개발 가능함 (ex. Electron, React Native)

![](https://camo.githubusercontent.com/627c774e3070482b180c3abd858ef2145d46303b/68747470733a2f2f656c656374726f6e6a732e6f72672f696d616765732f656c656374726f6e2d6c6f676f2e737667)

---

### React Native

* 2012년 전후로 Adobe PhoneGap을 사용해 HTML5로 모바일 앱을 만다는 시도가 다양히 이루어짐
* **Facebook**은 PhoneGap에 만족하지 못하고 모바일 앱을 만들 수 있게 하는 새로운 엔진 개발 (**React Native**)

<img src="https://miro.medium.com/max/1000/1*GkR93AAlILkmE_3QQf88Ug.png" style="zoom:50%;" />

* React Native를 사용하면 HTML5로 개발했을때 내부적을 안드로이드와 아이폰에 맞는 **Native Code**로 변함됨 (**AWESOME!**)
* Facebook, Instagram, Skype, Uber 모두 React Native로 개발됨

---

# HTML5 Tag Basics

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/61/HTML5_logo_and_wordmark.svg/1200px-HTML5_logo_and_wordmark.svg.png" style="zoom:25%;" />

(***Tip. 외우지 말고 ~한 태그가 있었구나 이해하기***)

### 태그(Tag)와 요소(Element)

* 태그는 HTML 페이지에서 객체 (요소)를 만들때 사용됨

```html
<h1>Hello World!</h1> <!-- 시작 & 끝 태그 pair-->
</br> <!-- 시작 / 끝 태그를 함께 사용하는 태그 -->

<!-- Nested tags -->
<article> 
	<h1>Heading</h1>
    <p>Paragraph</p>
</article>
```

* "요소 (element)를 생성" = "태그를 생성"

---

### 속성 (Attribute)

* 태그에 추가 정보를 부여할때 사용

```html
<h1 title="header">Heading with title attribute</h1>
<img src="image.png"/>
```

* 모든 태그와 속성은 W3C에서 표준으로 정의돼있음

---

### 주석 (Comment)

* 프로그램의 실행에 영향을 주지않고 **설명**을 위해 사용하는 코드

  <!-- Write some comments in here -->

---

### HTML5 페이지 구조

```html
<!DOCTYPE html>
<html>
    <head>
        <title>This is Title</title>
    </head>
    <body>
        <p>This is a paragraph</p>
    </body>
</html>
```

### `<!DOCTYPE>`

* 웹 브라우저가 현재 웹 페이지가 HTML5 문서임을 인식하게 만들어 줌
* 모든 HTML5 문서는 **반드시** 문서의 가장 첫 번째 줄에 작성

### `<html>`

* 모든 HTML 페이지의 **루트** 요소
* 모든 HTML 태그는 `<html>` 태그의 내부에 작성
* **lang** 속성을 입력할 수 있음

```html
<html lang="ko">
<!--
* 브라우저 동작에 영향 x
* 구글, 네이버 같은 검색 엔진이 해당 페이지가 어떤 언어로 만들어졌는지 쉽게 인식함 
-->
</html>
```

### `<head>`

- `<body>` 태그에서 필요한 **stylesheet**와 **자바스크립트**를 제공하는 데 사용
- `<head>` 태그에는 아래의 태그만 입력 가능

```html
<head>
    <meta>            웹 페이지에 추가정보를 전달
    <title></title>   웹 페이지의 제목
    <script></script> 웹 페이지에 스크립트를 추가
    <link />          웹 페이지에 다른 파일을 추가
    <style></style>   웹 페이지에 스타일시트를 추가
    <base>            웹 페이지의 기본 경로를 지정
</head>
```

### `<body>`

* 사용자에게 보이는 실제 부분

---

### 글자 태그

- 제목 글자 (heading)
- 본문 (paragraph)
- 앵커 (anchor)
- 글자 형태
- 루비문자

---

### Heading

```html
<h1>1st largest heading</h1>
<h2>2nd largest heading</h2>
             .
             .
             .
<h6>6th largest heading</h6>
```

* 각 브라우저마다 폰트는 다름

---

### Paragraph

```html
<p>하나의 단락 생성</p>
<hr/> 수평 줄 태그
<br/> 줄바꿈 태그
```

* Lorem ipsum

---

### Anchor

* HTML의 H는 Hypertext를 의미하며 이는 사용자의 선택에 따라 **특정한 정보와 관련된 부분으로 이동할 수 있게 조직화 된 문서**를 의미한다.

```html
<a herf="url">여기를 눌러주세요</a>
<!-- href 속성은 반드시 입력해야하며 속성 값에 "#"을 입력하여 빈 링크를 설정할 수 있음
```

* 앵커 태그 `<a>`는 **서로 다른 웹 페이지 사이를 이동**하거나, 웹 페이지 **내부에서 특정한 위치로 이동**할 때 사용

```html
<a href="#alpha">Move to Alpha</a>
<h1 id="alpha">Alpha</h1>
<!--
<a>를 통해 페이지 내부에서 원하는 장소로 이동 가능
이때는 원하는 장소에 id 속성을 부여하여 href 속성 값으로 #id를 입력
-->
```

---

### 글자 형태

```html
<b>굵은 글자</b>
<i>기울어진 글자</i>
<small>작은 글자</small>
<sub>아래에 달라붙는 글자</sub>
<sup>위에 달라붙는 글자</sup>
<ins>밑줄 글자</ins>
<del>가운데 줄이 그어진 글자</del>
```

---

### 루비 문자

* 한자 위에 표시되는 글자

![](https://www.w3docs.com/uploads/media/default/0001/01/b62d0c228cccda7416c2f5699af4d582f271b720.png)

---

### 목록 태그 - 기본 목록

```html
<body>
    <h3>Here is UNORDERED LIST</h3>
    <ul>
        <li>list item 1</li>	<!-- * list item 1 -->
        <li>list item 2</li>	<!-- * list item 2 -->
        <li>list item 3</li>	<!-- * list item 3 -->
    </ul>

    <h3>Here is ORDERED LIST</h3>
    <ol>
        <li>list item 1</li>	<!-- 1. list item 1 -->
        <li>list item 1</li>	<!-- 2. list item 2 -->
        <li>list item 1</li>	<!-- 3. list item 3 -->
    </ol>
</body>
```

---

### 목록 태그 - 정의 목록

```html
<body>
    <h3>Here is DEFINITION LIST</h3>
    <dl>
        <dt>Word to Explain</dt> <!-- definition term -->
        <dd>definition 1</dd> <!-- definition description -->
        <dd>definition 2</dd>
    </dl>
</body>
```

---

### 테이블 태그

* 

---

### 이미지 태그

* placehold.it

---

### 오디오 태그

* 

---

### 비디오 태그

* video.js

---

## FORM Tag

* action
* method (get vs. post)

### Input Tag (HTML5)

* Ajax

---

### Textarea Tag

* 

---

### Select Tag

* optgroup tag

---

### Fieldset & legend Tag

* 

---

## DIV & Span Tag

* 공간 분할 태그
* `<div>` block 형식으로 공간을 분할
* `<span>` inline 형식으로 공간 분할
* pg. 93
* **HTML5 콘텐츠 모델**

---

### HTML5 Semantic Tag

* **Semantic** : 의미론적인
* 기계적인 검색 엔진은 어떠한 태그가 어떠한 기능을 하는지 분별할 수 없음
* 이를 해결하고자 특정한 태그에 의미를 부여해서 웹 페이지를 만다는 시도가 시작 = Semantic Web

```html
<header></header> header
<nav></nav> navigation
<aside></aside> side area
<section></section> area for main content
<article></article> area for main content (words)
<footer></footer> footer
```

