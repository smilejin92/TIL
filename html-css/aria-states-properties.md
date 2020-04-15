# ARIA: States and Properties

ARIA는 HTML 요소의 의미(sematics)를 정의한다. 적용된 의미는 역할과(UI 요소의 타입을 정의), 상태 및 속성으로 이루어져 있다. 상태 및 속성 정보는 적용된 역할에 따라 달라진다. 이미 만들어진(네이티브) HTML 요소 중 적절한 의미를 가진 요소가 없다면, 개발자는 특정 요소에 ARIA 역할과 상태 및 속성을 추가하여 해당 요소의 생존 주기(life cycle)동안 접근 가능케 해야한다. ARIA를 사용하는 것은 브라우저의 접근성 API에 추가적인 정보를 노출시키는 것 뿐, DOM에 영향을 주지 않는다.

&nbsp;  

## 상태와 속성 (States and Properties)

WAI-ARIA는 다양한 운영 체제 플랫폼에서 접근성 API를 지원하는 데 사용되는 접근성 상태 및 속성을 제공한다. 보조 기술(assistive technologies)은 user agent DOM 혹은 접근성 API를 통해 이 정보에 접근할 수 있다. 역할(role) 정보와 함께 user agent는 사용자에게 UI 정보를 보조 기술에 언제든지 제공할 수 있다. 상태 혹은 속성 값의 변경은 보조 기술에 전달되고, 사용자가 변경이 발생했음을 인지할 수 있도록 한다.

아래 예제는 목록 아이템(`li`)을 체크 가능한 메뉴 아이템으로 사용하며, 자바스크립트를 통해 마우스와 키보드 이벤트를 감지하여 `aria-checked` 값을 반전시킨다. 이러한 위젯 동작을 user agent에 알리기 위해 역할(role) 속성이 사용된다.

```html
<li role="menuitemcheckbox" aria-checked="true">Sort by Last Modified</li>
```

대부분의 모던 user agent는 CSS 속성 선택자를 지원하며, CSS 속성 선택자를 사용하여 WAI-ARIA 속성을 선택할 수 있도록 한다.

```css
[aria-checke="true"] {
  font-weight: bold;
}

[aria-checked="true"]::before {
  background-image: url(checked.gif);
}
```

&nbsp;  

### 1. 번역될 수 있는 상태와 속성 (Translatable States and Properties)

아래 상태와 속성 값은 페이지가 지역화(localized)될 때 보조 기기 사용자가 이해할 수도록 번역되어야 한다.

| 상태 및 속성                                                 | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [aria-label](https://www.w3.org/TR/wai-aria-1.2/#aria-label) | 특정 요소를 명명(label)하는 문자열 속성                      |
| [aria-placeholder](https://www.w3.org/TR/wai-aria-1.2/#aria-placeholder) | 데이터 입력 시 사용자에게 제공되는 짧은 힌트(단어 혹은 문장) 속성 |
| [aria-roledescription](https://www.w3.org/TR/wai-aria-1.2/#aria-roledescription) | 요소의 역할을 설명하는 속성                                  |
| [aria-valuetext](https://www.w3.org/TR/wai-aria-1.2/#aria-valuetext) | range 위젯의 `aria-valuenow` 속성의 대체 텍스트 속성         |

&nbsp;  

### 2. 전역 상태와 속성 (Global States and Properties)

