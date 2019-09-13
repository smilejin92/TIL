# 20190909

### ROLE 부여

- Sementic 하지 않은 `<div>` 혹은 원래 목적의 `<a>` 같은 태그에 `role` 속성을 추가해 의미를 부여

------

### aria-label

### border-radius

### 웹 페이지 레이아웃 (ch. 5)

* google "embed mdn" [(link)](https://www.w3.org/TR/2010/WD-html5-20100624/the-iframe-element.html#the-embed-element)
* [html5 mulder21c](https://mulder21c.github.io/2016/10/14/prepare-to-translate-w3c-html5-specification/)

---

* https://developer.mozilla.org/en-US/docs/Web/HTML/Element/embed
* https://www.w3.org/TR/2010/WD-html5-20100624/the-iframe-element.html#the-embed-element
* https://mulder21c.github.io/2016/10/14/prepare-to-translate-w3c-html5-specification/
* https://www.w3schools.com/html/html_entities.asp
* https://developer.mozilla.org/en-US/docs/Web/CSS/transform
* https://www.slideshare.net/wsconf

---







![](C:\Users\Jinhyun Kim\Documents\dev\TIL\HTML-CSS\notes\images\menu-space.PNG)

메뉴 간격 생성

`<li>`에 padding vs. `<a>`에 padding

---

### menu-act (dynamic)

* using javascript (jQuery)
* CSS 선택자 구체성
  * tag -> 1
  * class -> 10
  * id -> 100
  * style
  * !important keyword (for debugging, 선택자 순위 보존)

* using ::after

---

```html
<ul class="menu">
    <li class="menu-item menu-act">
    	<a class="btn-menu" role="button">HTML</a>
        <ul class="sub-menu">
            <li class="sub-menu item">
            	<a>HTML5 소개</a>
            </li>
        </ul>
    </li>
</ul>
```

* 형제 선택자

* white-space: nowrap

---

### Marking-up Visual

* 특수문자 (&, $...) escape sequence
* [HTML Entities](https://www.w3schools.com/html/html_entities.asp)
* Animation
  * 시나리오
    * 이동 효과
    * 글자 투명도 (opacity)
    * 텍스트 크기 (font-size)

```css
.visual-text {
    background-color: yellow;
    animation-name: textAni;
    animation-duration: 1s;
    /* animation-name, animation-duration REQUIRED */
}
```

* transform

  * [transform function](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

  ``` css
  @keyframes textAni {
      0%{
          font-size: 12px;
          color: rgba(0,0,0,0);
          /* padding: 0; */
          /* margin: 0; */
          /* top: 0;
          left:0; */
  
          /* translate(x, y) */
          transform: translate(0, 0); /* top left */
      }
      100%{
          font-size: 24px;
          color: rgba(0,0,0,1);
          /* padding: 75px 0 0 400px; */
          /* margin: 75px 0 0 400px; */
          /* top: 75px;
          left: 400px; */
          transform: translate(400px, 75px);
      }
      /* 
      from{}
      to{}
      */
  }
  ```

---

* slideshare/wsconf
* z-index
* 시나리오 (continued)
  * bgAni
    * 깜빡임 (교차) - delay
    * 반복
    * animation-direction
    * infinite
    * transition-timing-function

---

https://cubic-bezier.com/#.46,-0.52,.83,.67

