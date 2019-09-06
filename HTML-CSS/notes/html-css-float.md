* 가상요소 (Pseudo class)

  * ::before (:before -> 하위 호환) - first child node

  * ::after - last child node

  * inline element

    ```html
    (in html)
    <li><a>real element</a></li>
    
    (in css)
    li::before {
        background-color: orange;
        content: "가상요소";
    }
    ```

  * 단점 : screen reader에 가상요소까지 같이 읽힘

    ([see more](https://www.youtube.com/watch?v=hvEfSbHJAfU&list=PLtaz5vK7MbK3EAPhmB2gFnCU9qU72YMq3&index=4))

  * [Icon Font 사용 가능](https://fontawesome.com/)

    ```html
    <i class="fas fa-camera"></i> <!-- this icon's 1) style prefix == fas and 2) icon name == camera -->
    <i class="fas fa-camera"></i> <!-- using an <i> element to reference the icon -->
    <span class="fas fa-camera"></span> <!-- using a <span> element to reference the icon -->
    ```

  * http://fontello.com/

  ---

  * :hover
  * :focus

---

### nth-child (구조 선택자)

* solve fence-post issue

### 여백 지정 대상

- margin vs. padding
- wide lickable element
- inline 요소는 좌우로는 늘어나지만 (padding, margin), 위로는 line-height의 영향을 받음

(tab 키로 선택되는 요소들은 `<a>` 혹은 `<form>`)

### Main-menu Markup

```html
<h1> (not visible)
	<nav>
		<h2>메인 메뉴</h2> -> a11y.hidden (accessibility)
        <ul class="menu">
            <li>
                (<a> vs. <span>)
                <a class="btn-menu" href="#" role="button">HTML에 대해</a>
                <ul class="sub-menu">
                    <li><a href="page1">예제 1</a></li>
                    <li><a href="page2">예제 2</a></li>
                    <li><a href="page3">예제 3</a></li>
                </ul>
            </li>
        </ul>
	</nav>
</h1> (not visible)
```

### ROLE 부여

* Sementic 하지 않은 `<div>` 혹은 원래 목적의 `<a>` 같은 태그에 `role` 속성을 부여하여 sementic 문제 해결

### 요소 배치 속성

* flex

* inline-block

* position

* ### float: 특 떠있음

  * 뜨는 순간 다음 요소가 당겨서 들어와짐?
  * float의 부모 노드에게 overflow: hidden 설정
  * clear

* grid (respoinsive)

* "margin" 병합

### aria-label

### border-radius



