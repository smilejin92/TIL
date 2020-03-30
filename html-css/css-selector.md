# CSS 선택자

## 전체 선택자(Universal Seletor)

전체 선택자는 **모든 요소**를 선택하는 방법으로 `*`를 선택자로 선언한다.

| 선택자 | 의미             |
| ------ | ---------------- |
| `*`    | 모든 요소를 선택 |

```css
* {
  margin: 0;
  padding: 0;
  border: none;
}
```

&nbsp;  

## 요소 선택자(Type Selector)

요소 선택자는 **HTML 요소**를 선택하는 방법으로, `h1`, `p`, `div` 등의 요소를 선택자로 지정할 수 있다.

| 선택자 | 의미            |
| ------ | --------------- |
| E      | "E" 요소를 선택 |

```css
h1 {
  font-size: 14px;
  font-weight: normal;
}
```

&nbsp;  

## 클래스 선택자(Class Selector)

클래스 선택자는 HTML 요소의 `class` 속성 값을 참조하여 선택하는 방법이다. 이때 `class` 속성 값은 하나의 HTML 요소에 여러 개를 지정할 수 있기 때문에 다중  class를 선택자로 지정할 수도 있다.

| 선택자     | 의미                                                         |
| ---------- | ------------------------------------------------------------ |
| E.box      | class 속성 값이 "box"인 "E" 요소를 선택                      |
| E.box.box2 | class 속성 값으로 "box"와 "box2"를 모두 가진 "E" 요소를 선택 |
| .box.box2  | class 속성 값으로 "box"와 "box2"를 모두 가진 모든 요소를 선택 |

```html
<div class="box box1">box1</div>
<div class="box box2">box2</div>

<style>
  /* div 요소 중 box 클래스를 가진 요소에 배경색을 지정 */
  div.box { 
    background-color: lightgreen; 
  }
  /* box 클래스와 box2 클래스를 모두 가진 요소에 폰트색을 지정 */
  div.box.box2 { 
    color: tomato; 
  }
</style>
```

&nbsp;  

## 아이디 선택자(ID Selector)

아이디 선택자는 HTML 요소의 `id` 속성 값을참조하여 선택하는 방법이다. 이때 `id` 속성 값은 하나의 HTML 문서에 한 번만 사용할 수 있기 때문에 아이디 선택자를 사용하면 유일한 요소를 선택할 수 있다.

| 선택자 | 의미                                  |
| ------ | ------------------------------------- |
| E#main | id 속성 값이 "main"인 "E" 요소를 선택 |

```html
<main class="main">
	Main section
</main>

<style>
  #main {
    margin: 0;
    padding: 0;
    border: none;
  }
</style>
```

&nbsp;  

## 속성 선택자(Attrivtue Selector)

속성 선택자는 HTML 요소의 속성을 참조하여 선택하는 방법을 의미한다. 이때 속성의 지정 여부나 속성 값의 일치 여부로 선택할 수 있다.

| 선택자         | 의미                                                         |
| -------------- | ------------------------------------------------------------ |
| E[attr]        | "attr" 속성을 가진 "E" 요소를 선택                           |
| E[attr="val"]  | "attr" 속성 값이 "val"인 "E" 요소를 선택                     |
| E[attr~="val"] | "attr" 속성 값 중에 공란으로 분리된 "val" 단어가 있는 "E" 요소를 선택 |
| E[attr=^"val"] | "attr" 속성 값이 "val"로 시작되는 "E" 요소를 선택            |
| E[attr$="val"] | "attr" 속성 값이 "val"로 끝나는 "E" 요소를 선택              |
| E[attr*="val"] | "attr" 속성 값이 "val"을 포함하는 "E" 요소를 선택            |
| E[attr\|="en"] | "attr" 속성 값이 "en"이거나 "en-"으로 시작하는 "E" 요소를 선택 |

```css
input[type="checkbox"] {
  display: inline-block;
  width: 15px;
  height: 15px;
}
```

&nbsp;  

## 가상 클래스 선택자(Pseudo-classes Selector)

가상 클래스 선택자는 요소의 상태나 상황에 따라 선택하는 방법으로, 링크의 경우 방문하기 전, 방문한 후, 링크 위에 마우스를 올렸거나 포커스 시 등의 상황을 선택하여 스타일을 구체적으로 지정할 수 있다. 또한 언어에 따른 구분이나 마크업 구조에 따라 특정 요소를 선택할 수도 있다.

