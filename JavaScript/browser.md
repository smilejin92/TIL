# 브라우저의 렌더링 과정

* 픽셀은 상대적 단위이다. 내 모니터의 1픽셀과 다른 사람 모니터의 1픽셀이 다를 수 있다.
* html은 문서의 구조와 정보를 제공한다.
* html 태그 안에는 컨텐트(텍스트 혹은 다른 태그)가 올 수 있다.
* 중첩된 태그는 문서의 구조를 나타낸다.
* self closing tag는 컨텐트를 포함하지 않기 때문에 닫는 태그가 없다.
* 브라우저는 홈페이지 주소(호스트 이름)를 입력 받으면 DNS에 해당 호스트 이름과 바인딩되어 있는 IP주소를 따라 홈페이지 서버에 도착한다.
* 도메인 입력은 요청을 생성한다.
* http는 단방향 통신이다.
* 서버 컴퓨터가 요청된 html 파일을 메모리에 2진수로 읽어 들여 패킷 단위로 쪼갠 후 응답한다. (utf-8이란걸 알려준다.)
* 클라이언트는 반환된 패킷들을 모아 html로 다운로드 한다. (utf-8 포맷이란걸 알고있다.)
* html 문서의 요소를 다시 쪼개어 해석한다(요소별로 객체를 만든다 - NODE)
* 문서의 구조를 나타내기 위해 NODE를 트리 형태로 담은 DOM을 생성한다.
* head 태그에는 메타정보, body 태그에는 렌더링 해야할 컨텐트 정보가 들어있다.
* 레이아웃(요소의 좌표 설정) + 페인팅(픽셀에 점 찍기) = 렌더링
* 렌더링 엔진 = 위의 일들을 처리하는 브라우저의 소프트웨어
* 자바스크립트는 렌더링을 제어한다.

&nbsp;  

구글의 V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임 환경(runtime envrionment)인 Node.js의 등장으로 자바스크립트는 웹 브라우저를 벗어나 서버 사이드 애플리케이션 개발에서도 사용할 수 있는 범용 개발 언어가 되었다. 하지만 자바스크립트가 가장 많이 사용되는 분야는 역시 웹 브라우저 환경에서 동작하는 웹 페이지/애플리케이션의 **클라이언트 사이드**이다.

대부분의 프로그래밍 언어는 운영 체제(OS)나 가상 머신 위에서 실행되지만, 웹 애플리케이션의 클라이언트 사이드 자바스크립트는 **브라우저에서 HTML, CSS와 함께 실행된다.** 따라서 효율적인 클라이언트 사이드 자바스크립트 프로그래밍을 하기 위해서는 **브라우저 환경**을 고려해야한다.

이를 위해 브라우저가 HTML, CSS, 자바스크립트로 작성된 텍스트 문서를 어떻게 파싱(parsing, 해석)하여 브라우저에 렌더링하는지 살펴보자.

아래 그림은 **브라우저의 렌더링 과정**(critical rendering path)을 간략히 표현한 것이다.

<img src="https://user-images.githubusercontent.com/32444914/82745471-c6eda980-9dbf-11ea-82bd-4a89c2f04d6a.png" width="80%" />

1. 브라우저는 HTML, CSS, 자바스크립트, 이미지, 폰트 파일 등 **렌더링에 필요한 리소스를 요청하고 서버로부터 응답 받는다.**
2. **브라우저의 렌더링 엔진**은 서버로부터 응답된 HTML과 CSS를 **파싱**하여 **DOM과 CSSOM을 생성**하고 이들을 결합하여 **렌더 트리**를 생성한다.
3. **브라우저의 자바스크립트 엔진**은 서버로부터 응답된 자바스크립트를 **파싱**하여 **AST(Abstract Syntax Tree)를 생성하고 바이트 코드로 변환하여 실행**한다. 이때 자바스크립트는 DOM API를 통해 DOM, CSSOM을 변경할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.
4. 렌더 트리를 기반으로 HTML 요소의 **레이아웃**(위치와 크기)를 계산하고, 브라우저의 화면에 HTML 요소를 **페인팅**한다.

&nbsp;  

## 1. 요청과 응답

브라우저의 핵심 기능은 **필요한 리소스를 서버에 요청(request)하고, 서버의 응답(response)을 받아 브라우저에 시각적으로 렌더링하는 것**이다. 즉, 렌더링에 필요한 리소스는 모두 서버에 존재하므로, 필요한 리소스를 서버에 요청하고 서버가 응답한 리소스를 파싱(parsing)하여 렌더링 하는 것이다.

