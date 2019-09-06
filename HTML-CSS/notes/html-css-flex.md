# CSS3

### Selector - 선택자

* 특정한 HTML 태그를 선택할 때 사용하는 기능

* 선택된 태그에 원하는 스타일 또는 기능을 적용

* 선택자 {스타일 속성: 스타일 값}

  ```html
  스타일시트
  <style>
      h1 {
          color: red;
          background-color: orange;
      }
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

* "id 속성은 웹 페이지 내부에서 중복되면 안된다" -> CSS에선 문제 없지만 JS에서 선택시 문제

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