| 선택자                | 의미                                                         |
| --------------------- | ------------------------------------------------------------ |
| **E:link**            | 아직 방문하지 않은 하이퍼링크를 가진 "E" 요소를 선택         |
| **E:visited**         | 이미 방문한 하이퍼링크를 가진"E" 요소를 선택                 |
| **E:active**          | 현재 사용자 액션을 받고 있는 "E" 요소를 선택 (ex. button이 눌릴 때) |
| **E:hover**           | 마우스 포인터가 올라간 "E" 요소를 선택                       |
| **E:focus**           | 키보드 포커스를 받은 "E" 요소를 선택                         |
| E:focus-within        | 키보드 포커스를 받은 "E" 요소 혹은 하위에 키보드 포커스를 받은 요소를 포함하는 "E" 요소를 선택 |
| E:target              | "E" 요소가 하이퍼링크 타깃이 되는 경우에 선택 (ex. a가 눌릴 때) |
| E:lang(ko)            | lang 속성 값이 "ko"인 "E" 요소를 선택                        |
| E:enabled             | 사용 가능 상태의 "E" 요소를 선택 (ex. disabled 속성이 없는 input) |
| E:disabled            | 사용 불가 상태의 "E" 요소를 선택                             |
| E:checked             | 체크된 "E" 요소를 선택함                                     |
| E:root                | 문서 최상위의 요소를 선택                                    |
| **E:nth-child(n)**    | 상위 요소의 n번째 자식 요소가 "E"이면 선택                   |
| E:nth-last-child(n)   | 상위 요소의 역순으로 n번째 자식 요소가 "E"이면 선택          |
| E:nth-of-type(n)      | 동일한 "E" 타입의 형제 요소                                  |
| E:nth-last-of-type(n) | 동일한 "E" 타입의 형제 요소 중 역순으로 n번째 "E" 요소를 선택 |
| **E:first-child**     | 첫 번째 자식 요소의 타입이 "E"이면 선택                      |
| **E:last-child**      | 마지막 자식 요소가 타입이 "E"이면 선택                       |
| E:first-of-type()     | 상위 요소에 대하여 첫 번째 자식 요소의 타입이 "E"이면 선택   |
| E:last-of-type()      | 상위 요소에 대하여 마지막 자식 요소의 타입이 "E"이면 선택    |
| E:only-child          | 상위 요소에 대하여 유일한 자식 요소가 타입이 "E"이면 선택함  |
| E:only-of-type        | 상위 요소에 대하여 자식 요소중 다른 "E" 요소가 없이 유일한 "E"일 경우 선택 |
| E:empty               | 텍스트 노드를 포함하여 아무런 자식 요소를 갖고 있지 않는 "E" 요소를 선택 |
| E:not(S)              | "S"로 지정된 선택자와 일치하지 않는 "E" 요소를 선택          |

더 많은 가상 클래스 요소는 [MDN Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)에서 확인 가능하다.

```css
a:visited {
  color: gray;
}

button:active {
  color: red;
}
```

&nbsp;  

## 가상 요소 선택자(Pseudo-element Selector)

가상 요소 선택자는 요소의 첫 글자나 첫 줄 또는 요소 앞이나 뒤 등 **가상의 영역**을 선택하고자 할 때 사용한다.

| 선택자         | 의미                                      |
| -------------- | ----------------------------------------- |
| E::first-line  | "E" 요소의 문자열 중 첫 번째 줄을 선택    |
| E:first-letter | "E" 요소의 문자열 중 첫 번째 문자를 선택  |
| E::before      | "E" 컨텐츠 앞으로 생성된 가상 요소를 선택 |
| E::after       | "E" 컨텐츠 뒤로 생성된 가상 요소를 선택   |
| E::selection   | 사용자가 선택한 "E" 요소의 범위를 선택    |

```css
button::after {
  content: '';
  display: block;
  width: 100%;
  height: 100%;
  background-image: url(./bg_image.png);
}
```

&nbsp;  

## 하위 선택자(Descendant Combinator)

하위 선택자 방식은 선행 선택자와 후행 선택자 사이를 **공백**으로 구분하여 선언하며, **선행 선택자의 하위 요소 중 후행 선택자에 해당하는 요소를 선택한다.**

