# CSS 기초

## CSS 기본문법

하나의 규칙은 크게 선택자(selector)와 선언부(declaration block)로 이루어지며, 선언부는 속성(property)과 속성 값(value)으로 구성되어 있다. 이때 선언부는 세미콜론(`;`)으로 속성과 속성 값을 구분하여 여러 개의 선언(declaration)을 지정할 수 있다.

```css
selector { /* 선택자 */
  /* 선언부 */
  property: value; /* 속성: 속성 값 */
  property: value; /* 속성: 속성 값 */
}
```

&nbsp;  

## CSS3 웹 브라우저별 접두사(vendor prefix)

CSS3는 표준안이 아직 확정되지 않은 상태이기 때문에 최신 웹 브라우저들은 CSS3 속성을 실험적으로 제공하고 있다. 이를 위해 속성이나 속성 값 앞에 웹 브라우저별로 접두사(vendor prefix)를 제공하고 있으며, 하나의 속성을 선언하기 위해서는 여러 번의 동일한 선언을 지정해야할 수도 있다.

| 웹 브라우저                  | 접두사(prefix) |
| ---------------------------- | -------------- |
| 파이어폭스(Firefox)          | -moz-          |
| 크롬, 사파리(Chrome, Safari) | -webkit-       |
| 오페라(Opera)                | -o-            |
| 인터넷 익스플로러(IE)        | -ms-           |

&nbsp;  

## 주석

CSS 파일의 내용이 많아질 경우 이를 관리하기 위해서 주석을 활용하면 좋다. 주석은 소스상에서만 표시될 뿐, 실질적으로 아무 영향을 미치지 않는 코드이다. css의 주석은 `/*`로 시작하여 `*/`로 끝난다.

```css
/* 주석입니다. */
h1 {
  border: 1px solid red;
}
```

&nbsp;  

## 단위

* **문자열 타입**: `inherit`, `bold`와 같이 CSS에서 미리 정의된 키워드나 제작자가 정의한 키워드 등 텍스트로 입력하는 속성 값
* **숫자 타입**: 개수 비율들을 나타낼 수 있는 정수, 실수 값, 퍼센트 값
* **길이 단위 타입**: 길이 단위 타입은 상대 길이 단위 값과 절대 길이 단위 값이 있으며, 상대 길이 단위 값은 특정 길이에 비율로 정해지는 값

**상대 단위**

| 단위 | 의미                                                         |
| ---- | ------------------------------------------------------------ |
| em   | 폰트의 기본 크기 값에 비례한 단위 (상속 받은 크기 값의 배수) |
| ex   | 폰트의 기본 X 높이에 비례한 단위                             |
| ch   | "0"의 기본 폭에 비례한 단위                                  |
| rem  | 최상위 요소(root)의 폰트 크기에 비례한 단위                  |
| vw   | 뷰포트 너비에 비례한 단위                                    |
| vh   | 뷰포트 높이에 비례한 단위                                    |
| vmin | 뷰표트 최소 너비, 높이에 비례한 단위                         |

&nbsp;  

**절대 단위**

| 단위 | 의미                             |
| ---- | -------------------------------- |
| cm   | 센티미터 단위                    |
| mm   | 밀리미터 단위                    |
| in   | 인치(inch) 단위, 1in = 2.54cm    |
| px   | 픽셀(pixels) 단위, 1px = 1/96in  |
| pt   | 포인트(point) 단위, 1pt = 1/72in |
| pc   | 피카(picas) 단위, 1pc = 12pt     |

&nbsp;

**기타 단위**

| 단위 | 용도   |
| ---- | ------ |
| deg  | 각도   |
| grad | 각도   |
| rad  | 각도   |
| turn | 각도   |
| s    | 시간   |
| ms   | 시간   |
| Hz   | 빈도   |
| kHz  | 빈도   |
| dpi  | 해상도 |
| dpcm | 해상도 |
| dppx | 해상도 |

위 단위들은 기존 CSS2에서 음성 브라우저 등의 특수 경우를 상정하여 정의되었던 것이지만, CSS3에서는 표현 속성이 다양해짐에 따라 각도나 시간은 일반적으로 사용되는 값의 형식이 된다.

&nbsp;  

## 색상

CSS3에서의 색상 단위는 좀 더 확대되었다. 특히 투명 값(alpha)이나 색상, 채도, 명도 등을 지정할 수 있는 HSL 방식과 `currentcolor` 키워드 등이 추가되었다.

**RGBA 형식**

```css
h1 {
  /* rgba(red, green, blue, 투명도) */
  color: rgba(255, 127, 45, 0.5); 
}
```

**HSLA 형식**

```css
h1 {
  /* hsla(새상, 채도, 명도, 투명도) */
  hsla(0, 0%, 100%, 0.5);
}
```

&nbsp;  

## CSS 적용하기

CSS를 적용하는 방법은 크게 세 가지이다.

### 1. External

CSS 파일을 외부에 생성하여 HTML 문서에 연결하는 방식으로 `<link>` 요소를 사용하는 방법과 `@import` 명령을 사용하는 두 가지 방식이 있다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <title>Document</title>
    <!-- 방법 1. -->
    <link rel="stylesheet" stype="text/css" href="css/style.css" />
    <style>
      /* 방법 2. */
      @import url(css/style.css);
    </style>
  </head>
</html>
```

&nbsp;  

### 2. Embedded

HTML 파일 내에 CSS 코드를 직접 포함하여 스타일이 적용되도록 하는 방법이다. CSS 코드는 `<style>` 요소내에 선언해야한다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <style>
      /* Embedded CSS */
      h1 {
        border: 1px solid red;
      }
    </style>
  </head>
  <body>
    <h1>헤딩 레벨1</h1>
  </body>
</html>
```

&nbsp;  

### 3. Inline

특정 HTML 요소에 style 속성의 값으로 추가하는 방법이다. 그러나 이 방법은 구조와 표현의 분리라는 관점에서 적합하지 않으며, inline 방식의 스타일은 선택자의 우선순위가 가장 높기 때문에 스타일의 재정의가 어렵다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <title>Document</title>
  </head>
  <body>
    <h1 style="border: 1px solid red;">헤딩 레벨1</h1>
    <p style="color: lightgreen;">This is a paragraph.</p>
  </body>
</html>
```

