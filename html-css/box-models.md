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

* 개행되지 않는다.
* `width`와 `height` 속성이 적용되지 않는다.
* padding, margin, border이 적용되지만, 다른 인라인 상자를 밀어내지 않는다.

요소에 적용된 상자의 타입은 `display` 속성 값에 의해 결정되며, `display` 속성의 outer 값과 관련이 있다.

&nbsp;  

## Inner & Outer 디스플레이 타입

CSS에서 박스는 **블록인지 인라인인지** 결정하는 **outer** 디스플레이 타입을 가지고 있다. 또한 박스는 **자신의 내부 요소들이 어떻게 배치되어야하는지** 결정하는 **inner** 디스플레이 타입을 가지고 있다. 기본적으로 박스 내부의 요소는 다른 블록 요소 혹은 인라인 요소와 같이 [**normal flow**](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow)로 배치되어 있다.

`display` 속성에 `flex`와 같은 값을 사용하여 inner 디스플레이 타입을 변경할 수 있다. 요소에 `display: flex` 속성을 지정하면, outer 디스플레이 타입은 블록이지만, inner 디스플레이 타입은 `flex`로 변경된다. 이러한 요소의 직계 자식 요소는 flex items으로 취급되며 [Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)의 규칙에 따라 배치된다.

블록과 인라인 레이아웃은 웹 상의 요소들이 동작하는 기본적인 방법이다. 다른 instruction이 없다면 박스는 블록 혹은 인라인 박스로 배치되기 때문에, 이러한 방법을 normal flow라 부른다.

&nbsp;  

## 디스플레이 타입 예제

### 예제 1

아래 세 개의 HTML 요소는 모두 outer 디스플레이 타입으로 `block`을 가지고 있다. 첫 번째 요소는 일반 텍스트를 포함하는 `<p>` 요소이다. 브라우저는 이 요소를 블록 상자로 렌더하기 때문에, 첫 번째  `<p>` 요소는 새로운 줄에서 시작되며, 가용할 수 있는 너비를 모두 차지한다.

두 번째 요소는 `<ul>` 요소이며 `display: flex` 속성으로 배치되어있다. 이 속성은 목록 내부 요소를 위한 flex 레이아웃을 형성한다. 하지만 `<ul>` 요소 자체는 블록 박스이며 첫 번째 요소인 `<p>` 처럼 새로운 줄에서 시작하며, 가용할 수 있는 너비를 모두 차지한다.

세 번째 요소는 두 개의 `<span>` 요소를 포함하는 블록 레벨 `<p>` 요소이다. 두 `<span>` 요소는 일반적으로 `inline` 상자이지만, 하나는 block 클래스를 가지고 있으며 `display: block` 속성으로 지정되었다.

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

<img src="/Users/smilejin92/Desktop/Screen Shot 2020-04-18 at 7.39.35 PM.png" style="zoom:50%;" />

&nbsp;  

### 예제 2

아래 예제를 통해 `inline` 요소가 어떻게 동작하는지 살펴 볼 수 있다.