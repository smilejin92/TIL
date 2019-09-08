# CSS3

### Selector - 선택자

* 특정한 HTML 태그를 선택할 때 사용하는 기능

* 선택된 태그에 원하는 스타일 또는 기능을 적용

* 선택자 {스타일 속성: 스타일 값}

  (태그 선택자 예제)
  
  ```html
  스타일시트
  <style>
      h1 {
          color: red;
          background-color: orange;
      }
      /* h1 태그를 선택하여 해당 속성을 부여하라 */
  </style>
  ```

![](https://miro.medium.com/max/1527/1*0ACE4i1MCqXCnlBpdQHm3Q.jpeg)

---

### 전체 선택자

```css
* {
    color: red;
}
```

* `<html>`, `<head>`, `<title>`, `<style>`, `<body>` 태그 모두 선택

---

### 아이디 선택자

```html
#아이디 {
	color: red;
}
```

* **"id 속성은 웹 페이지 내부에서 중복되면 안된다"** -> CSS에선 문제 없지만 JS에서 선택시 문제

---

### 클래스 선택자

```html
<head>
    <style>
        .item {
            color: red
        }
        .heaer {
            background-color: blue;
        }
	</style>
</head>
<body>
    <h1 class="item header">Head 1</h1>
</body>
```

* 위와 같이 공백을 사이에 두고 여러 클래스를 사용할 수 있음

* 클래스 이름 중복 시, 태그 이름까지 더하여 정교하게 선택

  `li.select {color: red;}`

---

### 후손 선택자와 자손 선택자

```html
<body>
    <div>
        <h1>CSS3 Selector Basic</h1>   <!-- child / descendant-->
        <h2>Lorem ipsum</h2>		   <!-- child / descendant-->
        <ul>                           <!-- child / descendant-->
            <li>item1</li>             <!-- descendant -->
            <li>item2</li>			   <!-- descendant -->
            <li>item3</li>			   <!-- descendant -->
        </ul>
    </div>
</body>
```

* 위와 같은 코드에서 `<div>` 태그 **한 단계** 아래 있는 태그들을 **자손 / 후손**이라 명함
* `<div>` 태그에서 **두 단계 이상** 떨어져 있는 태그들을 **후손**이라 명함

``` css
/* 후손 선택자 */
tag1 tag2 {
    /* tag1의 후손에 위치하는 tag2를 선택 */
}
```

``` css
/* 자손 선택자 */
tag1 > tag2 {
    /* tag1의 자손에 위치하는 tag2를 선택 */
}
```

---

### 동위 선택자

* 동위 관계에서 뒤에 위치한 태그를 선택할 때 사용하는 선택자

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
          h1 ~ h2 {
              color: red;
          }
      </style>
  </head>
  <body>
      <h1>Header - 1</h1>
      <h2>Header - 2</h2>
      <h2>Header - 2</h2>
      <h2>Header - 2</h2>
      <h2>Header - 2</h2>
      <h2>Header - 2</h2>
  </body>
  </html>
  ```

* 위의 코드에서 `<h1>` 태그 뒤의 ***첫 번째*** `<h2>` 태그를 선택

  ```css
  h1 + h2 {
  	color: red;
  }
  ```

* `<h1>` 태그 뒤에 ***모든*** `<h2>` 태그를 선택

  ``` css
  h1 ~ h2 {
      color: red;
  }
  ```

---

### 구조 선택자

* CSS3부터 지원하는 선택자

* 자손 선택자와 병행하여 많이 사용

  #### 일반 구조 선택자

  * 특정한 위치에 있는 태그를 선택

  ``` css
  :first-child 형제 관계 중에서 첫 번째에 위치하는 태그
  :last-child 형제 관계 중에서 마지막에 위치하는 태그
  :nth-child(n) 형제 관계 중에서 앞에서 n번째 위치하는 태그
  :nth-child(n + 3) 형제 관계 중에서 앞에서 3번째 위치하는 태그부터 이후 모든 형제 태그
  :nth-last-child(n) 형제 관계 중에서 뒤에서 n번째 태그
  ```

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
          ul > li:nth-child(n+3) {
              color: red;
          }
      </style>
  </head>
  <body>
      <ul>
          <li>item 1</li>
          <li>item 2</li>
          <li>item 3</li>	<!-- colored with RED -->
          <li>item 4</li>	<!-- colored with RED -->
          <li>item 5</li>	<!-- colored with RED -->
          <li>item 6</li>	<!-- colored with RED -->
          <li>item 7</li>	<!-- colored with RED -->
      </ul>
  </body>
  </html>
  ```

---

### 가상 요소 선택자 (문자 선택자)

* 태그 내부 특정 조건의 문자를 선택하는 선택자

  #### 시작 문자 선택자

  * 태그 내부의 첫 번째 글자와 첫 번째 줄을 선택할 때 사용함

  ``` css
  ::first-letter 첫 번째 글자를 선택
  ::first-line 첫 번째 줄을 선택
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          p::first-letter {
              font-size: 3em;
          }
          p::first-line {
              color: red;
          }
      </style>
  </head>
  <body>
      <h1>제목</h1>
      <p>첫 번째 문장입니다</p>
      <p>두 번째 문장입니다</p>
  </body>
  </html>
  ```

  ![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\pseudo-element-selector.PNG)

  #### 전후 문자 선택자

  * 특정 태그의 전후에 위치하는 ***공간***을 선택하는 선택자

  ``` css
  ::after 태그 뒤에 위치하는 공간을 선택
  ::before 태그 앞에 위치하는 공간을 선택
  
  <h1 class="logo"><a href="#"><img src="./images/logo.png" alt="Web Cafe"></a></h1>
  <ul class="member">
      <li><a href="#">홈</a></li>
      <li><a href="#">로그인</a></li>
      <li><a href="#">회원가입</a></li>
      <li><a href="#">사이트맵</a></li>
      <li><a href="#">English</a></li>
  </ul>
  
  .member li:nth-child(n+2)::before {
      display: inline-block;
      background-color: orange;
      content: '\f142'; /* vertical ... menu */
  }
  ```

  ![](C:\Users\Jinhyun Kim\AppData\Roaming\Typora\typora-user-images\1567947825439.png)

---

### 링크 선택자 

* `href` 속성을 가지고 있는 `<a>` 태그에 적용되는 선택자

``` css
:link     href 속성을 가지고 있는 <a> 태그를 선택
:visited  방문했던 링크를 가지고 있는 <a> 태그를 선택
```

---

# CSS 스타일 속성

### CSS 단위

* `%` - 백분율 단위

* `em` - 배수 단위

* `px` - 픽셀

* `red, orange, blue, green` - 색상 단위

* `#000000` - 색상 단위 2 (HEX 코드 단위, #(red)(green)(blue))

* `rgb(red, green, blue)` - 색상 단위 3 (RGB 색상 단위)

* `url` - url 단위

  ```css
  body {
  	background-image: url('image.png')
  }
  ```
  
* linear-gradient(red, green)

---

### Display 속성

```css
display: none (태그를 화면에서 보이지 않게 설정)
display: block (태그를 block 형식으로 지정)
display: inline (태그를 inline 형식으로 지정)
display: inline-block (태그를 inline-block 형식으로 지정)
```

---

### Display: flex

```css
display: flex
```

* asdf
* asdf

---

### Visibility 속성 (NAH)

* 대상을 보이거나 보이지 않게 지정하는 스타일 속성

```css
visibility: visible
visibility: hidden
visibility: collapse (table 태그를 보이지 않게 설정, only available in IE & Firefox)
```

* So what's the difference btwn `display: none` & `visibility: hidden`?
* `display: none` -> 태그가 화면에서 **제거**
* `visibility: hidden` -> 화면에서 보이지 않을 뿐, hold space

(see also `position`)

```css
.a11y-hidden {
    background-color: red;
    position: absolute;
    width: 1px;
    height: 1px;
    overflow: hidden;
    margin: -1px;
    clip: rect(0,0,0,0);
    white-space: nowrap;
}
```



---

### Opacity 속성

* 태그의 투명도를 조절하는 스타일 속성
* 0.0 ~ 1.0 사이의 숫자를 입력할 수 있으며 0.0은 투명, 1.0은 불투명
* Example: `opacity: 0.2`

---

### 박스 속성 (pg. 174)

- **box model**
- **box sizing**

### 테두리 속성 (pg. 180)

### 배경 속성 (pg. 185)

### 위치 속성

### Float 속성

### 그림자 속성

### 웹 페이지 레이아웃 (ch. 5)

* 초기화
* 웹 폰트
* 수평 메뉴
* 콘텐츠 구성

---

### 고정형 레이아웃 설계

* Using `float`
* `display:inline`
* `display:block`
* `display:flex`
  * flexible
  * IE 10 or higher
  * `flex` 설정된 노드의 자식도 (flex item) 모두 flex 값 적용됨
    * `justify-content` (parent)
    * `flex-basis` (child) = 각 축에 해당하는 (width / height) 의 값을 설정
    * `order` ???
    * flex-grow
  * 기본 direction은 **row**로 변경됨 (default = column)
    * direction = row 일때 메인 축은 x 축 (가로)
    * direction = col 일때 메인 축은 y 축 (세로)
  * `flex`가 적용된 노드를 flex container라고 부름
  * 가질 수 있는 속성은 flex parent와 flex child마다 다름
  * https://flexboxfroggy.com/#ko

---

### Main Menu (Header) - GNB (Global Navigation Bar)

![main-menu](./images/main-menu.PNG)

* Logo
  * text, link, 모음?
  * image vs. IR (image replacement)

* Markup GNB

```html
<header>
	<h1 class="logo"><a href="#"><img src="image.png" /></a></h1>
    <ul>
        <li><a href="home">Home</a></li>
        <li><a href="login">Log in</a></li>
        <li><a href="join">Join</a></li>
    </ul>
</header>
<!-- try h1.logo>a[href="#"]>img -->
```

---

### Organizing CSS - Programming paradigm

* BEM
* OOCSS
* SMACSS

---

### Using Emmet

example)

홈

로그인

회원가입

사이트맵

English

(select 5 rows and ctrl + shift + p, then type "emmet wrap individual line with abbrev")

write emmet syntax

ul.member>li*>a[href="#"]

---

### CSS INHERIT vs. Override

inherits parent nodes' property

---

### 폰트 단위

under computed tab in developer tools (chrome)

`em` vs. `%`

`rem` (하위 버전에서 인식 못함) -> px 단위도 넣어줘야함

1.15 vs. 1.15em vs. 1.15%

---

### NORMALIZE CSS

http://necolas.github.io/normalize.css/latest/normalize.css

### FONT

https://fonts.google.com/

(Noto Sans)

`position:absolute/relative`

---

`display:inline-block`

`fork` target repo into your repo

clone it into your local machine

