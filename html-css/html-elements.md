# HTML5 요소

## 1. 주요 범위

### &lt;html&gt;

문서의 루트 요소로, 모든 HTML 요소는 루트 요소 내에 포함되어야 한다.

**속성**

* lang: 문서의 언어 (ex. ko, en)

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

---

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

---

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
&#10;

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

---

### &lt;meta&gt;

다양한 문서 정보를 나타낼 때 사용한다. 빈 요소(empty element)이다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

**고유 속성**

* name
* http-equiv
* content
* charset

```html
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="author" content="smilejin92" />
  </head>
</html>
```

---

### &lt;style&gt;

CSS를 문서 내에 직접 기술할 때 사용한다. CSS 코드만을 포함한다.

**카테고리**

* 메타데이터 컨텐츠 (Metadata Content)
* scope 속성이 정의된 경우 플로우 컨텐츠 (Flow Content)

**고유 속성**

* type
* media
* scoped

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

---

### &lt;link&gt;

문서에 외부 문서를 연결할 때 사용한다. 빈 요소(empty element)이다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

**고유 속성**

* href
* hreflang
* media
* rel
* sizes
* type

```html
<html lang="ko-KR">
  <head>
    ...
    <link rel="stylesheet" ref="./css/style.css" />
  </head>
</html>
```

---

### &lt;base&gt;

문서의 상대 결로에 대한 기본 URL을 정의할 때 사용한다. 한 문서당 하나의 base 요소를 사용할 수 있다. 빈 요소이다.

**카테고리**: 메타데이터 컨텐츠 (Metadata Content)

**고유 속성**

* href
* target

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

&nbsp  

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
...
```

---

### &lt;header&gt;

페이지나 섹션 등의 헤더를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠 (Flow content)
* 팰퍼블 컨텐츠 (Palpable content)

**포함할 수 있는 컨텐츠 모델**

* header와 footer를 제외한 플로우 컨텐츠(Flow content)

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

---

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

---

### &lt;footer&gt;

페이지나 섹션 등의 푸터를 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 팰퍼블 컨텐츠(Palpable content)

**포함할 수 있는 컨텐츠 모델**

* header와 footer를 제외한 플로우 컨텐츠(Flow content)

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

---

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

---

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

---

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

---

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

---

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

---

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

&#10;

## 4. 문자 컨텐츠

### &lt;p&gt;

단락 컨텐츠를 정의할 때 사용한다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨첸츠(Phrasing content)

**display 스타일**: block

```html
...
<body>
  <p>
    This is a paragraph.
  </p>
</body>
```

---

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

---

### &lt;ol&gt;

순차 목록(ordered list)을 마크업 할 때 사용한다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: &lt;li&gt;

**고유 속성**

* start
* reversed

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

---

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

---

### &lt;dl&gt;

정의형 목록(description list)을 마크업 할 때 사용한다. 정의하려는 용어(define term)와 용어 설명(describe term)만을 포함한다..

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

---

### &lt;blockquote&gt;

인용 컨텐츠 블록을 정의할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 섹셔닝 컨텐츠(Sectioning content) 

**포함할 수 있는 컨텐츠 모델**: 플로우 컨텐츠(Flow content)

**고유 속성**: cite

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

---

### &lt;pre&gt;

공백이나 줄바꿈 등의 입력 형식 그대로 화면에 렌더링 하고자 할 때 사용한다 (preformatted text).

**카테고리**: 플로우 컨텐츠(Flow content) 

**포함할 수 있는 컨텐츠 모델**: 프레이징 컨첸츠(Phrasing content) 

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

---

### &lt;hr&gt;

단락의 주제를 구분하고자 할 때 사용한다. 빈 요소이다.

**카테고리**: 플로우 컨텐츠(Flow content) 

**display 스타일**: block

&#10;

## 5. 인라인 텍스트

### &lt;a&gt;

하이퍼링크를 지정할 때 사용한다.

**카테고리**

* 플로우 컨텐츠(Flow content) 
* 프레이징 컨첸츠(Phrasing content) 
* 인터랙티브 컨텐츠(Interactive content)

**포함할 수 있는 컨텐츠 모델**: 트랜스페어런트 (transparent)

**고유 속성**

* href
* hreflang
* target
* download
* ref

**display 스타일**: inline



## &lt;figure&gt;

figure 요소는 이미지, 오디오, 비디오, 표 등을 포함하는 그룹 영역을 의미한다.

**카테고리**

* 플로우 컨텐츠(Flow content)
* 섹셔닝 루트(Sectioning root)

**포함할 수 있는 컨텐츠 모델**

* 플로우 컨텐츠(Flow content) 
* &lt;figcaption&gt;

**display 스타일**: block

## &lt;figcaption&gt;

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

---

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

---