> <strong>리소스(Resource)</strong>
>
> HTML, CSS, 자바스크립트, 이미지, 폰트 등의 정적 파일 또는 서버가 동적으로 생성한 데이터

서버에 요청을 하기 위해 브라우저는 주소창을 제공한다. 브라우저의 주소창에 URL을 입력하고 엔터 키를 입력하면, URL의 호스트 이름은 DNS를 통해 IP 주소로 변환되고, 이 IP 주소를 갖는 서버에게 요청(request)를 전송한다.

<img src="https://user-images.githubusercontent.com/32444914/82746318-521f6d00-9dc9-11ea-8971-514fe8ed848b.png" width="80%" />

예를 들어 브라우저의 주소창에 `https://poiemaweb.com`을 입력하고 엔터 키를 입력하면 루트 요청(`/`, scheme과 호스트 이름만으로 구성된 URL에 의한 요청)이 poiemaweb.com 서버로 전송된다. **루트 요청에는 명확히 리소스를 요청하는 내용이 없기 때문에 일반적으로 서버는 루트 요청에 대해 암묵적으로 index.html을 응답하도록 기본 설정되어 있다.** 즉, `https://poiemaweb.com`은 `https://poiemaweb.com/index.html`과 같은 요청이다.

따라서 서버는 루트 요청에 대해 서버의 루트 폴더에 존재하는 정적 파일 index.html을 클라이언트(브라우저)로 응답한다. 만약 index.html이 아닌 다른 정적 파일을 서버에 요청하려면 브라우저의 주소창에 `https://poiemaweb.com/assets/data/data.json`과 같이 요청할 정적 파일 경로(서버의 루트 폴더 기준)와 파일 이름을 호스트 이름 뒤에 기술하여 서버에 요청한다. 그러면 서버는 루트 폴더의 assets/data 폴터 내에 있는 정적 파일 data.json을 응답할 것이다.

요청과 응답은 개발자 도구의 Network 패널에서 확인할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/82746509-767c4900-9dcb-11ea-8704-34535cf2c2a0.png" width="60%" />

위 그림을 살펴보면 index.html(poiemaweb.com)뿐만 아니라 CSS, 자바스크립트, 이미지, 폰트 파일들도 응답된 것을 확인할 수 있다.  이는 브라우저의 렌더링 엔진이 HTML(index.html)을 파싱하는 중 **외부 리소스를 로드하는 태그**(`<link>`, `<img>`, `<script>` 등)를 만나면 HTML의 파싱을 일시 중단하고 해당 리소스 파일을 서버로 요청하기 때문이다.

&nbsp;  

## 2. HTTP 1.1 vs. HTTP 2.0

HTTP(HyperText Transfer Protocol)는 웹에서 <strong>브라우저와 서버가 통신을 하기 위한 프로토콜(규약)</strong>이다. 1989년 HTML, URL과 함께 팀 버너스 리 경이 고안한 HTTP는 1991년 최초로 문서화되었고 1996년 HTTP/1.0, 1999년 HTTP/1.1, 2015년 HTTP/2가 발표되었다. 이중 **HTTP/1.1과 HTTP/2 버전의 차이**에 대해 간략히 살펴보자.

**HTTP/1.1**

<img src="https://user-images.githubusercontent.com/32444914/82746758-631ead00-9dce-11ea-8ebd-1072eb144837.png" width="30%" />

* 커넥션당 하나의 요청과 응답 만을 처리
* HTML 문서 내에 포함된 외부 리소스 요청(`<link>`, `<img>`, `<script>` 등)은 개별적으로 전송되고 응답 또한 개별적으로 전송
* 리소스의 동시 전송이 불가능한 구조이므로 요청할 리소스의 개수에 비례하여 응답 시간도 증가

&nbsp;  

**HTTP/2.0**

<img src="https://user-images.githubusercontent.com/32444914/82746777-96f9d280-9dce-11ea-81a1-bd23a4eadaed.png" width="30%" />

* 커넥션당 여러 개의 요청과 응답, 즉 다중 요청/응답이 가능
* HTTP/1.1에 비해 페이지 로드 속도가 약 50% 빠르다고 한다.

