# CSS3 - Position, Float, Font

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

* html 문서에 나온 순서 그대로 표시 (normal flow)

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

![](./images/position-static.PNG)



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

![](./images/position-relative.PNG)



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

![](./images/position-fixed.PNG)



### position: absolute

* positioned **relative to the nearest positioned ancestor** (anything except **static**)
* if there's no positioned ancestors, it uses **the document body** (ex. `<body>`)
* allow you to **place your element precisely where you want it**
* 부모 노드에 `position` 속성이 부여되어 있으면, 부모 영역을 기준으로 좌표를 설정하여 배치 가능

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

![](./images/position-absolute.PNG)



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

![](./images/z-index.PNG)

---



## [float](https://www.w3schools.com/css/css_float.asp)

* `float` property specifies **how an element should float**
* element with `position: absolute` **ignores** `float` property
* To avoid elements flowing around `float` element, use `clear` property

```css
float: none; (default, element does not float)
float: left; (the element floats to the left of its container)
float: right; (the element floats to the right of its container)
float: initial (back to default value)
```

* `float` takes elements **away from normal document flow**, so they **no longer occupies any HEIGHT in normal document flow**
* `float` 되는 요소는 기존의 박스 크기를 잃고, 컨텐츠의 높이/넓이만큼의 크기를 가짐. 따라서, 필요에 따라 **높이/넓이를 재설정 해줘야함**
* **position** 속성과 함께 같이 사용할 수 있음