| 선택자            | 의미                                                         |
| ----------------- | ------------------------------------------------------------ |
| [선택자] [선택자] | 후행 선택자가 반드시 선행 선택자 안에 포함되어 있을 경우 선택함 |

```html
<main class="main">
	<section class="section">...</section>
  <section class="section">...</section>
</main>

<style>
  /* .main 클래스를 가진 요소 하위에 .section 클래스를 가진 모든 요소를 선택 */
  .main .section {
    margin: 0;
    padding: 0;
    border: none;
  }
</style>
```

&nbsp;  

## 자식 선택자(Child Combinator)

자식 선택자 방식은 선행 선택자(부모) 요소 하위에 포함된 후행 선택자(자식)를 선택하는 방법이다. 이때 부모 요소와 자식 요소는 `>`로 구분하여 선언한다.

| 선택자                        | 의미                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| [부모 선택자] > [자식 선택자] | 자식 선택자가 부모 요소로 부모 선택자를 가지고 있는 경우 선택 |

```html
<ul class="lunch-menu">
  <li>메뉴 1</li>
  <li>메뉴 2</li>
  <li>메뉴 3</li>
</ul>

<style>
  /* .lunch-menu 클래스를 가진 요소의 직계 li 요소를 모두 선택 */
  .lunch-menu > li {
    color: red;
  }
</style>
```

> **자식 요소와 후손 요소**
>
> 자식 요소는 특정 요소의 **직하위**에 위치하는 요소를 말한다. 반면 후손 요소는 특정 요소의 직하위에 있거나 하위에 중첩돼있는 요소를 말한다. 즉, 모든 자식 요소는 후손 요소라 부를 수 있지만, 모든 후손 요소를 자식 요소라 말할 수는 없다.

&nbsp;  

## 형제 선택자(Sibling Combinators)

형제 선택자는 **기본 형제 선택자**와 **인접 형제 선택자**로 구분할 수 있다. 이때 기본 형제 선택자는 선행 선택자와 후행 선택자를 `+`로 구분하여 선언하고, 인접 형제 선택자는 `~`로 구분하여 선언한다.

| 선택자              | 의미                                                       |
| ------------------- | ---------------------------------------------------------- |
| [선택자] + [선택자] | 선행 선택자 뒤에 후행 선택자를 선택                        |
| [선택자] ~ [선택자] | 선행 선택자 뒤에 인접하여 등장하는 모든 후행 선택자를 선택 |

```html
<div class="first">first</div>
<div class="second">second</div>
<div class="third">third</div>

<style>
  /* first 클래스를 가진 요소의 바로 다음 형제 요소가 second 클래스를 가지고 있다면 선택 */
  .first + .second {
    color: red;
  }
  /* first 클래스를 가진 요소 이후에 나타나는 모든 형제 div 요소를 선택 */
  .first ~ div {
    color: blue;
  }
</style>
```

&nbsp;  

## 선택자 그룹화

위에서 살펴본 모든 선택자는 쉼표(`,`)를 사용하여 그룹화한 뒤 동일한 스타일을 한번에 선언할 수 있다.

| 선택자             | 의미                                                |
| ------------------ | --------------------------------------------------- |
| [선택자], [선택자] | 쉼표(`,`)로 구분된 모든 선택자에 동일한 선언이 적용 |

```html
<h1>제목</h1>
<p>본문입니다.</p>
<p class="note">노트입니다.</p>
<p title="description">설명입니다.</p>
<main id="main">
	...
</main>

<style>
  h1,
  h1 + p,
  .note,
  #main,
  p[title="description"] {
    font-size: 1.2rem;
  }
</style>
```

&nbsp;  

## 선택자 우선순위

| 선택자 예제 | id * 100 | class * 10 | tag * 1 | 구체성 | 우선순위 |
| ----------- | -------- | ---------- | ------- | ------ | -------- |
| li          | 0        | 0          | 1       | 1      | 5        |
| ul li       | 0        | 0          | 2       | 2      | 4        |
| div.note    | 0        | 1          | 1       | 11     | 3        |
| #list li    | 1        | 0          | 1       | 101    | 2        |
| ul#list li  | 1        |            | 2       | 102    | 1        |

&nbsp;  

## 참고자료

* [CSS3 Design](https://github.com/seulbinim/PDF/blob/master/CSS3.pdf)
* [MDN How is specificity calculated?](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
* [MDN Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