&nbsp;  

## 3. HTML 파싱과 DOM 생성

1. 서버에 존재하던 HTML 파일이 브라우저의 요청에 의해 응답된다. 이때 서버는 브라우저가 요청한 HTML 파일을 읽어 들여 메모리에 저장한 다음 메모리에 저장된 바이트(2진수)를 인터넷을 경유하여 응답한다.
2. 브라우저는 서버가 응답한 HTML 문서를 바이트(2진수) 형태로 응답 받는다. 그리고 바이트 형태의 HTML 문서는 meta 태그의 charset 어트리뷰트에 의해 지정된 **인코딩** 방식(ex. utf-8)을 기준으로 **문자열로 변환**된다.
3. 문자열로 변환된 HTML 문서를 읽어 들여 **문법적 의미를 갖는 코드의 최소 단위인 토큰(token)들로 분해**한다.
4. **각 토큰들은 객체로 변환하여 노드(node)들을 생성**한다. 토큰의 내용에 따라 문서 노드, 요소 노드, 어트리뷰트 노드, 텍스트 노드가 생성된다. 노드는 이후 DOM을 구성하는 기본 요소가 된다.
5. HTML 문서는 HTML 요소들의 집합으로 이루어지며 **HTML 요소는 중첩 관계를 가진다.** 즉, HTML 요소의 컨텐츠 영역(시작 태그와 종료 태그 사이)에는 텍스트 뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이때 HTML 요소 간에는 중첩 관계에 의해 부자 관계가 형성된다. 이러한 HTML 요소 간의 부자 관계를 반영하여 모든 노드들을 **트리 자료 구조**로 구성한다. 이 노드들로 구성된 트리 자료 구조를 **DOM(Document Object Model) 혹은 DOM Tree**라고 부른다.

&nbsp;  

브라우저의 요청에 의해 서버가 응답한 HTML 문서는 문자열로 이루어진 순수한 텍스트이다. 순수한 텍스트인 HTML 문서를 브라우저에 시각적인 픽셀로 렌더링 하려면 **HTML 문서를 브라우저가 이해할 수 있는 자료구조(객체)로 변환하여 메모리에 저장**해야 한다.

예를 들어 아래와 같은 index.html이 서버로부터 응답되었다고 가정해보자.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <ul>
      <li id="apple">apple</li>
      <li id="banana">banana</li>
      <li id="orange">orange</li>
    </ul>
    <script src="app.js"></script>
  </body>
</html>
```

브라우저의 렌더링 엔진은 아래 그림과 같은 과정을 통해 **응답 받은 HTML 문서를 파싱하여 DOM(Document Object Model)을 생성**한다.

<img src="https://user-images.githubusercontent.com/32444914/82746962-1cca4d80-9dd0-11ea-82b5-b9c5165b414a.png" width="80%" />

즉, **DOM은 HTML 문서를 파싱한 결과물이다.**

&nbsp;  

## 4. CSS 파싱과 CSSOM 생성

* 바이트 -> 문자 -> 토큰 -> 노드 -> CSSOM

&nbsp;  

렌더링 엔진은 HTML을 처음부터 한줄씩 순차적으로 파싱해서 DOM을 생성해 나간다. 이때 렌더링 엔진은 CSS를 로드하는 `<link>` 태그나 `<style>` 태그를 만나면 DOM 생성을 일시 중단한다.

그리고 `<link>` 태그의 `href` 어트리뷰트에 정의된 CSS 파일을 서버에 요청하여 로드한 CSS나, `<style>` 태그내의 CSS를 HTML과 동일한 파싱 과정(바이트 -> 문자 -> 토큰 -> 노드 -> CSSOM)을 통해 해석하여 <strong>CSSOM(CSS Object Model)</strong>을 생성한다. 이후 CSS 파싱을 완료하면 HTML 파싱이 중단된 지점부터 다시 HTML을 파싱하기 시작하여 DOM 생성을 재개한다.

위에서 살펴본 index.html을 다시 살펴보자. index.html에는 CSS 파일을 로드하는 `<link>` 태그가 존재한다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
    ...
```

렌더링 엔진은 meta 태그까지 HTML을 순차적으로 해석한 다음, link 태그를 만나면 DOM 생성을 일시 중단하고 link 태그의 href 어트리뷰터에 정의된 CSS 파일을 서버에 요청한다. 예를 들어, 아래와 같은 style.css 파일이 서버로부터 응답되었다고 가정해보자.

