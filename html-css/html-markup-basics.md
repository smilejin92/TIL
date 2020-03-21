# HTML5 Markup의 기초

HTML 문서는 요소(element)와 태그(tag), 그리고 컨텐츠로 구성되어 있다. 요소는 HTML의 의미를 가진 개념이라고 할 수 있다.

## 태그 (tag)

* 태그는 시작 태그와 종료 태그로 나눌 수 있으며 `<`와 `>`로 둘러싸여 있다.
* 기본 형식은 시작 태그의 경우 `<tag>`의 형태를 가지며, 종료 태그는 `</tag>` 형태를 가진다.
* 일부 태그의 경우 **종료 태그를 가지지 않는 경우**도 있다. 이를 **빈 요소**(empty element)라고 한다.

```html
<p>
  This is a paragraph with an <img src="./img.png" alt="image">.
</p>
```

## 속성 (attribute)

* 시작 태그는 필요에 따라 정해진 속성을 가질 수 있다. 사용할 수 있는 속성은 태그마다 다를 수 있다.
* 시작 태그 내에 여러 개의 속성을 선언할 수 있다. 이 경우 속성과 속성은 **공백**으로 구분하여 지정해야 한다.
* 속성에는 값을 가지지 않는 **논리 속성**도 있다. 하지만 XHTML1.0에서는 값을 생략할 수 없기 때문에 속성명을 값으로 지정해야한다.

```html
<!-- HTML4.01 -->
<input type="checkbox" checked>

<!-- XHTML1.0 -->
<input type="checkbox" checked="checked" />

<!-- HTML5에서는 두 방법 모두 허용된다. -->
```

## 요소 (element)

시작 태그와 종료 태그 모두를 포함하여 요소라고 한다.

## HTML5 서식

HTML5는 **HTML4.01이나 XHTML1.0 문법을 모두 허용**하기 때문에 기존에 사용하던 마크업 문법을 그대로 사용할 수 있다 (하위 호환성). 따라서 HTML5는 종료 태그를 생략할 수 있다 (일부 태그에 한해서). 하지만 XHTML1.0의 규칙처럼 시작과 종료 태그를 정확히 명시하여 정형식(well-formed) 구조로 마크업하는 것이 좋다.

```html
<!-- 두 방법 모두 허용된다. -->
<p><img src="./img.png" alt="image"></p>
<p><img src="./img.png" alt="image" /></p>
```

HTML5는 시작 및 종료 태그와 속성에 대문자 또는 소문자를 모두 사용할 수 있다. 그러나 기존 XHTML1.0 규칙처럼 소문자를 사용하는 것이 좋다.

```html
<!-- 대문자와 소문자를 모두 사용할 수 있다. -->
<P>
  <img SRC="./img.png" ALT="image">
</P>
```

HTML5는 종료 태그를 가지지 않는 빈 요소를 작성할 때 `/`를 생략하는 것이 허용된다.

```html
<!-- 두 방법 모두 허용된다. -->
<img src="./img.png" alt="image">
<img src="./img.png" alt="image" />
```

논리 속성의 경우 속성 값을 지정 또는 생략할 수 있다.

```html
<!-- 두 방법 모두 허용된다. -->
<input type="checkbox" checked>
<input type="checkbox" checked="checked" />
```

속성 값은 인용 부호를 생략하거나 홀따옴표, 겹따옴표 등으로 구분할 수도 있다.

```html
<!-- 모두 허용된다. -->
<img src=./img.png>
<img src='./img.png'>
<img src="./img.png" />
```

시작 태그에 동일한 **속성을 중복하여 선언할 수 없다.**

```html
<p style="color: red;" style="background: yellow;">
  This is a paragraph with two style attributes.
</p>
```

&lt;, &gt;, &amp;와 같은 특수 문자는 entity name 혹은 character entity code로 변환하여 마크업해야 한다.

```html
<p>웹 표준 & 웹 접근성</p> <!-- 잘못된 방법이다. -->
<p>웹 표준 &amp; 웹 접근성</p>
<p>웹 표준 &#38; 웹 접근성</p>
```

HTML4.01이나 XHTML1.0에서는 HTML 문서의 첫줄에 문서형 선언을 기술했었다. 이러한 문서형 선언은 해당 HTML 문서의 버전과 문서 타입을 명시했지만, HTML5에서는 문서의 버전 및 타입이 생략된 형식을 가진다. 그 이유는 기존 HTML 문서형 선언의 목적과 달리 **모든 웹 브라우저에서 표준 모드(Standards Mode)로 렌더링될 수 있도록 하는 역할만을 담당하기 때문이다.**

```html
<!-- HTML 4.01 Frameset -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">

<!-- XHTML 1.0 Frameset -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">

<!-- HTML5 -->
<!DOCTYPE html>
```

> **HTML DTD**
>
> Document Type Definition의 줄임말로 사용하고자 하는 HTML 문서의 종류와 버전을 표시한다.

HTML5에서는 문자 인코딩 지정 방법이 간소화 되었다.

```html
<!-- HTML5 -->
<meta charset="utf-8">

<!-- HTML4.01, XHTML1.0 -->
<meta http-equiv="content-type" content="text/html; charset=utf-8" />
```

기존의 HTML4 혹은 XHTML1.0에서는 컨텐츠 모델이라는 개념이 없고, 각 요소의  **display 스타일**에 의해 하위에 포함할 수 있는 요소들이 정해졌다. 예를 들면, 블록 요소는 블록 요소, 인라인 요소를 모두 포함할 수 있지만, 인라인 요소가 블록 요소를 포함하면 오류였다. **하지만 HTML5에서는 요소의 display 스타일에 의해 포함할 수 있는 하위 요소가 결정되는 것이 아니고, 컨텐츠 모델 상 허용하는지의 여부에 따라 문법 오류가 결정된다. 따라서 컨텐츠 모델의 관계에 따라 인라인 요소가 블록 요소를 포함할 수도 있다.**

## 참고 자료

* [HTML5 Markup](https://github.com/seulbinim/PDF/blob/master/HTML5.pdf)
* [HTML DOCTYPE Declaration](https://www.w3schools.com/tags/tag_doctype.asp)
* [Declaring character encodings in HTML](https://www.w3.org/International/questions/qa-html-encoding-declarations)

