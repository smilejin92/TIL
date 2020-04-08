# HTML Placeholder 링크의 사용 목적

HTML5 이전에는 `<a>` 요소를 사용할 때 필수로 입력해야하는 속성은 `href`뿐이었다.하지만 HTML5에서는 `href` 속성마저 생략할 수 있게되었다. 아무 속성도 없는 `<a>` 요소를 placeholder link라 부른다.

```html
<a>Placeholder link</a>
```

&nbsp;  

## 개발 기간 중 Placeholder 링크 사용

대부분의 웹 개발자들은 웹 사이트를 디자인하는 과정에서 placeholder 링크를 한번 쯤은 사용하게 된다. HTML5 이전의 개발자는 이러한 단계에서 아래와 같은 placeholder 링크를 작성했을 것이다.

```html
<a href="#">link text</a>
```

placeholder 링크의 `href` 속성 값으로  `#`을 사용할 때의 문제점은 해당 태그가 클릭 가능하다는 것이다. 이는 개발자가 나중에 올바른 주소 값으로 변경해야하는 사실을 잊게 만들 수도 있다.

따라서 개발 기간 중 `<a>` 요소를 단지 placeholder의 역할로 사용할 것이라면 아무 속성도 사용하지 않으면된다. 아무런 속성도 가지지 않는 `<a>` 태그는 클릭되지 않으며, CSS로 스타일링하는 데 아무런 지장이 없다.

&nbsp;  

## 라이브 사이트에서 Placeholder 링크 사용

placeholder 링크는 개발 목적으로만 사용되는 것은 아니다. 