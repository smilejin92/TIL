# HTML Placeholder 링크의 사용 목적

HTML5 이전에는 `<a>` 요소를 사용할 때 필수로 입력해야 하는 속성은 `href`뿐이었다. 하지만 HTML5에서는 `href` 속성마저 생략할 수 있게 되었다. 아무 속성도 없는 `<a>` 요소를 placeholder link라 부른다.

```html
<a>Placeholder link</a>
```

&nbsp;  

## 1. 개발 기간 중 Placeholder 링크 사용

대부분의 웹 디자이너들은 웹 사이트를 디자인하는 과정에서 placeholder 링크를 한 번쯤은 사용하게 된다. HTML5 이전의 디자이너는 이러한 단계에서 아래와 같은 placeholder 링크를 작성했을 것이다.

```html
<a href="#">link text</a>
```

placeholder 링크의 `href` 속성값으로  `#`을 사용하는 것의 문제점은 해당 태그가 클릭 가능하다는 것이다. 이는 디자이너가 나중에 올바른 주솟값으로 변경해야 하는 사실을 잊게 만들 수도 있다.

따라서 개발 기간 중 `<a>` 요소를 단지 placeholder의 역할로 사용할 것이라면 아무 속성도 사용하지 않으면 된다. 아무런 속성도 가지지 않는 `<a>` 태그는 클릭 되지 않으며, CSS로 스타일링하는 데 아무런 지장이 없다. 다만 `<a>`요소를 placeholder 링크로 사용하는 것은 키보드 포커싱이 안되며, 하이퍼링크의 역할을 잃기 때문에 접근성 차원에서 문제가 될 수 있다. 

&nbsp;  

## 2. 라이브 사이트에서 Placeholder 링크 사용

placeholder 링크는 개발 목적으로만 사용되는 것은 아니다. placeholder 링크는 페이지에서 현재 내가 위치한 곳을 표시하는 내비게이션의 역할로써 사용되기도 한다. 예를 들어, 현재 방문 중인 메뉴 탭에 대해 CSS 속성을 별도로 지정하고 싶다면, 해당 메뉴 탭에만 `href` 속성을 부여한 후 CSS 속성 선택자로 스타일링할 수 있다.

<img src="https://user-images.githubusercontent.com/32444914/78852557-9fcd5980-7a57-11ea-83bb-5f0f139a83d9.png" style="zoom:50%;" />

```html
<ul>
  <li><a>메뉴1</a></li>
  <li><a>메뉴2</a></li>
  <li><a href="#">방문 중 메뉴</a></li>
</ul>

<style>
	a {
    color: black;
    text-decoration: none;
  }

  a[href] {
    color: tomato;
    font-weight: bold;
    text-decoration: underline;
  }
</style>
```

이러한 방법을 통해 메뉴 요소의  `class` 속성값을 변경하거나, 메뉴 탭의 부모 요소에 "active" 상태를 추가하는 방법을 사용하지 않아도 현재 방문 중인 메뉴에 대한 피드백을 구현할 수 있다.

