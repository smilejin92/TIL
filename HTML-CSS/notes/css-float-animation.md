# CSS3 - Animation

### Markup Sub-menu

``` html
<nav class="navigation">
    <ul class="menu">
        <li class="menu-item menu-act">
            <!-- assign role="button" in <a> -->
            <a class="btn-menu" role="button">HTML에 대해</a>
            <!-- sub-list in list -->
            <ul class="sub-menu">
                <li class="sub-menu item">
                    <a>HTML5 소개</a>
                </li>
            </ul>
        </li>
        <li class="menu-item"></li>
        			.
        			.
        			.
	</ul>
</nav>
```

* menu-item 중, menu-act가 추가되어 있는 li 요소만 sub-menu를 보여주게 설정 (**jQuery** 필요)



---

### HTML Entities & Special Characters

* **HTML Entities** - are used to implement **reserved characters** or to express characters that cannot easily be entered with the keyboard

| Character | Entity Name |      Description      |
| :-------: | :---------: | :-------------------: |
|     &     |   `&amp;`   |       Ampersand       |
|     "     |  `&quot;`   |    Quotation Mark     |
|     '     |  `&apos;`   | Single quotation mark |
|     <     |   `&lt;`    |       less than       |
|     >     |   `&gt;`    |     greater than      |

([see more](https://www.w3schools.com/html/html_entities.asp))



---

### [CSS Animation](https://www.w3schools.com/css/css3_animations.asp)

* An animation lets an element gradually change **from one style to another**
* CSS 애니메이션을 사용하려면, **keyframes**을 우선적으로 명시해야함
* `keyframes` : 특정 시간대에 요소가 가져야 할 CSS 속성을 품고 있음
* 일부 오래된 브라우저에서 애니메이션을 사용하려면, prefix를 명시해줘야함 (ex. `-webkit-`)



### @Keyframes

``` css
/* The animation code */
@keyframes example {
   /* from this property (0%) */
  from {
      background-color: red;
      top: 0px;
      left: 0px;
  }
  /* to this property (100%) */
  to {
      background-color: yellow;
      top: 200px;
      left: 200px;
  }
}

/* The element to apply the animation to */
div {
  width: 100px;
  height: 100px;
  background-color: red;
  animation-name: example; /* name of @keyframes */
  animation-duration: 4s; /* for how long */
}
```

* `animation-name`: 애니메이션 속성을 품고 있는 @keyframes의 이름을 설정 (**필수**)

* `animation-duration`: 애니메이션을 완료하는 데 얼만큼의 시간이 걸릴지 설정 (**필수**, default = 0 sec)

* `animation-delay`: 애니메이션 시작을 입력하는 값만큼 지연시킴

  ``` css
  div {
    width: 100px;
    height: 100px;
    position: relative;
    background-color: red;
    animation-name: example;
    animation-duration: 4s;
    animation-delay: 2s; /* 애니메이션 시작을 2초 지연 */
    /* animation-delay: -2s; 애니메이션을 2초 진행된 부분에서 시작 */
  }
  ```

* `animation-iteration-count`: 애니메이션을 몇 회 반복할 것인지 설정 (`infinite` -> 무한)

* `animation-direction`: 애니메이션 재생 방향을 설정

  ``` css
  div {
    width: 100px;
    height: 100px;
    position: relative;
    background-color: red;
    animation-name: example;
    animation-duration: 4s;
    animation-direction: normal; /* 기본값, 정방향으로 진행 */
    animation-direction: reverse; /* 역방향으로 진행 */
    animation-direction: alternate; /* 정방향, 역방향 번갈아가며 진행 (count >= 2)*/
    animation-direction: alternate-reverse; /* 역방향, 정방향 번갈아가며 진행 (count >= 2)*/
  }
  ```

* `animation-timing-function` : 애니메이션 재생 속도 곡선 설정 ([see difference here](https://www.w3schools.com/css/tryit.asp?filename=trycss3_animation_speed))

  ``` css
  #div1 {animation-timing-function: linear;} /* 속도 유지 */
  #div2 {animation-timing-function: ease;} /* 느림 -> 빠름 -> 느림 */
  #div3 {animation-timing-function: ease-in;} /* 느림 -> 빠름 */
  #div4 {animation-timing-function: ease-out;} /* 빠름 -> 느림 */
  #div5 {animation-timing-function: ease-in-out;} /* 느림 -> 빠름 -> 느림 */
  ```

  * `animation-timing-function: cubic-bezier(n,n,n,n)`: define your own values ([see more](https://cubic-bezier.com/#.17,.67,.83,.67))

* `animation-fill-mode`: 애니메이션 시작 전후에 어떤 스타일 속성을 가지게 할 것인지 설정

  ``` css
  div {
      animation-name: example;
      animation-duration: 3s;
      /* 기본값, 애니메이션이 적용된 요소에 어떠한 스타일 변화도 주지 않음 */
      animation-fill-mode: none;
      
      /* 애니메이션이 끝나면 해당 요소에 @keyframes의 마지막 (to, 100%) 스타일이 적용됨 */
      animation-fill-mode: forwards;
      
      /* 애니메이션이 끝나면 해당 요소에 @keyframes의 첫번째 (from, 0%) 스타일이 적용됨 */
      animation-fill-mode: backwards;
      
      /* 애니메이션 시작 전/후에 각각 @keyframes의 첫번째, 마지막 스타일을 적용 */
      animation-fill-mode: both;
  }
  ```



### Shorthand Property

``` css
div {
  animation-name: example;
  animation-duration: 5s;
  animation-timing-function: linear;
  animation-delay: 2s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

/* can be written as below */

div {
  animation: example 5s linear 2s infinite alternate;
}
```



### 2D Transform function

* Allow you to `move`, `rotate`, `scale`, and `skew` elements

* `translate()`: move an element from its current position to given XY value

  ``` css
  /* 이전 @keyframes에선 top, left로 위치를 지정 */
  @keyframes example {
    from {
        background-color: red;
        /* top: 0px; */
        /* left: 0px; */
        transform: translate(0px, 0px); /* x, y coordinates */
    }
    to {
        background-color: yellow;
        /* top: 200px; */
        /* left: 200px; */
        transform: translate(200px, 200px); /* x, y coordinates */
    }
  }
  ```

([see more](https://www.w3schools.com/css/css3_2dtransforms.asp))



---

### Markup Visual - Animation

* 시나리오 작성 (텍스트)
  * 이동 효과
  * 글자 투명도 (opacity)
  * 텍스트 크기 (font-size)

```css
@keyframes textAni {
    0% {
        font-size: 12px;
        color: rgba(0,0,0,0);
        transform: translate(0, 0);
    }
    100% {
        font-size: 24px;
        color: rgba(0,0,0,1);
        transform: translate(400px, 75px);
    }
}

.visual-text {
    background-color: yellow;
    animation-name: textAni;
    animation-duration: 1s;
}
```

* 시나리오 작성 (배경 이미지)
  * 깜빡임 (교차) - delay
  * 반복 (infinite)
  * 진행 방향
  * transition-timing-function

``` css
@keyframes bgAni {
    0% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
}

.visual::before, .visual::after {
    content: "";
    width: 100%;
    height: 100%;
    position: absolute;
    animation: bgAni 2000ms 1000ms infinite alternate ease-in-out;
}
```



---

([prev - CSS float, Marking Up GNB](./css-float-gnb.md))

([next - Form Tag & WAI-ARIA](./form-waiAria.md))

([Back to List](../../README.md))