([see more examples with `float`](https://www.w3schools.com/css/css_float.asp))



### float - Line Box

고정된 너비 안에 여러개의 요소가 float 되면, float 요소의 너비 합이 컨테이너의 너비를 초과하여 아래로 떨어짐. 이 과정에서 아래로 떨어진 요소는 바로 이전의 요소의 라인 박스 높이 만큼 공간이 추가되어 떨어짐.



## [clear](https://www.w3schools.com/css/css_float.asp)

* `clear` property specifies **what elements can float beside the cleared element and on which side**

``` css
clear: none; (allow floating elements on both sides)
clear: left; (No floating elements allowed on the left side)
clear: right; (No floating elements allowed on the right side)
clear: both; (No floating elements allowed on either the left or the right side)

/* example */
.blue {
   float: left; /* it sitll wants to float, */
   clear: left; /* but not something (float element) on the left */
}
```

* non-floating element 안에 floating element를 올려놓을 수 있음 (using clearfix)

---

### [clearfix Hack](https://www.w3schools.com/howto/howto_css_clearfix.asp)

* float 설정된 요소가 자신을 감싸고 있는 부모 영역보다 크면 (**HEIGHT**), 부모 영역 밖으로 **overflow** 됨. 
* 아래와 같은 코드에서 menu-item 클래스를 float 시키면 부모 요소인 menu의 높이가 사라짐

``` html
<style>
    .menu {
        background: skyblue;
    }
    .menu-item {
        width: 100px;
        height: 100px;
        border: 1px solid black;
        background: orange;
        float: left;
    }
</style>

<div class="menu">
    <div class="menu-item">HTML</div>
    <div class="menu-item">CSS</div>
    <div class="menu-item">웹표준</div>
</div>
```

(before float: left)

![](./images/clearfix1.PNG)



(after float: left)

![](./images/clearfix2.PNG)



위와 같은 문제를 해결하기 위해 **부모 요소**인 menu 클래스에 clearfix를 설정

``` html
<style>
	.menu {
        background: skyblue;
    }
    .clearfix::after {
		content: "";
        clear: both;
        display: table;
    }
    /*
    or
    .clearfix {
    	overflow: auto;
    }
    */
    .menu-item {
        width: 100px;
        height: 100px;
        border: 1px solid black;
        background: orange;
        float: left;
    }
</style>

<div class="menu clearfix">
    <div class="menu-item">HTML</div>
    <div class="menu-item">CSS</div>
    <div class="menu-item">웹표준</div>
</div>
```

(after clearfix)

![](./images/clearfix3.PNG)



---

### [overflow](https://www.w3schools.com/css/css_overflow.asp)

* `overflow` property controls **what happens to content that is too big to fit into an area**
* specify whether **to clip** the content or **to add scrollbars** when the content of an element is too big to fit in the specified area
* **ONLY WORKS for block elements with a specified height**
* OS X Lion에서는 `overflow: scroll`을 부여해도, 컨텐트가 모두 표시될 경우 스크롤바가 보이지않음

``` css
overflow: visible (default value, the overflow is not clipped, renders outside the box)
overflow: fidden (overflow is clipped, the rest of the content will be INVISIBLE)
overflow: scroll (overflow is clipped, and a scrollbar is added to see the rest)
overflow: auto (add scrolbars ONLY WHEN NECESSARY)
```



### overflow: visible

* 넘치는 내용물을 자르지 않고 그대로 출력, 요소의 박스 밖으로 렌더링 됨

![](./images/overflow-visible.PNG)



### overflow: hidden

* 넘치는 내용물이 잘려나감

![](./images/overflow-hidden.PNG)





### overflow: scroll

* 넘치는 내용물이 잘린 뒤, 스크롤바가 박스 안에 생성됨 (가로, 세로 방향으로 모두 생성)

![](./images/overflow-scroll.PNG)



### overflow: auto

* 내용물이 넘칠때만 스크롤바 생성

![](./images/overflow-auto.PNG)

### overflow-x & overflow-y

* `overflow-x`: 내용물의 좌우 끝 부분을 어떻게 처리할건지 지정
* `overflow-y`: 내용물의 상하 끝 부분을 어떻게 처리할건지 지정

```css
div {
  overflow-x: hidden; /* Hide horizontal scrollbar */
  overflow-y: scroll; /* Add vertical scrollbar */
}
```



---

### white-space

* 요소 안의 공백을 어떻게 처리할 것인지 결정하는 속성
* 대부분의 경우 **줄바꿈을 허용하지 않을 때** 사용

``` css
white-space: normal (기본값, 연속되는 공백을 하나의 공백으로 처리. 필요한 경우 문자는 자동으로 wrap)
white-space: nowrap (연속되는 공백을 하나의 공백으로 처리. 문자는 <br>을 만나기 전까지 절대 다음 줄로 넘어가지 않음)
white-space: pre (브라우저에 의해 모든 공백이 보존됨. <br>에 의해 다음 줄로 넘어감)
white-space: pre-line (연속되는 공백을 하나의 공백으로 처리. 문자는 <br> 혹은 필요할 때에 다음 줄로 넘어감)
white-sapce: pre-wrap (브라우저에 의해 모든 공백이 보존됨. 문자는 <br> 혹은 필요할 때에 다음 줄로 넘어감)
```



---

### text-overflow

* specify how overflowed content (text) should be signaled to the user
* MUST INCLUDE `white-space` and `overflow` properties when using `text-overflow`

``` css
.example {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: clip; /* default value, the text is clipped and not accessible */
    text-overflow: ellipsis; /* represent the clipped text as "..." */
}
```

* [Multi-line Ellipsis CSS](http://hackingui.com/front-end/a-pure-css-solution-for-multiline-text-truncation/)



---

### -shadow effects

* `text-shadow`: 문자에 그림자 속성을 부여

``` css 
h1 {
    text-shadow: 2px 2px 5px red;/* horizontal shadow, vertical shadow, blur, color */
    text-shadow: 0 0 3px #FF0000, 0 0 5px #0000FF /* multiple shadows */
}
```



* `box-shadow`: 요소에 그림자 속성을 부여

``` css
div {
    box-shadow: 10px 10px 5px grey; /* horizontal shadow, vertical shadow, blur, color */
}

/* 가상 요소에 box-shadow 속성 부여 가능 */
div::after {
    box-shadow: 0 15px 20px rgba(0, 0, 0, 0.3);
}
```

**(box-shadow는 마진에 영향을 주지 않음)**



---

### border-radius

* 요소의 모서리를 둥글게 만드는 CSS 속성

``` css
#example1 {
  border: 2px solid red;
  /* 모든 모서리를 둥글게 설정 */
  border-radius: 25px;
  
  /* (왼쪽 위, 오른쪽 위)를 50px, (왼쪽 밑, 오른쪽 밑)를 20px 둥글게 설정 */
  border-radius: 50px 20px;
  
  /* 왼쪽 위, 오른쪽 위, 오른쪽 밑, 왼쪽 밑을 해당 값만큼 둥글게 설정 */
  border-radius: 15px 50px 30px 15px;
}
```



---

### Organizing CSS - Programming paradigm

- OOCSS (Object Oriented CSS)

- BEM (Block Element Modifier)

- SMACSS (Scalable and Modular Architecture for CSS)

  ([see more](https://mattstauffer.com/blog/organizing-css-oocss-smacss-and-bem/))



---

### NORMALIZE.CSS

* a CSS file that provides better **cross-browser consistency** in the default styling of HTML elements
* an alternative to [CSS resets](https://meyerweb.com/eric/tools/css/reset/)
* **preserve useful browser defaults** rather than erasing them
* **Normalize styles** for a wide range of HTML elements
* **Correct bugs** and common browser inconsistencies.

``` css
@import url('https://necolas.github.io/normalize.css/latest/normalize.css');
```

​	[(see more)](http://necolas.github.io/normalize.css/latest/normalize.css)



---

### CSS INHERIT vs. Override Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            margin: 10px;
            padding: 10px;
            background-color: green;
        }
        .box1 {
            background-color: blue;
        }
    </style>
</head>
<body>
    <!-- INHERITS the properties from div selector  -->
    <div>this is div 1</div>
    
    <!-- INHERITS the properties from div selector and OVERRRIDE background-color -->
    <div class="box1">this is div2</div>
</body>
</html>
```



---

### Markup GNB (Global Navigation Bar)

![main-menu](./images/main-menu.PNG)

- Logo
  - text, link
  - image vs. IR (image replacement - **see a11y.hidden below**)
- Markup GNB

```html
<h1> (.a11y-hidden)
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
</h1>
```



#### a11y-hidden

* 스크린 리더에는 읽히지만, 눈에서는 보이지 않게 설정
* Semantic한 마크업을 위해 html에 요소를 추가하는 대신, 보이지 않게 처리함으로써 의미론적, 시각적 효과를 모두 부여할 수 있음

``` CSS
.a11y-hidden {
      /* clip으로 자르기 위해 pos: abs 설정 */
      position: absolute;
      width: 1px;
      height: 1px;

      /* Setting a negative top margin indicates that you want negative spacing above
    your block. Negative spacing may in itself be a confusing concept, but just the way
    positive top margin pushes content down, a negative top margin pulls content up. */
      margin: -1px;

      /* 개행 금지 */
      white-space: nowrap;

      /* 영역 밖으로 넘치는건 보이지 않게 */
      overflow: hidden;
      
      /* position: absolute, fixed 된 요소에만 사용 가능한 속성
      요소의 어느 부분을 보이게 할지 정의
      rect(top, right, bottom, left) */
      clip: rect(0,0,0,0);
    }
```



------

### Emmet - Wrap individual line with abbrev

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



---

### WEB FONT

* 웹 브라우저는 사용자의 컴퓨터에 설치된 폰트만 사용할 수 있음
* 웹 폰트는 사용자가 웹 페이지에 접속하는 순간 폰트를 자동으로 내려받고 해당 웹 페이지에서 사용할 수 있게 만들어주는 기능
* [구글 무료 폰트 서비스](https://fonts.google.com/) : 원하는 폰트를 선택한 후 폰트 링크를 css 파일에 `import` 

``` css
@import url('https://spoqa.github.io/spoqa-han-sans/css/SpoqaHanSans-kr.css');

body{
  font-family: 'Spoqa Han Sans';
}
```



---

### Icon Font

- Instead of containing letters or numbers, they contain symbols and glyphs.
- can be styled with CSS in the same way you style regular text
- https://fontawesome.com/
- http://fontello.com/

```css
@import url('./fontello.css');

.member li:nth-child(n+2)::before{
  font-family: "fontello";
  content: '\f142';
}
```



---

### Image Replacement

* CSS image replacement: technique of replacing a text element (ex. h1) with **image (logo)**

```css
/* padding을 활용한 IR */
.brand1 {
    /* 배경 이미지 지정 */
    background: url(./images/title.png) no-repeat;
    
    /* 배경 이미지 너비 지정 */
    width: 290px;
    
    /* 해당 요소의 높이를 0 처리하여 컨텐츠가 overflow되게끔 설정 */
    height: 0px;
    
    /* 배경 이미지 높이 지정 (요소 패딩에 삽입) */
    padding-top: 195px;
    
    /* 요소의 높이가 0이 되어 overflow된 컨텐츠를 숨김 */
    overflow: hidden;
}

/* text-indent를 활용한 IR */
.brand2 {
    /* 배경 이미지 설정 */
    background: url(./images/title.png) no-repeat;
    
    /* 배경 이미지 너비/높이 설정 */
    width: 290px;
    height: 195px;
    
    /* 텍스트 시작 전, 배경이미지 너비만큼 공백 삽입 */
    text-indent: 290px;
    
    /* text-indent로 밀려난 텍스트를 개행 금지 처리 */
    white-space: nowrap;

    /* 영역 밖 컨텐츠를 숨김 처리 */
    overflow: hidden;
}

/* 위 두 방법의 단점: 서버 연결이 불안정하여 이미지가 로드되지 않으면, 대체 텍스트가 보이지 않음  */
/* 이미지로 텍스트 덮어버리기, 이미지가 로드되지 않아도, 뒤의 텍스트가 보임 */

.brand3 {
    /* 이미지 너비/높이 설정 */
    width: 290px;
    height: 195px;

    /* 라인 박스의 높이를 설정. line-height를 height과 동일하게 설정하면, 영역내 가운데 정렬
    (수직 정렬)이 이루어지는 것처럼 설정할 수 있음. 단, height 값이 바뀌면 line-height도
    다시 바꿔줘야함. */
    line-height: 195px;

    /* 블록 요소 안의 컨텐츠를 가운데 정렬 */
    text-align: center;

    font-size: 16px;
    font-weight: 400;
    
    /* 가상요소가 배치될 수 있도록 relative를 설정 */
    position: relative;
}
.brand3::before { /* or ::after */
    content:"";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: url(./images/title.png) no-repeat;
}
```



([prev - CSS Selector& Flex Box](./css-selector-flex.md))

([next - CSS Animation](./css-float-animation.md))

([Back to List](../../README.md))