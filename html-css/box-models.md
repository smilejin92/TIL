# CSS 박스 모델

CSS의 모든 것은 상자로 감싸져 있다. CSS 레이아웃 설계의 핵심은 박스 모델을 이해하는 것이다.

&nbsp;  

## 블록 & 인라인 상자

CSS에서는 크게 **블록 상자**와 **인라인 상자** 두 가지 타입의 상자가 있다. 각 상자의 타입은 페이지 흐름의 측면에서 상자가 어떻게 동작하는지를 의미하며, 다른 상자와의 관계에서 어떻게 동작해야하는지를 나타낸다.

**블록 상자**

* 새로운 줄에서 시작된다.
* 자신을 포함하는 컨테이너의 너비를 100% 차지한다.
* `width`와 `height` 속성이 적용된다.
* padding, margin, border는 주변 요소를 밀어낸다.

**인라인 상자**

* 줄바뀜이 생기지 않는다.
* `width`와 `height` 속성이 적용되지 않는다.
* padding, margin, border이 적용되지만, 다른 인라인 상자를 밀어내지 않는다.

요소에 적용된 상자의 타입은 `display` 속성 값에 의해 결정되며, `display` 속성의 outer 값과 관련이 있다.

&nbsp;  

## Inner & Outer 디스플레이 타입

CSS에서 박스는 **블록인지 인라인인지** 결정하는 **outer** 디스플레이 타입을 가지고 있다. 또한 박스는 **자신의 내부 요소들이 어떻게 배치되어야하는지** 결정하는 **inner** 디스플레이 타입을 가지고 있다. 기본적으로 박스 내부의 요소는 다른 블록 요소 혹은 인라인 요소와 같이 [**normal flow**](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow)로 배치되어 있다.

`display` 속성에 `flex` 같은 값을 사용하여 inner 디스플레이 타입을 변경할 수 있다. 요소에 `display: flex` 속성을 지정하면, outer 디스플레이 타입은 블록이지만, inner 디스플레이 타입은 `flex`로 변경된다. 이러한 요소의 직계 자식 요소는 flex items으로 취급되며 [Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)의 규칙에 따라 배치된다.

블록과 인라인 레이아웃은 웹 상의 요소들이 동작하는 기본적인 방법이다. 다른 instruction이 없다면 박스는 블록 혹은 인라인 박스로 배치되기 때문에, 이러한 방법을 normal flow라 부른다.

&nbsp;  

## 디스플레이 타입 예제

### 예제 1

아래 세 개의 HTML 요소는 모두 outer 디스플레이 타입으로 `block`을 가지고 있다. 첫 번째 요소는 일반 텍스트를 포함하는 `<p>` 요소이다. 브라우저는 이 요소를 블록 상자로 렌더하기 때문에, 첫 번째  `<p>` 요소는 새로운 줄에서 시작되며, 가용할 수 있는 너비를 모두 차지한다.

두 번째 요소는 `<ul>` 요소이며 `display: flex` 속성으로 배치되어있다. 이 속성은 목록 내부 요소를 위한 flex 레이아웃을 형성한다. 하지만 `<ul>` 요소 자체는 블록 박스이며 첫 번째 요소인 `<p>` 처럼 새로운 줄에서 시작하며, 가용할 수 있는 너비를 모두 차지한다.

세 번째 요소는 두 개의 `<span>` 요소를 포함하는 블록 레벨 `<p>` 요소이다. 두 `<span>` 요소는 일반적으로 `inline` 상자이지만, 하나는 block 클래스를 가지고 있으며 `display: block` 속성으로 지정되었다.

<img src="https://user-images.githubusercontent.com/32444914/79850013-432a5100-83fe-11ea-8bdc-299a9c4fc875.png" style="zoom:50%;" />

```html
<style>
	p,
  ul {
    border: 2px solid rebeccapurple;
    padding: .5em;
  }
  .block,
  li {
    border: 2px solid blue;
    padding: .5em;
  }
  ul {
    display: flex;
    list-style: none;
  }
  .block {
    display: block;
  }
</style>

<body>
  <p>I am a paragraph. A short one.</p>
  <ul>
    <li>Item One</li>
    <li>Item Two</li>
    <li>Item Three</li>
  </ul>
  <p>
    I am another paragraph. Some of the <span class="block">word</span> have been wrapped in a <span>span element</span>.
  </p>
</body>
```

&nbsp;  

### 예제 2

아래 예제를 통해 `inline` 요소가 어떻게 동작하는지 살펴 볼 수 있다. 첫 번째 `<p>` 요소 내부의 `<span>` 요소는 기본적으로 인라인 속성을 가지기 때문에 줄바뀜이 발생하지 않는다.

두 번째 `<ul>` 요소는 `display: inline-flex` 속성을 가지고 있으며, flex items를 감싸는 인라인 상자를 생성한다.

마지막 두 개의 `<p>` 요소는 `display: inline`으로 지정되었다. 인라인 flex 속성을 가진 `<ul>`과 두 개의 `<p>` 요소가 개행되지 않고, 같은 줄에서 진행되는 것을 확인할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/79850211-884e8300-83fe-11ea-9687-1b4facb8ce62.png" style="zoom:50%;" />

```html
<style>
	p,
  ul {
  	border: 2px solid rebeccapurple;
  }
  span,
  li {
    border: 2px solid blue;
  }
  ul {
    display: inline-flex;
    list-style: none;
    padding: 0;
  }
  .inline {
    display: inline;
  }
</style>

<body>
  <p>
    I am a paragraph. Some of the <span>words</span> have been wrapped in a <span>span element</span>.
  </p>
  <ul>
    <li>Item One</li>
    <li>Item Two</li>
    <li>Item Three</li>
  </ul>
  <p class="inline">I am a paragraph. A short one.</p>
  <p class="inline">I am another paragraph. Also a short one.</p>
</body>
```