```css
body {
  font-size: 18px;
}

ul {
  list-style-type: none;
}
```

서버로부터 CSS 파일이 응답되면 렌더링 엔진은 HTML과 동일한 해석 과정(바이트 -> 문자 -> 토큰 -> 노드 -> CSSOM)을 거쳐 CSS를 파싱하여 CSSOM을 생성한다.

CSSOM은 CSS의 상속을 반영하여 생성된다. 위 예제에서 body 요소에 적용한 `font-size` 프로퍼티와 ul 요소에 적용한 `list-style-type` 프로퍼티는 모든 li 요소에 상속된다. 이러한 상속 관계가 반영되어 아래와 같이 CSSOM이 생성된다.

<img src="https://user-images.githubusercontent.com/32444914/82747635-07f0b880-9dd6-11ea-9241-4ebf8d66ad1c.png" width="60%" />

&nbsp;  

## 5. 렌더 트리 생성

* 렌더링을 위한 트리 구조의 자료 구조
* 완성된 렌더 트리는 각 HTML 요소의 레이아웃(위치와 크기) 계산에 사용되며, 브라우저 화면에 픽셀을 렌더링 하는 페인팅 처리에 입력된다.
* 레이아웃 계산과 페인팅을 다시 실행하는 리렌더링은 성능에 악영향을 주는 작업이다.

&nbsp;  

렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 각각 DOM과 CSSOM을 생성한다. 그리고 DOM과 CSSOM은 렌더링을 위해 <strong>렌더 트리(render tree)</strong>로 결합된다.

렌더 트리는 **렌더링을 위한 트리 구조의 자료 구조**이다. 따라서 브라우저 화면에 렌더링되지 않는 노드(ex. `<meta>`, `<script>` 태그 등)와 CSS에 의해 비표시(ex. `display: none`)되는 노드들은 포함하지 않는다. 다시 말해, **렌더 트리는 브라우저 화면에 렌더링되는 노드들로만 구성된다.** 

<img src="https://user-images.githubusercontent.com/32444914/82747742-391db880-9dd7-11ea-99d4-28f7f86ee6da.png" width="80%" />

이후 완성된 렌더 트리는 각 HTML 요소의 레이아웃(위치와 크기) 계산에 사용되며, 브라우저 화면에 픽셀을 렌더링하는 페인팅(painting) 처리에 입력된다.

<img src="https://user-images.githubusercontent.com/32444914/82747767-69655700-9dd7-11ea-97d7-3ec7a5e43a78.png" width="60%" />

지금까지 살펴본 브라우저의 렌더링 과정은 반복해서 실행될 수 있다. 예를 들어 아래와 같은 경우, 반복해서 레이아웃 계산과 페인팅이 재차 실행된다.

* 자바스크립트에 의한 노드 추가 또는 삭제
* 브라우저 윈도우의 리사이징에 의한 viewport 크기 변경
* HTML 요소의 레이아웃(크기, 위치)에 변경을 발생시키는 `width`, `height`, `margin`, `padding`, `border`, `display`, `position`, `top`, `right`, `bottom`, `left` 등의 스타일 변경

&nbsp;  

레이아웃 계산과 페인팅을 다시 실행하는 **리렌더링은 비용이 많이 드는, 즉 성능에 악영향을 주는 작업이다**. 따라서 가급적 빈번한 리렌더링이 발생하지 않도록 주의가 필요하다.

&nbsp;  

## 6. 자바스크립트 파싱과 실행

<strong>1. 토크나이징(tokenizing)</strong>

단순한 문자열인 소스 코드를 어휘 분석(lexical analysis)하여 문법적 의미를 가지는 코드의 최소 단위인 토큰(token)들로 분해한다.

<strong>2. 파싱(parsing)</strong>

토큰들의 집합을 구문 분석(syntatic analysis)하여 <strong>AST(Abstract Syntax Tree, 추상적 구문 트리)</strong>를 생성한다. AST는 토큰에 문법적 의미와 구조를 반영한 트리 구조의 자료 구조이다.

**3. 바이트 코드 생성과 실행**

파싱의 결과물로서 생성된 AST는 인터프리터가 실행할 수 있는 중간 코드(intermediate code)인 바이트 코드(bytecode)로 변환되고 인터프리터에 의해 실행된다.

