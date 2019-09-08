# CSS Property - continued

### position

* `position:absolute/relative`

---

### display: float

* 

---

### -shadow

* text-shadow
* box-shadow

---

### Markup GNB (Global Navigation Bar)

![main-menu](C:/Users/Jinhyun Kim/Documents/dev/TIL/HTML-CSS/notes/images/main-menu.PNG)

- Logo
  - text, link
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
```

------

### Organizing CSS - Programming paradigm

- BEM
- OOCSS
- SMACSS

------

### Emmet Syntax for creating Menu

```html
1. 각 메뉴 이름 작성

홈
로그인
회원가입
사이트맵
English

2. 위의 메뉴를 마우스로 모두 선택하여 ctrl + shift + p

3. "emmet wrap individual line with abbrev" 입력

4. 입력란에 emmet 문법 작성
(ex. ul.member>li*>a[href="#"])

<ul class="member">
        <li>
            <a href="#">홈</a>
        </li>
        <li>
            <a href="#">로그인</a>
        </li>
        <li>
            <a href="#">회원가입</a>
        </li>
        <li>
            <a href="#">사이트맵</a>
        </li>
        <li>
            <a href="#">English</a>
        </li>
    </ul>
```

------

### CSS INHERIT vs. Override

* 



------

### 폰트 단위

under computed tab in developer tools (chrome)

`em` vs. `%`

`rem` (하위 버전에서 인식 못함) -> px 단위도 넣어줘야함

1.15 vs. 1.15em vs. 1.15%

------

### NORMALIZE CSS

http://necolas.github.io/normalize.css/latest/normalize.css

---

### External FONT

https://fonts.google.com/

(Noto Sans)

---

### Fork Repo in Github

`fork` target repo into your repo

clone it into your local machine

---

### Display 숨김처리

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

### Icon Font

* https://fontawesome.com/

* http://fontello.com/

---

### 여백 지정 대상

- margin vs. padding

- inline 요소는 좌우로는 늘어나지만 (padding, margin), 위로는 line-height의 영향을 받음

  (tab 키로 선택되는 요소들은 `<a>` 혹은 `<form>` -> focus )

---

### Main-menu Markup

```html
<h1> (not visible)
	<nav>
		<h2>메인 메뉴</h2> -> a11y.hidden (include for web accessibility)
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

---

### ROLE 부여

* Sementic 하지 않은 `<div>` 혹은 원래 목적의 `<a>` 같은 태그에 `role` 속성을 추가해 의미를 부여

---

### 요소 배치 속성

* grid (respoinsive)
* "margin" 병합

---

### aria-label

### border-radius

### 웹 페이지 레이아웃 (ch. 5)

([Back to List](../../README.md))