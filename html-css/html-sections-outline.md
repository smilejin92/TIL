#  HTML 섹션과 아웃라인 사용

HTML5 스펙은 문서를 체계화하기 위한 몇가지 시맨틱(semantic) 태그를 포함하고 있다. 시맨틱 요소는 브라우저, 개발자, 독자 그리고 문서를 해석하는 매체(ex. 음성 지원, 스크린 리더기)에 의미를 전달하기 위해 디자인되어있다.

예를 들어, `<div>` 태그는 아무 의미도 갖지 않지만, `<figcaption>` 태그는 자신이 포함하고 있는 컨텐츠를 명확히 설명한다.

웹사이트의 구역화(sectioning)를 개선하기 위해 새로운 시맨틱 요소들이 HTML5에 추가되었다. 이러한 시맨틱 요소들을 각 요소의 존재 목적, 혹은 설계 의도에 벗어나여 사용하는 것은 바람직하지 않다. 많은 접근성 도구들이 HTML5 시맨틱 요소에 의지하기 때문이다.

---

## HTML5의 섹션 요소

* **HTML Navigational 요소**(`<nav>`)는 사이트에서 자주 표시되는 링크들를 포함하는 영역을 정의한다. `<nav>` 요소를 primary 메뉴와 secondary 메뉴로서 사용할 수 있지만, `<nav>` 하위에 또 다른 `<nav>`가 위치할 수 없다.
* **HTML Article 요소**(`<article>`)는 자기 자신만을 포함하는 컨텐츠를 정의한다. `<article>` 요소는 다른 컨텐츠를 참조하지 않으며, 문서에서 분리되어 독릭접으로 사용될 수 있는 컨텐츠(ex. 위젯, RSS 피드)를 포함한다.
* **HTML Section 요소**(`<section>`)는 문서 내에서 서로 관련된 컨텐츠를 분류한 영역을 정의할 때 사용한다. 상위 컨텐츠에 대한 추가 설명이 필요한 경우 하위에 `<section>` 요소를 활용할 수 있다.
* **HTML Aside 요소**(`<aside>`)는 메인 요소에 관련돼있지만, 주흐름에서 벗어나는 컨텐츠(ex. 부가 설명 박스, 광고)를 포함한 영역을 정의할 때 사용한다. `<aside>` 요소는 자신만의 아웃라인을 가지고 있지만, 메인 아웃라인에 속하지는 않는다.

**구역화에 사용되는 다른 시맨틱 요소**

* **HTML Body 요소**(`<body>`)는 문서의 모든 컨텐츠와 HTML 태그를 포함하는 요소이다.
* **HTML Header 요소**(`<header>`)는 대체로 문서의 로고, 제목, 내비게이션을 포함하는 요소이다. `<header>` 요소는 `<article>`, `<section>`과 같은 다른 시맨틱 요소 혹은 특정 구역의 제목, 저자와 같은 정보를 담는 헤더로서 사용될 수 있다. `<article>`, `<section>`, `<aside>`, `<nav>` 요소는 자신만의 `<header>`르ㄹ 포함할 수 있다.  `<header>`라는 이름과 달리 문서의 시작 혹은 구역의 시작 부분에 위치하지 않아도된다.
* **HTML Footer 요소**(`<footer>`)는 대체로 문서의 저작권, 법적 고지, 링크를 포함하고 있다. 또한 특정 구역의 작성 날짜, 라이센스 정보 등을 포함할 수 있다. `<article>`, `<section>`, `<aside>`, `<nav>` 요소는 자신만의 `<footer>`를 포함할 수 있다. `<footer>`라는 이름과 달리 문서의 끝 혹은 구역의 끝 부분에 위치하지 않아도 된다.

### 섹셔닝 요소 예제

```html
<body>
  <header>
    <h1>Page Title</h1>
  	<nav>
    	<ul>
        <li><a href="#">link</a></li>
        <li><a href="#">link</a></li>
        <li><a href="#">link</a></li>
      </ul>
    </nav>
  </header>
  <section>
  	<h2>My Blog Posts</h2>
    <article>
    	<header>
      	<p>Article Title</p>
      </header>
      <p>Article Content</p>
    </article>
    <aside>
    	<p>Author info</p>
    </aside>
  </section>
  <footer>Copyright Info</footer>
</body>
```

&nbsp;  

### Nav 요소

`<nav>` 요소는 내비게이션 영역을 의미하며 주요 navigational 메뉴로서 사용되어야 한다.

```html
<nav>
	<ul>
    <li><a href="#">link</a></li>
    <li><a href="#">link</a></li>
  </ul>
</nav>
```

&nbsp;  

#### 중첩 메뉴

`<nav>` 요소는 중첩하여 사용하지 않는다. 단, `<nav>` 요소는 primary, secondary 메뉴를 둘 다 포함할 수 있다.

```html
<nav>
	<ul>
    <li><a href="#">primary link</a></li>
    <li>
      <a href="#">primary link</a>
    	<ul>
        <li><a href="#">secondary link</a></li>
        <li><a href="#">secondary link</a></li>
      </ul>
    </li>
    <li><a href="#">primary link</a></li>
  </ul>
</nav>
```

&nbsp;  

#### 링크의 모음

`<nav>` 요소는 오로지 사이트 내비게이션 메뉴로서 사용되어야 한다. 소셜 미디어 프로필 혹은 자주 찾는 블로그와 같은 링크의 모음은 `<nav>` 요소에 포함되어서는 안된다.

&nbsp;  

#### &lt;nav&gt; 하위 요소

내비게이션 안에 목록 요소가 주로 쓰이지만, 필수적인 것은 아니다. `<p>`와 같은 다른 요소들도 사용할 수 있다.

&nbsp;  

---

### Article 요소