&nbsp;  

## 그래서 CSS 박스 모델은 무엇인가?

블록 박스는 CSS 박스 모델의 모든 특성을 사용하며, 인라인 박스는 CSS 박스 모델의 일부 특성만 사용한다. 박스 모델은 margin, border, padding, 컨텐츠가 박스를 형성할 때 어떻게 동작하는지를 정의한다. 박스 모델의 종류와 특징은 아래와 같다.

* **Content box**: `width`, `height` 속성으로 크기를 조절할 수 있는 컨텐츠가 표시되는 영역
* **Padding box**: 패딩은 컨텐츠 주변의 공백 영역으로 위치한다. 패딩 박스의 사이즈는 `padding` 속성으로 조절될 수 있다.
* **Border box**: 보더 박스는 컨텐츠와 패딩을 감싼다. 보더 박스의 사이즈와 스타일은 `border` 속성으로 조절될 수 있다.
* **Margin box**: 마진은 요소 사이의 공백으로서 컨텐츠, 패딩, 보더를 감싸는 가장 바깥 쪽 레이어이다. 마진은 `margin` 속성으로 조절될 수 있다.

![](https://user-images.githubusercontent.com/32444914/79850221-8b497380-83fe-11ea-96df-229a5068fd94.png)

(이미지 출처: [MDN Web Docs - The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model))

&nbsp;  

### 스탠다드 CSS 박스 모델

스탠다드 박스 모델에서 박스의 `width`와 `height` 속성을 지정하면, **컨텐트 박스(content box)**의 너비와 높이가 정의된다. **패딩과 보더는** 컨텐트 박스의 영역이 계산된 후 **추가로 더해져 박스의 전체 사이즈를 정의한다.** 아래 예제를 통해 스탠다드 CSS 박스 모델의 사이즈 계산 방법을 알아보자.

```css
.box {
  width: 350px;
  height: 150px;
  padding: 25px;
  border: 5px solid black;
  margin: 10px;
}
```

요소에 위와 같은 CSS 속성 값을 지정할 경우, 스탠다드 박스 모델의 영역은 아래와 같이 계산된다.

* 컨텐트 박스: 350px * 150px
* 패딩 박스: (25px * 2 + 컨텐트 박스 너비) * (25px * 2 + 컨텐트 박스 높이)
* 보더 박스: (5px * 2 + 패딩 박스 너비) * (5px * 2 + 패딩 박스 높이)
* 마진 박스: (10px * 2 + 보더 박스 너비) * (10px * 2 + 보더 박스 높이)
* **상자의 전체 영역 = 보더 박스 = 410px * 210px**
* 요소의 전체 영역 = 마진 박스 = 430px * 230px

![](https://user-images.githubusercontent.com/32444914/79850222-8be20a00-83fe-11ea-9331-58764e0aacff.png)

(이미지 출처: [MDN Web Docs - The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model))

> **Note**: 마진은 박스의 실제 사이즈에 포함되지 않는다. 마진은 박스의 전체 영역에 영향을 주지만, 박스의 **바깥쪽 여백**에 해당된다. 박스의 실질적 사이즈는 보더까지이며, 바깥쪽 여백(마진)까지 늘어나지 않는다.

&nbsp;  

### 대체 CSS 박스 모델

 박스의 실질적인 사이즈를 계산하기 위해 border와 padding을 더해야하는 것이 불편하게 느껴질 수 있다. 이러한 이유로, CSS에서는 스탠다드 박스 모델 이후 대체(alternative) 박스 모델을 출시했다. **대체 박스 모델을 사용하는 경우**, 너비는 페이지에 표시되는 상자의 너비이기 때문에 **컨텐츠 영역의 너비는 패딩 및 보더의 너비를 제외한 너비이다**. 위의 예제에서 사용된 동일한 CSS 속성은 아래와 같은 결과를 생성한다 (width = 350px, height = 150px).

![](https://user-images.githubusercontent.com/32444914/79850228-8c7aa080-83fe-11ea-8cbc-fb57b8339d4d.png)

(이미지 출처: [MDN Web Docs - The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model))

기본적으로 브라우저는 스탠다드 박스 모델을 사용한다. 요소에 `box-sizing: border-box` 속성을 지정하면 대체 박스 모델을 사용할 수 있다. 해당 속성을 지정하는 것은 브라우저에게 지정한 크기의 영역을 보더 박스로서 인식하게끔 한다.

```css
.box {
  box-sizing: border-box;
}
```

만약 모든 요소의 영역을 대체 박스 모델로서 사용하고 싶다면, `<html>` 요소의 `box-sizing` 속성에 `border-box` 값을 지정하여 모든 요소로 하여금 `box-sizing` 속성을 상속 받을 수 있게 설정할 수 있다.

```css
html {
  box-sizing: border-box;
}

*, *::before, *::after {
  box-sizing: inherit;
}
```

&nbsp;  

### 브라우저 개발자 도구를 이용한 박스 모델 분석

브라우저 개발자 도구를 사용하여 박스 모델를 더욱 쉽게 이해할 수 있다. 예를 들어, Firefox의 개발자 도구를 사용하여 요소 검사를 실행할 경우, 아래 그림과 같이 마진, 패딩, 보더가 더해진 요소의 크기를 한 눈에 파악할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/79850233-8dabcd80-83fe-11ea-984a-c785a39afb0d.png" style="zoom:38%;" />

(이미지 출처: [MDN Web Docs - The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model))

&nbsp;  

## 참고 자료

* [MDN Web Docs - The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
* [Block and inline layout in normal flow](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/Block_and_Inline_Layout_in_Normal_Flow)

