# CSS Property - continued

### [position](https://www.w3schools.com/css/css_positioning.asp)

([exercise](https://www.w3schools.com/css/exercise.asp?filename=exercise_positioning1))

* specify the **type of positioning method** used for an element
* elements are **then positioned using the top, bottom, left, and right properties (POSITION PROPERTY MUST BE SET FIRST)**

``` css
position: static; (default)
position: relative;
position: absolute;
position: fixed;
position: sticky; (IE or Edge 15 이전 버전 지원 x)

```



### position: static

* default value

* **NOT AFFECTED** by top, bottom, left, and right properties

* html 문서에 나온 순서 그대로 표시

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <style>
  div.static {
    position: static;
    border: 3px solid #73AD21;
  }
  </style>
  </head>
  <body>
  <div class="static">
    This div element has position: static;
  </div>
  
  </body>
  </html>
  ```

![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\position-static.PNG)



### position: relative

* positioned **relative to its normal position**
* setting **top, right, bottom, and left** properties of relatively-positioned element will cause it to be **adjusted away from its normal position**
* 이로 인해 생기는 여백은 다른 요소들로 **채워지지 않는다**

``` html
<!DOCTYPE html>
<html>
<head>
<style>
    div.relative {
      position: relative;
      left: 30px;
      border: 3px solid #73AD21;
    }
</style>
</head>
<body>
    <div class="relative">
    This div element has position: relative;
    </div>
</body>
</html>

```

![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\position-relative.PNG)



### position: fixed

* positioned relative to the **viewport**
* always stays in the same place even if the page is **scrolled**
* **top, right, bottom, left** properties are used to position the element

``` html
<!DOCTYPE html>
<html>
<head>
<style>
    div.fixed {
      position: fixed;
      bottom: 0;
      right: 0;
      width: 300px;
      border: 3px solid #73AD21;
    }
</style>
</head>
<body>
    <div class="fixed">
    	This div element has position: fixed;
    </div>
</body>
</html>

```

![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\position-fixed.PNG)



### position: absolute

* positioned **relative to the nearest positioned ancestor** (anything except **static**)
* if there's no positioned ancestors, it uses **the document body**
* allow you to **place your element precisely where you want it**
* 부모 노드가 position: relative면 영역 안에서 움직임 **(what if parent is set to absolute?)**

```css
HTML
<div id=”parent”>
  <div id=”child”></div>
</div>

CSS
#parent { 
  position: relative; 
  width: 500px; 
  height: 400px; 
  background-color: #fafafa; 
  border: solid 3px #9e70ba; 
  font-size: 24px; 
  text-align: center; 
} 
#child { 
  position: absolute; 
  right: 40px; 
  top: 100px; 
  width: 200px; 
  height: 200px; 
  background-color: #fafafa; 
  border: solid 3px #78e382; 
  font-size: 24px; 
  text-align: center; 
}
```

![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\position-absolute.PNG)



### Overlapping Elements

* Elements can overlap other elements
* `z-index` property specify the **stack order of an element** (앞으로 가져오기, 뒤로 가져오기)
* can have positive/negative stack order

``` css
img {
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: -1;
}
```

![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\z-index.PNG)

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