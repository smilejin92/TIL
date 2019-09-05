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

### CSS INHERIT vs. Overide

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