&nbsp;  

HTML 문서를 파싱한 결과물로서 생성된 DOM은 HTML 문서의 구조와 정보 뿐만 아니라, HTML 요소와 스타일 등을 변경할 수 있는 프로그래밍 인터페이스로서의 DOM API를 제공한다. 즉, **자바스크립트 코드에서 DOM API를 사용하면 이미 생성된 DOM을 동적으로 조작할 수 있다.**

CSS 파싱 과정과 마찬가지로 렌더링 엔진은 HTML을 한줄씩 순차적으로 파싱하며 DOM을 생성해 나가다가, 자바스크립트 파일을 로드하는 `<script>` 태그나 자바스크립트 코드를 컨텐츠로 가지는 `<script>` 태그를 만나면 DOM 생성을 일시 중단한다.

그리고 `<script>` 태그 `src` 어트리뷰트에 정의된 자바스크립트 파일을 서버에 요청하여 로드한 자바스크립트 코드나, `<script>` 태그 내의 자바스크립트 코드의 파싱을 위해 자바스크립트 엔진에 제어권을 넘긴다. 이후 자바스크립트 파싱과 실행이 종료되면 렌더링 엔진으로 다시 제어권을 넘겨 HTML 파싱이 중단된 지점부터 다시 HTML 파싱을 시작하여 DOM 생성을 재개한다.

**자바스크립트 파싱과 실행은** 브라우저의 렌더링 엔진이 아닌 **자바스크립트 엔진이 처리한다.** 자바스크립트 엔진은 자바스크립트 코드를 CPU가 이해할 수 있는 저수준 언어(low-level language)로 변환하는 역할을 한다. 자바스크립트 엔진은 구글 크롬과 Node.js의 V8, 파이어폭스의 SpiderMonkey, 사파리의 JavaScriptCore 등 다양한 종류가 존재하며, 모든 자바스크립트 엔진은 ECMAScript 사양을 준수한다.

렌더링 엔진으로부터 제어권을 넘겨 받은 자바스크립트 엔진은 자바스크립트 코드를 파싱하기 시작한다. 렌더링 엔진이 HTML과 CSS를 파싱하여 DOM과 CSSOM을 생성하듯 자바스크립트 엔진은 자바스크립트를 해석하여 <strong>AST(Abstract Syntax Tree, 추상적 구문 트리)</strong>를 생성한다. 그리고 AST를 기반으로 인터프리터가 실행할 수 있는 중간 코드(intermediate code)인 바이트 코드(bytecode)를 생성하여 실행한다.

<img src="https://user-images.githubusercontent.com/32444914/82748450-eba44a00-9ddc-11ea-9a2f-b6442e93f71a.png" width="70%" />

&nbsp;  

## 7. 리플로우와 리페인트

만약 자바스크립트 코드에 DOM이나 CSSOM을 변경하는 DOM API가 사용된 경우, DOM이나 CSSOM이 변경된다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합되고 **변경된 렌더 트리를 기반으로 레이아웃과 페인트 과정을 거쳐 브라우저의 화면에 다시 렌더링한다. 이를 리플로우(reflow), 리페인트(repaint)라 한다.**

<img src="https://user-images.githubusercontent.com/32444914/82748609-75a0e280-9dde-11ea-82c7-c6546c0cd56c.png" width="80%" />

**리플로우**는 레이아웃 계산을 다시 하는 것을 말하며 노드 추가/삭제, 요소의 크기/위치 변경, 윈도우 리사이징 등 **레이아웃**에 영향을 주는 변경이 발생한 경우에 한하여 실행된다.

**리페인트**는 재결합된 렌더 트리를 기반으로 다시 페인팅 하는 것을 말한다.

따라서 리플로우와 리페인트가 반드시 순차적으로 동시에 실행되는 것은 아니다. 레이아웃에 영향이 없는 병견은 리플로우 없이 리페인트만 실행된다.

&nbsp;  

## 8. 자바스크립트 파싱에 의한 HTML 파싱 중단

지금까지 살펴본 바와 같이 렌더링 엔진과 자바스크립트 엔진은 병렬적으로 파싱을 실행하지 않고 **직렬적**으로 파싱을 수행한다.

<img src="https://user-images.githubusercontent.com/32444914/82748718-25765000-9ddf-11ea-8810-5cf70dd23505.png" width="70%" />

