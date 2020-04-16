# ARIA 사용 규칙

접근성 정보를 추가하여 장애를 가진 사용자가 웹 컨텐츠와 웹 어플리케이션에 더 쉽게 접근할 수 있도록 할 수 있다. 본 게시글은 HTML5에서의 WAI-ARIA 사용 규칙에 대해 설명한다.

&nbsp;  

## 1. ARIA 사용의 첫 번째 규칙

만약 사용 목적에 맞는 네이티브 HTML 요소 혹은 속성이 **이미 존재한다면**, 다른 요소에 ARIA 속성을 추가하는 것 대신 **네이티브 요소를 그대로 사용한다.**

**이 규칙이 적용되지 않는 경우는?**

* 사용하고자 하는 기능이 [HTML](https://html.spec.whatwg.org/multipage/)에 존재하지만, 구현되지 않은 경우
* 사용하고자 하는 기능이 HTML에 존재하고, 구현되었지만 [접근성 지원](https://www.html5accessibility.com/)이 안되는 경우
* 특정 네이티브 요소를 필요에 맞게 스타일링 할 수 없는 경우
* 구현하고자 하는 기능이 [현재 HTML에서 지원하지 않는 경우](https://developer.paciellogroup.com/blog/2014/10/aria-in-html-there-goes-the-neighborhood/#html5na)

&nbsp;  

## 2. ARIA 사용의 두 번째 규칙

정말 필요한 경우가 아니라면, **요소의 태생적 의미를 변경하지 않는다.**

예를 들어, 탭 역할을 가진 헤딩을 만들고자 할 때 아래와 같은 방법을 사용하지 않는다.

```html
<!-- 잘못된 예 -->
<h2 role="tab">heading tab</h2>
```

아래와 같이 수정하여 사용한다.

```html
<!-- 올바른 예 -->
<div role="tab">
  <h2>heading tab</h2>
</div>
```

> **NOTE**
>
> 만약 비대화형(non-interactive) 요소가 대화형(interactive) 요소로 사용되어야 하는 경우, 개발자는 ARIA 속성을 활용하여 역할과 상태를 추가해야하고, 스크립트로 적절한 상호작용(ex. 키보드 포커싱)을 구현해야한다. 예를 들어 버튼의 경우, HTML 네이티브 버튼(`<button>`)을 그대로 사용하는 것이 더욱 좋은 방법이다.

> **NOTE**
>
> ARIA 역할과 비슷한 의미를 가진 네이티브 HTML 요소를 fallback으로 사용해도 괜찮다. 예를 들어, HTML의 [목록 요소](https://www.w3.org/TR/html51/grouping-content.html#elementdef-ul)를 ARIA와 자바스크립트로 만들어진 [트리 위젯](http://hanshillen.github.io/jqtest/#goto_tree)의 뼈대로 사용할 수 있다.

```html
<ul role="tree">
  <li role="presentation">...</li>
  <li role="presentation">...</li>
  <li role="presentation">...</li>
</ul>
```

&nbsp;  

## 3. ARIA 사용의 세 번째 규칙

모든 대화형 ARIA 컨트롤은 **키보드로 사용할 수 있어야 한다.**

사용자가 클릭, 탭, 드래그 &amp; 드랍, 슬라이드, 스크롤할 수 있는 위젯을 만들 때 키보드로도 동일한 액션을 수행할 수 있도록 해야한다.

즉, 모든 대화형 위젯은 표준 키 입력 또는 키 스트로크 조합에 응답할 수 있도록 스크립팅되어야 한다.

예를 들어, `role="button"` ARIA 역할을 가지고 있는 요소는 반드시 포커스를 받을 수 있어야하며, 사용자는 <kbd>Enter</kbd> 키(Windows) 혹은 <kbd>return</kbd> 키(macOS)와 <kbd>space</kbd> 키를 모두 사용하여 요소와 관련된 작업을 활성화할 수 있어야 한다.

자세한 내용은 [WAI-ARIA-PRACTICES-1.2](https://www.w3.org/TR/wai-aria-practices/)의 [Design Patterns and Widgets](https://www.w3.org/TR/wai-aria-practices/#aria_ex)와 [Developing a Keyboard Interface](https://www.w3.org/TR/wai-aria-practices/#keyboard) 섹션을 참조.

&nbsp;  

## 4. ARIA 사용의 네 번째 규칙

포커스를 받는(focusable) 요소에 `role="presentation"` 혹은 `aria-hidden="true"` 속성을 사용하지 않는다.

포커스를 받는 요소에 해당 ARIA 속성을 사용하게 된다면, 사용자는 아무 것도 아닌 요소에 초점을 맞추게 될 수 있기 때문이다.

```html
<!-- 잘못된 예 -->
<button role="presentation">press me</button>
<button aria-hidden="true">press me</button>
```

> **NOTE**
>
> 대화형 요소를 포함하는 상위 요소에 `aria-hidden` 속성을 적용하면, 하위의 대화형 요소도 숨김 처리되기 때문에 주의해야한다. 따라서 아래와 같은 코드 역시 작성하면 안된다.

```html
<div aria-hidden="true">
  <button>press me</button> <!-- 숨김 처리 -->
</div>
```

> **NOTE**
>
> 대화형 요소를 시각적으로 확인할 수 없거나(초점을 받을 수 없는 상태) 상호작용할 수 없는 상태라면, `aria-hidden` 속성을 사용할 수 있다.

```html
<style>
  button {
    opacity: 0;
  }
</style>

<button tabindex="-1" aria-hidden="true">press me</button>
```

> **NOTE**
>
> 대화형 요소 혹은 대화형 요소를 포함하는 상위 요소가 `display: none` 혹은 `visibility: hidden` 처리되어 있다면, 포커스를 받을 수 없기 때문에 `aria-hidden="true"` 속성과  `tabindex="-1"` 속성을 명시적으로 추가할 필요가 없다. 또한 이러한 요소는 [accessibility tree](https://www.w3.org/TR/accname-1.1/#dfn-accessibility-tree)에서도 사라지게 된다.

&nbsp;  

## 5. ARIA 사용의 다섯 번째 규칙

모든 대화형 요소는 반드시 접근 가능한 이름([accessible name](https://www.w3.org/TR/accname-1.1/#dfn-accessible-name))을 가져야한다.

대화형 요소는 Accessibility API의 접근 가능한 이름(혹은 동등한 이름) 속성에 값이 있을 때만 접근 가능한 이름을 갖는다.

예를 들어, 아래의 input 요소는 시각적으로 'user name'이라는 이름을 갖지만, 접근 가능한 이름은 갖지 않는다.

```html
user name <input type="text" />

<!-- 혹은 -->

<span>user name</span> <input type="text" />
```

위 예제는 [MSAA](https://en.wikipedia.org/wiki/Microsoft_Active_Accessibility) accName 속성이 비어있다.

<img src="https://user-images.githubusercontent.com/32444914/79046770-c3f28b80-7c4d-11ea-9d2b-e823b9b2840e.png" style="zoom:100%;" />

반면 아래의 input 요소는 시각적으로 'user name'이라는 이름을 가짐과 동시에 접근 가능한 이름을 갖는다. input 요소는 레이블이 붙을 수 있는(labellable) 요소이며, label 요소는 label 텍스트를 input 요소와 연결하기 위해 올바르게 사용된다.

```html
<input type="text" aria-label="User Name" />

<!-- 혹은 -->

<span id="p1">user name</span>
<input type="text" aria-labelledby="p1" />
```

위 예제는 [MSAA](https://en.wikipedia.org/wiki/Microsoft_Active_Accessibility) accName 속성 값을 가지고 있다.

![](https://user-images.githubusercontent.com/32444914/79046784-dbca0f80-7c4d-11ea-9716-10f8c44e7074.png)

> **NOTE**
>
> 위 예제는 ARIA 위젯에 관한 예제이다. 일반 HTML input 요소에 대해서는 ARIA 사용의 첫 번째 규칙에 따라 label 요소의 for 속성을 사용하여 input 요소를 연결한다.

&nbsp;  

### HTML label 요쇼와 labelable 요소

label 요소는, [label로 연결할 수 있는 네이티브 HTML 요소](https://www.w3.org/TR/html51/sec-forms.html#labelable-element)를 참조하지 않는 한, 사용자 정의 컨트롤에 accessible name을 제공하기 위한 수단으로 사용될 수 없다.

```html
<label>
	user name <input type="text" role="combobox" />
</label>
```

위 예제는 [MSAA](https://en.wikipedia.org/wiki/Microsoft_Active_Accessibility) accName 속성 값을 가지고 있다.

![](https://user-images.githubusercontent.com/32444914/79046806-f308fd00-7c4d-11ea-9258-fa680fe135e5.png)

반면 `div` 요소는 어떠한 ARIA 역할을 가지고 있더라도 label로 연결될 수 없는 요소이다.

```html
<label>
	user name <div role="combobox"></div>
</label>
```

위 예제는 [MSAA](https://en.wikipedia.org/wiki/Microsoft_Active_Accessibility) accName 속성이 비어있다.

![](https://user-images.githubusercontent.com/32444914/79046821-04520980-7c4e-11ea-99e8-f5096dd07f62.png)

&nbsp;  

## 참고 자료

* [Using ARIA](https://www.w3.org/TR/using-aria/)

