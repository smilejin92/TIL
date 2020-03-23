# HTML5 요소

## 1. 주요 범위

<h3>&lt;html&gt;</h3>

문서의 루트 요소로, 모든 HTML 요소는 루트 요소 내에 포함되어야 한다.

| 속성 | 의미                                                         | 값             |
| ---- | ------------------------------------------------------------ | -------------- |
| lang | 문서의 언어 ([ISO 639-1]([https://ko.wikipedia.org/wiki/ISO_639-1_%EC%BD%94%EB%93%9C_%EB%AA%A9%EB%A1%9D](https://ko.wikipedia.org/wiki/ISO_639-1_코드_목록))) | `ko`, `en` ... |

**포함할 수 있는 컨텐츠 모델**

* `<head>`
*  `<body>`

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>...</body>
</html>
```

&nbsp;    

### &lt;head&gt;

문서의 **메타데이터 집합 요소**로, 문서 제목, 스타일 파일 연결, 자바스크립트 삽입을 위한 요소들을 포함할 수 있다.

**포함할 수 있는 컨텐츠 모델**

* 1개 이상의 메타데이터 컨텐츠
* `<title>` (일부 조건 하에 생략 가능)

```html
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <link rel="stylesheet" ref="./css/style.css" />
    <script src="./js/main.js" defer></script>
  </head>
  <body>
    ...
  </body>
</html>
```

&nbsp;    

### &lt;body&gt;

문서의 본문 요소로, 문서 내에서 한 번만 사용할 수 있다.

**카테고리**: 섹셔닝 루트 (Sectioning Root)

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠 (Flow Content)

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <div class="container">
      <header>...</header>
      <main>...</main>
      <footer>...</footer>
    </div>
  </body>
</html>
```

&nbsp;    

## 2. 메타데이터

### &lt;title&gt;

문서의 제목 및 SEO를 위한 텍스트를 포함한다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

```html
<html lang="ko-KR">
  <head>
    <title>Website - HTML5, CSS, JavaScript</title>
  </head>
  <body>
    ...
  </body>
</html>
```

&nbsp;    

### &lt;meta &#47;&gt;

다양한 문서 정보를 나타낼 때 사용한다. 빈 요소(empty element)이다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

| 속성       | 의미                                                         | 값                               |
| ---------- | ------------------------------------------------------------ | -------------------------------- |
| charset    | [문자인코딩 방식](https://www.iana.org/assignments/character-sets/character-sets.xhtml) | `UTF-8`, `EUC-KR` ...            |
| name       | 메타 데이터의 이름([정보의 종류](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta#attr-name)) | `author`, `description`          |
| http-equiv | 서버/사용자 에이전트의 작동방식 변경에 대한 [지시](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta#attr-http-equiv)(HTTP 응답 헤더 제공) | `refresh`, `X-UA-Compatible` ... |
| content    | name, http-equiv의 값                                        |                                  |

```html
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="author" content="smilejin92" />
  </head>
</html>
```

&nbsp;    

### &lt;style&gt;

CSS를 문서 내에 직접 기술할 때 사용한다. CSS 코드만을 포함한다.

**카테고리**

* 메타데이터 컨텐츠 (Metadata Content)
* scope 속성이 정의된 경우 플로우 컨텐츠 (Flow Content)

| 속성 | 의미                                                         | 기본값     |
| ---- | ------------------------------------------------------------ | ---------- |
| type | [MIME 타입](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types) | `text/css` |

```html
<html lang="ko-KR">
  <head>
    ...
    <style type="text/css">
      body {
        margin: 0;
        padding: 0;
      }
    </style>
  </head>
</html>
```

&nbsp;    

### &lt;link &#47;&gt;

문서에 외부 문서를 연결할 때 사용한다. 빈 요소(empty element)이다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

| 속성 | 의미                                                         | 값                             |
| ---- | ------------------------------------------------------------ | ------------------------------ |
| rel  | (필수) 현재 문서와 외부 리소스와의 관계([Link types](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types)) | `stylesheet`, `icon` ...       |
| href | 외부 리소스의 URL                                            | URL                            |
| type | 외부 리소스의 MIME 타입                                      | `text/css`, `image/x-icon` ... |

```html
<html lang="ko-KR">
  <head>
    ...
    <link rel="stylesheet" ref="./css/style.css" />
  </head>
</html>
```

&nbsp;    

### &lt;base &#47;&gt;

문서의 상대 결로에 대한 기본 URL을 정의할 때 사용한다. **한 문서당 하나의 base 요소를 사용할 수 있다**. 빈 요소이다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

| 속성   | 의미                                             | 값                | 기본값  |
| ------ | ------------------------------------------------ | ----------------- | ------- |
| href   | 기준 URL                                         | URL               |         |
| target | a 요소처럼 target 속성을 사용하는 요소의 기본 값 | `_self`, `_blank` | `_self` |

```html
<html lang="ko-KR">
  <head>
    ...
    <base href="https://www.w3schools.com/" />
  </head>
  <body>
    <img src="images/logo.png" />
    <a href="tags/tag_base.asp">HTML base Tag</a>
  </body>
</html>
```

&nbsp;    

## 3. 컨텐츠 구분

### &lt;h1&gt; ~ &lt;h6&gt;

컨텐츠 블록의 제목(heading)을 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 헤딩 컨텐츠(Heading content)

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

**display 스타일**: block

```html
...
<body>
  <header>
    <h1>HTML5 요소</h1>
  </header>
  <main>
  	<section>
    	<h2>h1 태그란?</h2>
      <p>...</p>
    </section>
  </main>
</body>
```

&nbsp;    

### &lt;header&gt;

페이지나 섹션 등의 헤더를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠 (Flow content)
* 팰퍼블 컨텐츠 (Palpable content)

**포함할 수 있는 컨텐츠 모델**: `<header>`와 `<footer>`를 제외한 플로우 컨텐츠(Flow content)

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <header>
    	<h1>HTML5 요소</h1>
      ...
    </header>
  </body>
</html>
```

&nbsp;    

### &lt;main&gt;

문서의 주요 컨텐츠 영역을 정의할 때 사용하며, **문서에는 하나의 &lt;main&gt; 요소만 존재할 수 있다.**

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow content) 

**display 스타일**: block

```html
...
<body>
  <main>
  	<section>...</section>
    <section>...</section>
  </main>
</body>
```

&nbsp;    

### &lt;footer&gt;

페이지나 섹션 등의 푸터를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 팰퍼블 컨텐츠(Palpable content)

**포함할 수 있는 컨텐츠 모델**: `<header>`와 `<footer>`를 제외한 플로우 컨텐츠(Flow content)

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
  </body>
</html>
```

&nbsp;    

### &lt;section&gt;

장이나 절 등으로 구성할 수 있는 컨텐츠 섹션을 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠 (Flow content)
* 섹셔닝 컨텐츠 (Sectioning content)
* 팰퍼블 컨텐츠 (Palpable content)

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <header>...</header>
    <main>
    	<section>
      	<h2>section 요소</h2>
        ...
      </section>
    </main>
  </body>
</html>
```

&nbsp;    

### &lt;nav&gt;

문서의 주요 내비게이션을 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠 (Flow content)
* 섹셔닝 컨텐츠 (Sectioning content)

**포함할 수 있는 컨텐츠 모델**

* 플로우 컨텐츠
* 섹셔닝 컨텐츠
* 팰퍼블 컨텐츠 (Palpable content)

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <header>
    	<h1>HTML5 요소</h1>
      <nav>
      	<h2>메인 메뉴</h2>
        <ul class="main-menu">
          <li>...</li>
          ...
        </ul>
      </nav>
    </header>
    <main>...</main>
  </body>
</html>
```

&nbsp;    

### &lt;article&gt;

RSS 피드로 재배포할 가치가 있는 **독립된 컨텐츠**를 정의할 때 사용한다. 이때 반드시 RSS로 재배포할 것인지의 여부는 중요하지 않다.

**카테고리**

* 플로우 컨텐츠 (Flow contnet)
* 섹셔닝 컨텐츠 (Sectioning content)
* 팰퍼블 컨텐츠 (Palpable content)

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <header>...</header>
    <main>
    	<section class="news-room">
      	<article class="news" id="0">
        	<h2>HTML6 is coming</h2>
          ...
        </article>
      </section>
    </main>
  </body>
</html>
```

&nbsp;    

### &lt;aside&gt;

본문 컨텐츠와 연관성이 적은 컨텐츠를 정의할 때 사용한다.

**카테고리**: 플로우 컨텐츠 (Flow content)

**포함할 수 있는 컨텐츠 모델**

* 플로우 컨텐츠
* 섹셔닝 컨텐츠 (Sectioning content)
* 팰퍼블 컨텐츠 (Palpable conetnet)

**display 스타일**: block

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <header>...</header>
    <main>...</main>
    <aside>...</aside>
    <footer>...</footer>
  </body>
</html>
```

&nbsp;    

### &lt;address&gt;

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델** 

* 플로우 컨텐츠(Flow content)
* 헤딩 및 섹셔닝 컨텐츠(Sectioning content)를 포함할 수 없음

**display 스타일**: block

```html
...
<footer>
	<address>
	  <span class="name">smilejin92</span>
    <span class="email">smilejin92@gmail.com</span>
  </address>
</footer>
...
```

&nbsp;    

### &lt;div&gt;

컨텐츠 블록의 시맨틱한 의미를 가지고 있지는 않지만, 디자인이나 개발 이슈로 인해 컨텐츠 블록을 그룹화(division) 하고자 할 때 사용한다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow content) 

**display 스타일**: block

```html
...
<body>
  <div class="container">
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
  </div>
</body>
```

&nbsp;    

## 4. 문자 컨텐츠

### &lt;p&gt;

단락 컨텐츠를 정의할 때 사용한다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

**display 스타일**: block

```html
...
<body>
  <p>
    This is a paragraph.
  </p>
</body>
```

&nbsp;    

### &lt;ul&gt;

비순차 목록(unordered list)을 마크업 할 때 사용한다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: &lt;li&gt;

**display 스타일**: block

```html
...
<body>
  <ul>
    <li>item1</li>
    <li>item2</li>
  </ul>
</body>
```

&nbsp;    

### &lt;ol&gt;

순차 목록(ordered list)을 마크업 할 때 사용한다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: &lt;li&gt;

| 속성  | 의미                           | 값                      |
| ----- | ------------------------------ | ----------------------- |
| start | 항목에 매겨지는 번호의 시작 값 | 숫자 (Number)           |
| type  | 항목에 매겨지는 번호의 유형    | `a`, `A`, `i`, `I`, `1` |

**display 스타일**: block

```html
...
<body>
  <ol start="2">
    <li>item1</li> <!-- 2. itme1 -->
    <li>item2</li> <!-- 3. itme1 -->
  </ol>
</body>
```

&nbsp;    

### &lt;li&gt;

순차 또는 비순차 목록의 항목을 정의할 때 사용한다.

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow content)

**display 스타일**: block

```html
...
<body>
  <ul>
    <li>item1</li>
    <li>item2</li>
  </ul>
</body>
```

&nbsp;    

### &lt;dl&gt;

정의형 목록(description list)을 마크업 할 때 사용한다. 정의하려는 용어(define term)와 용어 설명(describe term)만을 포함한다. key/value 형태를 표시할 때 유용하다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**

* &lt;dt&gt;
* &lt;dd&gt;

**display 스타일**: block

### &lt;dt&gt;

정의형 목록의 용어 제목을 의미한다.

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow Content)

**display 스타일**: block

### &lt;dd&gt;

정의형 목록의 용어 설명을 의미한다.

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠 (Flow Content)

**display 스타일**: block

```html
...
<body>
  <dl>
    <dt>Coffee</dt>
    <dd>Black hot drink</dd>
  </dl>
</body>
```

&nbsp;    

### &lt;blockquote&gt;

인용 컨텐츠 블록을 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 섹셔닝 컨텐츠(Sectioning content) 

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow content)

| 속성 | 의미              | 값   |
| ---- | ----------------- | ---- |
| cite | 인용된 정보의 URL | URL  |

**display 스타일**: block

```html
<blockquote cite="https://www.huxley.net/bnw/four.html">
    <p>
      Words can be like X-rays, if you use them properly—they’ll go through anything. You read and you’re pierced.
  </p>
  <footer>
    —Aldous Huxley, <cite>Brave New World</cite>
  </footer>
</blockquote>
```

&nbsp;    

### &lt;pre&gt;

공백이나 줄바꿈 등의 입력 형식 그대로 화면에 렌더링 하고자 할 때 사용한다 (preformatted text).

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: block

```html
<pre>
  L          TE
    A       A
      C    V
       R A
       DOU
       LOU
      REUSE
      QUE TU
      PORTES
    ET QUI T'
    ORNE O CI
     VILISÉ
    OTE-  TU VEUX
     LA    BIEN
    SI      RESPI
            RER       - Apollinaire
</pre>
```

태그 안에 작성한 텍스트와 공백 문자 모두 그대로 출력된다.

&nbsp;    

### &lt;hr&gt;

단락의 주제를 구분하고자 할 때 사용한다. 빈 요소이다. 시각적 요소로 사용하면 안된다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**display 스타일**: block

&nbsp;    

## 5. 인라인 텍스트

### &lt;a&gt;

다른 페이지, 같은 페이지 위치(`#`, 해시 태그), 파일, 이메일 주소, 전화번호 등 다른 URL로 연결할 수 있는 **하이퍼링크**를 설정할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 
* 인터랙티브 컨텐츠(Interactive content)

**포함할 수 있는 컨텐츠 모델**: [**트랜스패어런트**](https://www.w3.org/TR/2011/WD-html5-20110525/content-models.html#transparent) (transparent)

| 속성     | 의미                                                         | 값                            | 기본값  | 특징      |
| -------- | ------------------------------------------------------------ | ----------------------------- | ------- | --------- |
| download | 이 요소가 리소스를 다운로드하는 용도임을 의미                | Boolean                       |         |           |
| href     | 링크 URL                                                     | URL                           |         | 생략 가능 |
| rel      | 현재 문서와 링크 URL의 관계([Link types](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types)) | `license`, `prev`, `next` ... |         |           |
| target   | 링크 URL의 표시(브라우저 탭) 위치                            | `_self`, `_blank`             | `_self` |           |
| type     | 링크 URL의 [MIME 타입](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types) | `text/html` ...               |         |           |

**display 스타일**: inline

```html
...
<body>
  <a href="https://google.com" target="_blank">google</a>
</body>
```

> **transparent** 컨텐츠 모델 (Transparent content models)
>
> 트랜스패어런트 요소의 컨텐츠 모델은, 해당 요소의 부모 요소의 컨텐츠 모델에 의해 결정된다. 또한, 트랜스패어런트 요소 하위에 올 수 있는 요소는, 해당 요소의 부모 요소의 하위에 올 수 있는 요소여야 한다.

&nbsp;    

### &lt;abbr&gt;

축약어(Abbreviation)를 지정할 때 사용한다. 보통 `title` 속성을 사용하여 전체 글자나 설명을 제공 한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <abbr title="HyperText Markup Language">HTML</abbr>
</body>
```

&nbsp;    

### &lt;b&gt;

문체가 다른 글자의 범위(Bring Attention)를 설정한다. 특별한 의미를 가지지 않으며 읽기 흐름에 도움을 주는 용도로 사용된다. 다른 태그가 적합하지 않은 경우 마지막 수단으로 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <p>
    This is a paragraph with <b>bolded text</b>.
  </p>
</body>
```

&nbsp;    

### &lt;mark&gt;

사용자의 관심을 끌기 위해 **하이라이팅**할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <p>
    This is a paragraph with <mark>highlighted text</mark>.
  </p>
</body>
```

&nbsp;    

### &lt;em&gt;

텍스트를 강조하고자 할 때 사용한다. 중첩이 가능하며, 중첩될수록 강조 의미가 강해진다. 정보통신보조기기 등에서 구두 강조로 발음된다. 기본적으로 이탈릭체(Italic type)로 표시된다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

**display 스타일**: inline

```html
...
<body>
  <p>
    This is a paragraph with <em>emphasized text</em>.
  </p>
</body>
```

&nbsp;    

### &lt;strong&gt;

의미의 중요성을 나타내기 위해 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <p>
    This paragraph contains <strong>strong importance</strong>.
  </p>
</body>
```

&nbsp;    

### &lt;i&gt;

HTML5에서 의미가 변한 요소로, 단순히 이탈릭체로 나타내기 위한 요소가 아니라 분위기를 전환하는 의미의 텍스트를 나타낸다. 전문 용어, 관용구, 이모지 등에 사용된다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

&nbsp;    

### &lt;dfn&gt;

문장 혹은 단락 내에서 용어를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <p>
    <dfn>Coffee</dfn> is a brewed drink prepared from roasted coffee beans, the seeds of berries from certain Coffea species.
  </p>
</body>
```

&nbsp;    

### &lt;cite&gt;

창작물에 대한 참조를 설정할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <blockquote>
    <p>
      It was a bright cold day in April, and the clocks were striking thirteen.
    </p>
    <footer>
    	First sentence in <cite><a href="http://www.george-orwell.org/1984/0.html">Nineteen Eighty-Four</a></cite> by George Orwell (Part 1, Chapter1).
    </footer>
  </blockquote>
</body>
```

&nbsp;    

### &lt;q&gt;

짧은 인용문을 설정할 때 사용한다 (inline quotation). 긴 인용문을 설정할 경우 `<blockquote>`를 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

| 속성 | 의미              | 값   |
| ---- | ----------------- | ---- |
| cite | 인용된 정보의 URL | URL  |

**display 스타일**: inline

&nbsp;    

### &lt;code&gt;

소스코드 범위를 설정할 때 사용한다 (inline code). 기본적으로 고정폭 (Monospace) 글꼴 계열로 표시된다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content)

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  <p>
    <code>const text = "text";</code> is a piece of JS code.
  </p>
</body>
```

&nbsp;    

### &lt;kbd&gt;

텍스트 입력 장치(키보드)에서 사용자 입력을 나타내는 텍스트 범위를 설정한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content)

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

**display 스타일**: inline

```html
...
<body>
  <p>
    <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>K</kbd>
  </p>
  <kbd>ESC</kbd>
</body>
```

&nbsp;    

### &lt;sub&gt;, &lt;sub&gt;

윗첨자 및 아래첨자를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content) 

**display 스타일**: inline

```html
...
<body>
  X<sup>4</sup> + Y<sup>2</sup>, H<sub>2</sub>O
</body>
```

&nbsp;    

### &lt;time&gt;

기계적으로 이해하거나 처리할 수 있는 날짜 및 시간 정보를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

| 속성     | 의미                                                         | 값   |
| -------- | ------------------------------------------------------------ | ---- |
| datetime | [유효한 날짜 문자](https://www.w3.org/TR/html51/infrastructure.html#dates-and-times) | Date |

**display 스타일**: inline

```html
...
<body>
  <p>
    The Cure will be celebrating their 40th anniversary on <time datetime="2018-07-07">July 7</time> in London's Hyde Park.
  </p>
</body>
```

&nbsp;    

### &lt;span&gt;

**인라인 텍스트를 그룹화할 때 사용한다.** 본질적으로 아무런 의미를 갖지 않는다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨텐츠(Phrasing content)

**display 스타일**: inline

```html
...
<body>
  <div class="box">
    <span class="text-group1">inline span tag</span>
  </div>
</body>
```

&nbsp;    

### &lt;br /&gt;

줄바꿈을 하고자 할 때 사용한다. 빈 요소이다.

**카테고리**

* 플로우 컨텐츠(Flow content)
* 프레이징 컨텐츠(Phrasing content)

&nbsp;    

## 5. 수정

### &lt;del&gt;

삭제된(변경된) 텍스트의 범위를 지정할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 

**포함할 수 있는 컨텐츠 모델**: 트랜스패어런트 (Transparent)

| 속성     | 의미                                                         | 값   |
| -------- | ------------------------------------------------------------ | ---- |
| cite     | 변경을 설명하는 리소스의 URI                                 | URI  |
| datetime | 변경이 일어난 [유효한 날짜 문자](https://www.w3.org/TR/html51/infrastructure.html#dates-and-times) | Date |

**display 스타일**: inline

&nbsp;    

### &lt;ins&gt;

새로 추가된(변경된) 텍스트의 범위를 지정할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content)
* 프레이징 컨텐츠(Phrasing content)

**포함할 수 있는 컨텐츠 모델**: 트랜스패어런트 (transparent)

| 속성     | 의미                                                         | 값   |
| -------- | ------------------------------------------------------------ | ---- |
| cite     | 변경을 설명하는 리소스의 URI                                 | URI  |
| datetime | 변경이 일어난 [유효한 날짜 문자](https://www.w3.org/TR/html51/infrastructure.html#dates-and-times) | Date |

&nbsp;    

## 6. 멀티미디어

### &lt;img /&gt;

이미지를 삽입할 때 사용한다. 빈 요소이다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 
* 임베디드 컨텐츠(Embedded content)
* 인터랙티브 컨텐츠(Interactive content) - `usemap` 속성이 있을 때

**포함할 수 있는 컨텐츠 모델**: 빈 컨텐츠

| 속성   | 의미                                                         | 값       |
| ------ | ------------------------------------------------------------ | -------- |
| src    | (필수) 이미지 URL                                            | URL      |
| alt    | (필수) 이미지의 대체 텍스트                                  |          |
| width  | 이미지의 가로 너비                                           |          |
| height | 이미지의 세로 너비                                           |          |
| srcset | 브라우저에게 제시할 이미지 URL과 원본 크기의 목록을 정의     | `w`, `x` |
| sizes  | 미디어 조건과 해당 조건일 때 이미지 최적화 크기의 목록을 정의 |          |

**display 스타일**: inline-block

```html
<!-- srcset, sizes -->
<!-- 다양한 디스플레이 해상도에 맞는 최적의 이미지를 브라우저가 선택해서 사용 -->
<img srcset="./small.jpb 320w,
             ./medium.jpg 640w,
             ./large.jpg 1024w"
     sizes="(max-width: 480px) 300px,
            (max-width: 800px) 400px,
            900px"
     src="./small.jpg"
     alt="the image" />
<img srcset="./image.jpg,
             ./image-1.5x jpg 1.5x,
             ./image-2x.jpg 2x"
     src="./image.jpg"
     alt="the image" />
     
```

&nbsp;    

### &lt;audio&gt;

소리 컨텐츠(ex. mp3)를 삽입할 때 사용한다. `autoplay`가 지정된 경우, `preload`는 무시된다.

**카테고리**

* 플로우 컨텐츠(Flow content)
* 프레이징 컨텐츠(Phrasing content)
* 임베디드 컨텐츠(Embedded content)
* 인터랙티브 컨텐츠(Interactive content) - `controls` 속성이 있을 경우

**포함할 수 있는 컨텐츠 모델**

* `<track>` - `src` 속성이 있는 경우
* `<source>`, `<track>` - `src` 속성이 없는 경우

| 속성     | 의미                                                  | 값                                                           | 기본값     |
| -------- | ----------------------------------------------------- | ------------------------------------------------------------ | ---------- |
| autoplay | 준비되면 바로 재생                                    | Boolean                                                      |            |
| controls | 제어 메뉴를 표시                                      | Boolean                                                      |            |
| loop     | 재생이 끝나면 다시 처음부터 재생                      | Boolean                                                      |            |
| preload  | 페이지가 로드될 때 파일을 로드할지의 지정 (힌트 제공) | `none`: 로드하지 않음&nbsp;   `metadata`: 메타데이터만 로드 &nbsp;  `auto`: 전체 파일 로드 | `metadata` |
| src      | 컨텐츠 URL                                            | URL                                                          |            |
| muted    | 음소거 여부                                           | Boolean                                                      |            |

**display 스타일**: inline

```html
<figure>
  <figcaption>Listen to the T-Rex:</figcaption>
  <audio controls src="./media/examples/t-rex-roar.mp3">
    Your broswer does not support the <code>audio</code> element.
  </audio>
</figure>
```

&nbsp;    

### &lt;video&gt;

동영상 컨텐츠(ex. mp4)를 삽입할 때 사용한다. `autoplay`가 지정된 경우, `preload`는 무시된다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 
* 임베디드 컨텐츠(Embedded content)
* 인터랙티브 컨텐츠(Interactive content) - `controls` 속성이 있을 경우

**포함할 수 있는 컨텐츠 모델** 

* transparent - `src` 속성이 있을 경우
* 1개 이상의 `<source>` - `src` 속성이 있을 경우

| 속성     | 의미                                                 | 값                                                           | 기본값     |
| -------- | ---------------------------------------------------- | ------------------------------------------------------------ | ---------- |
| autoplay | 준비되면 바로 재생                                   | Boolean                                                      |            |
| controls | 제어 메뉴를 표시                                     | Boolean                                                      |            |
| loop     | 재생이 끝나면 다시 처음부터 재생                     | Boolean                                                      |            |
| muted    | 음소거 여부                                          | Boolean                                                      |            |
| poster   | 동영상 썸네일 이미지 URL                             | URL                                                          |            |
| preload  | 페이지가 로드될 때 파일을 로드할지의 지정(힌트 제공) | `none`: 로드하지 않음&nbsp;   `metadata`: 메타데이터만 로드 &nbsp;  `auto`: 전체 파일 로드 | `metadata` |
| src      | 컨텐츠 URL                                           | URL                                                          |            |
| width    | 동영상 가로 너비                                     |                                                              |            |
| height   | 동영상 세로 너비                                     |                                                              |            |

**display 스타일**: inline

```html
<video controls width="250">
	<source src="./media/examples/flower.webm" type="video/webm" />
  <source src="./media/examples/flower.mp4" />
  Sorry, your browser doesn't support embedded videos.
</video>
```

&nbsp;    

### &lt;source&gt;

`<picture>`, `<video>`, `<audio>`의 폴백(fallback) 컨텐츠를 삽입할 때 사용한다. 빈 요소이다.

**포함할 수 있는 컨텐츠 모델**: 빈 컨텐츠



### &lt;track&gt;

`<audio>`, `<video>` 같은 미디어가 재생 중일 때 표시할 자막, 캡션 파일 등을 지정할 때 사용한다. 빈 요소이다.

&nbsp;    

### &lt;figure&gt;

figure 요소는 이미지, 오디오, 비디오, 표 등을 포함하는 그룹 영역을 의미한다.

**카테고리**

* 플로우 컨텐츠(Flow content)
* 섹셔닝 루트(Sectioning root)

**포함할 수 있는 컨텐츠 모델**

* 플로우 컨텐츠(Flow content) 
* &lt;figcaption&gt;

**display 스타일**: block

&nbsp;    

### &lt;figcaption&gt;

figcaption은 figure 요소에 포함된 컨텐츠에 대한 캡션을 정의할 때 사용된다.

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow content)

**display 스타일**: block

```html
...
<body>
	<figure>
  	<img src="/media/examples/elephant-660-480.jpg" alt="Elephant at sunset" />
    <figcaption>An elephant at sunset</figcaption>
  </figure>
</body>
```

&nbsp;    

## 7. 내장 컨텐츠

### &lt;iframe&gt;

다른 HTML 페이지를 현재 페이지에 삽입할 때 사용한다 (중첩된 브라우저 컨텍스트를 표시).

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨텐츠(Phrasing content) 
* 임베디드 컨텐츠 (Embedded content)
* 인터랙티브 컨텐츠(Interactive content)

**포함할 수 있는 컨텐츠 모델**: 텍스트

| 속성            | 의미                           | 값                                                           | 기본값 |
| --------------- | ------------------------------ | ------------------------------------------------------------ | ------ |
| name            | 프레임의 이름                  |                                                              |        |
| src             | 포함할 문서의 URL              | URL                                                          |        |
| width           | 프레임의 가로 너비             |                                                              |        |
| height          | 프레임의 세로 너비             |                                                              |        |
| allowfullscreen | 전체 화면 모드 사용 여부       | Boolean                                                      |        |
| frameborder     | 프레임 테두리 사용 여부        | `0`, `1`                                                     | `1`    |
| sandbox         | 보안을 위한 읽기 전용으로 삽입 | Boolean, &nbsp;  `allow-form`: 양식 제출 가능, &nbsp;  `allow-scripts`: 스크립트 실행 가능, &nbsp;  `allow-same-origin`: 같은 출저(도메인)의 리소스 사용 가능 |        |

**display 스타일**: inline

```html
<iframe width="1280" 
        height="720" 
        src="https://youtu.be/n-wLTtge5wE" 
        frameborder="0" 
        allowfullscreen>
</iframe>
```





## 9. 스크립트

### &lt;script&gt;

문서에 자바스크립트 파일을 삽입하거나 자바스크립트 코드를 기술할 때 사용한다.

**카테고리**

* 메타데이터 컨텐츠 (Metadata content)
* 플로우 컨텐츠 (Flow content)
* 프레이징 컨텐츠 (Phrasing content)

**포함할 수 있는 컨텐츠 모델**: 빈 컨텐츠

**고유 속성**

* async
* type
* charset
* defer
* src

```html
<html lang="ko-KR">
  <head>
    ...
    <script src="./js/main.js"></script>
  </head>
</html>
```

&nbsp;    

### &lt;noscript&gt;

자바스크립트를 지원하지 않을 경우 제공할 폴백(fall back) 컨텐츠를 정의할 때 사용한다.

**카테고리**

* 메타데이터 컨텐츠 (Metadata content)
* 플로우 컨텐츠 (Flow content)
* 프레이징 컨텐츠 (Phrasing content)

**포함할 수 있는 컨텐츠 모델**: 빈 컨텐츠

**고유 속성**

* async
* type
* charset
* defer
* src

```html
<html lang="ko-KR">
  <head>...</head>
  <body>
    <noscript>
    	자바스크립트를 지원하지 않습니다.
    </noscript>
  </body>
</html>
```