이처럼 브라우저는 동기적(synchronous)으로, 즉 위에서 아래 방향으로 순차적으로 HTML, CSS, 자바스크립트를 파싱하고 실행한다. 이것은 **script 태그의 위치에 따라 HTML 파싱이 블로킹되어 DOM 생성이 지연될 수 있다는 것**을 의미한다. 따라서 **script 태그의 위치는 중요한 의미를 가진다.**

위 예제의 경우, app.js의 파싱과 실행 이전까지는 DOM의 생성이 일시 중단된다. 이때 자바스크립트 코드(app.js)에서 DOM이나 CSSOM을 변경하는 DOM API를 사용할 겨우, DOM이나 CSSOM이 이미 생성되어 있어야 한다. 만약 DOM을 변경하는 DOM API를 사용할 때 DOM의 생성이 완료되지 않은 상태라면 문제가 발생할 수 있다.

아래는 script 태그의 위치에 의해 블로킹이 발생하는 예제이다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
    <script>
    	const $apple = document.getElementById('apple');
      $apple.style.color = 'red';
      // TypeError: Cannot read property 'style' of null
    </script>
  </head>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
  </body>
</html>
```

자바스크립트 코드 내에서 DOM API `document.getElementById('apple')`를 실행하는 시점에는 아직 DOM API가 참조하는 HTML 요소가 파싱되어 DOM에 포함되지 않은 상태이므로, 위 예제는 정상적으로 동작하지 않는다.

이러한 문제를 회피하기 위해 **script 태그의 위치를 body 요소 최하단으로 이동**시킬 수 있다. 그 이유는 아래와 같다.

* DOM이 완성되지 않은 상태에서 자바스크립트가 DOM을 조작한다면 에러가 발생한다.
* 자바스크립트 스크립트 로딩/파싱/실행으로 인한 HTML 요소들의 렌더링에 지장 받는 일이 발생하지 않아 페이지 로딩 시간이 단축된다.

&nbsp;  

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
    <script>
    	const $apple = document.getElementById('apple');
      $apple.style.color = 'red';
      // Success!
    </script>
  </body>
</html>
```

&nbsp;  

## 9. script 태그의 async / defer 어트리뷰트

앞에서 살펴본 **자바스크립트 파싱에 의한 DOM 생성이 중단(blocking)되는 문제를 근본적으로 해결하기 위해** HTML5부터 script 태그에 `async`와 `defer` 어트리뷰트가 추가되었다.

async와 defer 어트리뷰트는 src 어트리뷰트를 통해 **외부 자바스크립트 파일을 로드하는 경우에만 사용**한다. 즉, src 어트리뷰트가 없는 인라인 자바스크립트에는 사용할 수 없다.

```html
<script src="external.js" async></script>
<script src="external.js" defer></script>
```

async와 defer 어트리뷰트를 사용하면 **HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다.** 하지만 **자바스크립트의 실행 시점에 차이가 있다.**

&nbsp;  

**1. async 어트리뷰트**

HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다. 단, **자바스크립트의 파싱과 실행은 자바스크립트 로드가 완료된 직후 진행되며, 이때 HTML 파싱이 중단된다.**

<img src="https://user-images.githubusercontent.com/32444914/82749691-e39cd800-9de5-11ea-9805-bcdf75a3660f.png" width="70%" />

여러 개의 script 태그의 async 어트리뷰트를 지정하면 **script 태그의 순서와는 상관없이 로드가 완료된 자바스크립트부터 먼저 실행**되므로 순서가 보장되지 않는다. 따라서 순서 보장이 필요한 script 태그에는 async 어트리뷰트를 지정하지 않아야 한다. IE10 이상 버전에서 지원된다.

&nbsp;  

**2. defer 어트리뷰트**

HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다. 단, **자바스크립트의 파싱과 실행은 HTML 파싱이 완료된 직후(DOM 생성이 완료된 직후) 진행된다.**

<img src="https://user-images.githubusercontent.com/32444914/82749778-82293900-9de6-11ea-92fc-09f7c2e09483.png" width="70%" />

따라서 DOM 생성이 완료된 이후 실행되어야 할 자바스크립트에 유용하다. IE10 이상 버전에서 지원된다.

&nbsp;  

## 출처

* [poiemaweb.com - 브라우저의 렌더링 과정](https://poiemaweb.com/fastcampus/browser-rendering)

