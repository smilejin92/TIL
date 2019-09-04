# HTML5 Markup

([Lecture slides at here](https://github.com/seulbinim/pdf))

### 새로운 표준 HTML5

* **Content Models** : 명확한 정보 구조 설계 및 구성을 위해 카테고리를 정의하여, 비슷한 성격을 가진 요소별로 그룹화한 것

* **Category Examples**

  * Sectioning Root
  * Metadata Content
  * Flow Content
  * Sectioning Content
  * Heading Content
  * Sectioning Content

  ![](https://www.w3.org/TR/2011/WD-html5-20110525/content-venn.png)

---

### Outline Algorithm

* 정보 구조를 명확히 할 수 있도록 H TML5에 새롭게 도입된 개념
* 웹 페이지의 정보 구조를 판별할 수 있음 (ex. 목차)
* HTML5에 추가된 많은 요소들은 대부분 Outline Algorithm과 관련이 있음 (ex. Heading, Sectioning)

---

### HTML5의 API

* HTML5에서는 JS 기술을 편리하게 이용할 수 있도록 다양한 API를 지원
  * 오프라인 웹 구현을 위한 API (ex. Web Storage, Web SQL Database)
  * 실시간 커뮤니케이션 API (ex. Web Socket)
  * 파일/하드웨어 접근 API (ex. Desktop Drag-In, Geolocation)
  * API for GUI (ex. Drag & Drop)

---

### XML

- **Extensive Markup Language** : markup language that **DEFINES** a set of rules for encoding documents in a format that is **both human & machine readable**
  * (ex. `<item>`a110`</item>`)
- XML을 HTML에 적용 -> XHTML with **strict grammar**
  * (ex. `<br />`)

------

### HTML5 서식

* HTML 4.01, XHTML 1.0 등 기존에 사용하던 마크업 문법을 모두 허용 (하위 호환성)

---

### DTD (Document Type Definition)

* 모든 웹 문서의 시작은 문서형 정의 (DTD)의 선언으로 시작
* HTML5, XHTML, HTML 세 가지 문서 유형 존재
* **HTML5**에서 DTD 선언 = `<!DOCTYPE html>`
* HTML 4.01에서의 DTD ([see example](http://www.w3.org/TR/html4/loose.dtd))
  * Strict DTD
  * Transitional DTD
  * Frameset DTD

---

### 개발환경 설정

- Add Chrome Extension 
  - Web Developer
  - headingsMap
  - Tota11y
- Install Extension in VS Code
  - auto close tag
  - auto rename tag
  - monokai-contrast theme

---

### [Emmet](https://emmet.io/)

* a plugin for text editors which greatly improves HTML & CSS workflow (embedded in VS Code)

* [Documentation](https://docs.emmet.io/)

* [Shorcut Cheat Sheet](https://docs.emmet.io/cheat-sheet/) (example codes below)

  * Type `header` and hit enter -> `<header></header>`

  * Type `header.header` -> `<header class="header"></header>`

  * `header.class_name{요소}` -> `<header class="class_name">요소 값</header>`

  * header+div+main+article+footer

    ```html
    <header></header>
    <div></div>
    <main></main>
    <article></article>
    <footer></footer>
    ```

  * header>div (child tag)

    ```html
    <header>
        <div></div>
    </header>
    ```

  * div*3.group (make 3 div tags with class named "group")

    ```html
    <div class="group"></div>
    <div class="group"></div>
    <div class="group"></div>
    ```

  * div.group.group$*3 (dollar sign = incrementing number)

    ```html
    <div class="group group1"></div>
    <div class="group group2"></div>
    <div class="group group3"></div>
    ```

  * div.group.group${그룹$}*3 (also work in element value)

    ```html
    <div class="group group1">그룹1</div>
    <div class="group group2">그룹2</div>
    <div class="group group3">그룹3</div>
    ```

---

### HTML 페이지 디자인

1. 페이지 영역 분석

   * HTML page divided into 3 section (header, contents (body), footer)

     * header
     * contents
       * banner
       * main
       * slogan

     * footer

2. HTML로 Markup

```html
<!DOCTYPE html>
<html lang="ko-KR">
<head>
    <!-- type of encoding -->
    <meta charset="UTF-8">
    <!-- expose keywords that match to your purpose -->
    <title>keyword1, keyword2, keyword3</title>
</head>
<body>
    <header></header>
    <section>
        <header></header>
    </section>
</body>
</html>
```

3. Name Elements
   * Use Naming Convention
     * Camel Case (`var = 'camelCase'`)
     * Snake Case (`var = 'snake_case'`)
     * ?? (`var = 'temp-case'`)
   * id (unique) vs. class (group)

4. Code

---

### DOM (Document Object Model)

* A cross-platform and language interface that treats an XML or HTML document as a ***tree structure*** wherein each node is an object representing a part of the document.
* A document with a ***logical tree***

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/DOM-model.svg/1024px-DOM-model.svg.png)

# CSS3

* **box model**
* **box sizing**

