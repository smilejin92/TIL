### 위치 속성 (position)

### Float 속성

### 그림자 속성

### 웹 페이지 레이아웃 (ch. 5)

------

### 고정형 레이아웃 설계

- Using `float`
- `display:inline`
- `display:block`
- `display:flex`
  - flexible
  - IE 10 or higher
  - `flex` 설정된 노드의 자식도 (flex item) 모두 flex 값 적용됨
    - `justify-content` (parent)
    - `flex-basis` (child) = 각 축에 해당하는 (width / height) 의 값을 설정
    - `order` ???
    - flex-grow
  - 기본 direction은 **row**로 변경됨 (default = column)
    - direction = row 일때 메인 축은 x 축 (가로)
    - direction = col 일때 메인 축은 y 축 (세로)
  - `flex`가 적용된 노드를 flex container라고 부름
  - 가질 수 있는 속성은 flex parent와 flex child마다 다름
  - https://flexboxfroggy.com/#ko

------

### Main Menu (Header) - GNB (Global Navigation Bar)

![main-menu](C:/Users/Jinhyun Kim/Documents/dev/TIL/HTML-CSS/notes/images/main-menu.PNG)

- Logo
  - text, link, 모음?
  - image vs. IR (image replacement)
- Markup GNB

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

------

### Organizing CSS - Programming paradigm

- BEM
- OOCSS
- SMACSS

------

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

------

### CSS INHERIT vs. Override

inherits parent nodes' property

------

### 폰트 단위

under computed tab in developer tools (chrome)

`em` vs. `%`

`rem` (하위 버전에서 인식 못함) -> px 단위도 넣어줘야함

1.15 vs. 1.15em vs. 1.15%

------

### NORMALIZE CSS

http://necolas.github.io/normalize.css/latest/normalize.css

### FONT

https://fonts.google.com/

(Noto Sans)

`position:absolute/relative`

------

`display:inline-block`

`fork` target repo into your repo

clone it into your local machine



숨김처리

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







* [Icon Font 사용 가능](https://fontawesome.com/)

  ```html
  <i class="fas fa-camera"></i> <!-- this icon's 1) style prefix == fas and 2) icon name == camera -->
  <i class="fas fa-camera"></i> <!-- using an <i> element to reference the icon -->
  <span class="fas fa-camera"></span> <!-- using a <span> element to reference the icon -->
  ```

* http://fontello.com/

---

* :hover
* :focus

---

### 여백 지정 대상

- margin vs. padding
- inline 요소는 좌우로는 늘어나지만 (padding, margin), 위로는 line-height의 영향을 받음

(tab 키로 선택되는 요소들은 `<a>` 혹은 `<form>`)

### Main-menu Markup

```html
<h1> (not visible)
	<nav>
		<h2>메인 메뉴</h2> -> a11y.hidden (accessibility)
        <ul class="menu">
            <li>
                (<a> vs. <span>)
                <a class="btn-menu" href="#" role="button">HTML에 대해</a>
                <ul class="sub-menu">
                    <li><a href="page1">예제 1</a></li>
                    <li><a href="page2">예제 2</a></li>
                    <li><a href="page3">예제 3</a></li>
                </ul>
            </li>
        </ul>
	</nav>
</h1> (not visible)
```

### ROLE 부여

* Sementic 하지 않은 `<div>` 혹은 원래 목적의 `<a>` 같은 태그에 `role` 속성을 부여하여 sementic 문제 해결

### 요소 배치 속성

* flex

* inline-block

* position

* ### float: 특 떠있음

  * 뜨는 순간 다음 요소가 당겨서 들어와짐?
  * float의 부모 노드에게 overflow: hidden 설정
  * clear

* grid (respoinsive)

* "margin" 병합

### aria-label

### border-radius



([Back to List](../../README.md))