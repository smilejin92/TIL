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
| [aria-label](https://www.w3.org/TR/wai-aria-1.2/#aria-label) | 현재 요소의 이름을 나타내는 문자열 속성                      |
| [aria-placeholder](https://www.w3.org/TR/wai-aria-1.2/#aria-placeholder) | 데이터 입력 시 사용자에게 제공되는 짧은 힌트(단어 혹은 문장) 속성 |
| [aria-roledescription](https://www.w3.org/TR/wai-aria-1.2/#aria-roledescription) | 요소의 역할을 설명하는 속성                                  |
| [aria-valuetext](https://www.w3.org/TR/wai-aria-1.2/#aria-valuetext) | range 위젯의 `aria-valuenow` 속성의 대체 텍스트 속성         |

&nbsp;  

### 2. 전역 상태와 속성 (Global States and Properties)

일부 상태와 속성은 역할에 관계 없이 모든 요소에 적용될 수 있다. 아래 전역 상태와 속성은 별도로 제한되지 않는 한 모든 역할과 기본 마크업 요소에서 지원된다.

| 상태 및 속성                                                 | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [aria-atomic](https://www.w3.org/TR/wai-aria-1.2/#aria-atomic) | `aria-relevant` 속성으로 정의한 변경 알림을 통해 변경된 모든(혹은 일부) 영역에 대한 정보를 보조 기기에 전달할 것인지에 대해 명시하는 속성(`true`, `false`) |
| [aria-busy](https://www.w3.org/TR/wai-aria-1.2/#aria-busy)   | 요소가 변경되는 중(being modified)임을 명시하는 상태(`true`, `false`). 보조 기기는 변경 사항이 모두 완료될 때까지 해당 요소를 사용자에게 노출시키는 것을 지연할 수 있다. |
| [aria-controls](https://www.w3.org/TR/wai-aria-1.2/#aria-controls) | 현재 요소가 제어하는 요소를 식별하는 속성. 예를 들어 `tab` 요소의 `aria-controls` 속성 값으로 `tabpanel`의 `id`가 올 수 있다. |
| [aria-current](https://www.w3.org/TR/wai-aria-1.2/#aria-current) | 컨테이너 혹은 관련 요소 그룹 내에서 현재 표시되고 있는 요소를 명시하는 상태. `aria-current`는 관련 요소 그룹 내에서 현재 선택된 / 표시되는 요소를 시각적으로 스타일링한 경우 사용된다 (ex. page 1 of 10) |
| [aria-describedby](https://www.w3.org/TR/wai-aria-1.2/#aria-describedby) | 자신을 설명하는 요소의 참조. (속성)                          |
| [aria-details](https://www.w3.org/TR/wai-aria-1.2/#aria-details) | 자신을 설명하는 요소의 참조. `aria-describedby` 속성보다 더욱 자세한 설명을 가진 요소의 참조. (속성) |
| [aria-dropeffect](https://www.w3.org/TR/wai-aria-1.2/#aria-dropeffect) | deprecated in ARIA 1.1                                       |
| [aria-flowto](https://www.w3.org/TR/wai-aria-1.2/#aria-flowto) | 읽기 순서 중 다음 컨텐츠 요소를 참조하는 속성. `aria-flowto` 속성은 보조 기기를 사용하는 사용자의 결정에 의해 문서의 기본 읽기 순서을 벗어나 `aria-flowto` 속성이 참조하는 요소로 바로 이동할 수 있도록한다. |
| [aria-grabbed](https://www.w3.org/TR/wai-aria-1.2/#aria-grabbed) | deprecated in ARIA 1.1                                       |
| [aria-hidden](https://www.w3.org/TR/wai-aria-1.2/#aria-hidden) | 요소를 accessibility API에 노출시킬 것인지에 대해 명시하는 상태 |
| [aria-keyshortcuts](https://www.w3.org/TR/wai-aria-1.2/#aria-keyshortcuts) | 요소를 활성화시키거나 요소에 포커스를 맞출 수 있는 단축키를 명시하는 속성. |
| [aria-label](https://www.w3.org/TR/wai-aria-1.2/#aria-label) | 현재 요소의 이름을 나타내는 문자열 속성.                     |
| [aria-labelledby](https://www.w3.org/TR/wai-aria-1.2/#aria-labelledby) | 현재 요소의 이름을 나타내는 요소의 참조. (속성)              |
| [aria-live](https://www.w3.org/TR/wai-aria-1.2/#aria-live)   | 요소가 업데이트될 것임을 명시하는 속성. 속성 값의 종류에 업데이트 알림의 우선 순위가 결정된다. |
| [aria-owns](https://www.w3.org/TR/wai-aria-1.2/#aria-owns)   | DOM 요소의 시각적, 기능적, 맥락적 부모/자식 관계를 정의하기 사용되는 속성. DOM 계층 구조를 통해 요소간 관계를 나타낼 수 없을 때 사용된다. 속성 값으로 한 개 이상의 요소의 참조 값을 공백으로 구분하여 가질 수 있다. |
| [aria-relevant](https://www.w3.org/TR/wai-aria-1.2/#aria-relevant) | 실시간 영역(live region) 내부의 accessibility tree가 조작되었을 때, user agent가 전달할 알림을 명시하는 속성. |
| [aria-roledescription](https://www.w3.org/TR/wai-aria-1.2/#aria-roledescription) | 요소의 역할을 설명하는 속성                                  |

&nbsp;  

### 3. 위젯 속성(attributes)

아래 속성은 

