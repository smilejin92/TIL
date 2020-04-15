# ARIA: States and Properties

ARIA는 HTML 요소의 의미(sematics)를 정의한다. 적용된 의미는 역할과(UI 요소의 타입), 상태 및 속성으로 이루어져 있다. 상태 및 속성 정보는 적용된 역할에 따라 달라진다. 이미 만들어진(네이티브) HTML 요소 중 적절한 의미를 가진 요소가 없다면, 개발자는 특정 요소에 ARIA 역할과 상태 및 속성 정보를 추가하여 해당 요소의 생존 주기(life cycle)동안 접근 가능케 해야한다. ARIA를 사용하는 것은 브라우저의 접근성 API에 추가적인 정보를 노출시키는 것 뿐, DOM에 영향을 주지 않는다.

&nbsp;  

## 상태와 속성 (States and Properties)

WAI-ARIA는 다양한 운영 체제 플랫폼에서 접근성 API를 지원하는 데 사용되는 접근성 상태 및 속성을 제공한다. 보조 기술(assistive technologies)은 user agent DOM 혹은 접근성 API를 통해 이러한 정보에 접근할 수 있다. 역할(role) 정보와 함께 user agent는 사용자에게 UI 정보를 보조 기술에 언제든지 제공할 수 있다. 상태 혹은 속성 값의 변경은 보조 기술에 전달되고, 사용자가 변경이 발생했음을 인지할 수 있도록 한다.

아래 예제는 목록 아이템(`li`)을 체크 가능한 메뉴 아이템으로 사용하며, 자바스크립트를 통해 마우스와 키보드 이벤트를 감지하여 `aria-checked` 값을 반전시킨다. 이러한 위젯 동작을 user agent에 알리기 위해 역할 속성이 사용된다.

```html
<li role="menuitemcheckbox" aria-checked="true">Sort by Last Modified</li>
```

대부분의 모던 user agent는 CSS 속성 선택자를 지원하며, CSS 속성 선택자를 사용하여 WAI-ARIA 속성을 가진 요소를 선택할 수 있도록 한다.

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

아래 상태와 속성의 값은 페이지가 지역화(localized)될 때 보조 기술 사용자가 이해할 수도록 번역되어야 한다.

| 상태 및 속성                                                 | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [aria-label](https://www.w3.org/TR/wai-aria-1.2/#aria-label) | 현재 요소를 레이블하는 문자열을 정의한다.                    |
| [aria-placeholder](https://www.w3.org/TR/wai-aria-1.2/#aria-placeholder) | 입력 양식이 비어있을 때 데이터 입력을 돕기 위한 짧은 힌트(단어 혹은 짧은 구절)를 정의한다. |
| [aria-roledescription](https://www.w3.org/TR/wai-aria-1.2/#aria-roledescription) | 요소의 역할에 대한 설명을 정의한다.                          |
| [aria-valuetext](https://www.w3.org/TR/wai-aria-1.2/#aria-valuetext) | range 위젯을 위한 `aria-valuenow` 속성 값의 대체 텍스트를 정의한다. |

&nbsp;  

### 2. 전역 상태와 속성 (Global States and Properties)

일부 상태와 속성은 역할이 적용되었는 지에 관계 없이 모든 호스트 언어 요소에 적용될 수 있다. 아래 전역 상태와 속성은 **별도로 제한되지 않는 한** 모든 역할과 기본 마크업 요소에서 지원된다. 단, 일부 역할은 전역 상태와 속성의 사용을 제한한다.

| 상태 및 속성                                                 | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [aria-atomic](https://www.w3.org/TR/wai-aria-1.2/#aria-atomic) | `aria-relevant` 속성에 의해 정의된 변경 알림에 근거하여, 보조 기술이 변경된 모든(혹은 일부) 영역을 나타낼 것인지 명시한다. |
| [aria-busy](https://www.w3.org/TR/wai-aria-1.2/#aria-busy)   | 요소가 변경되는 중임을 나타낸다. 또한 보조 기술에 해당 요소를 사용자에게 노출하기 전에 변경이 모두 완료될 때까지 대기할 것을 나타낸다. |
| [aria-controls](https://www.w3.org/TR/wai-aria-1.2/#aria-controls) | 컨텐츠가 현재 요소에 의해 제어되는 요소를 식별한다. 예를 들어 `tab` 요소의 `aria-controls` 속성 값으로 `tabpanel`의 `id`가 맵핑될 수 있다. |
| [aria-current](https://www.w3.org/TR/wai-aria-1.2/#aria-current) | 컨테이너 혹은 관련 요소 집합 내에서 현재 항목을 나타내는 요소를 식별한다. |
| [aria-describedby](https://www.w3.org/TR/wai-aria-1.2/#aria-describedby) | 현재 요소를 설명하는 요소를 식별한다.                        |
| [aria-details](https://www.w3.org/TR/wai-aria-1.2/#aria-details) | 현재 요소를 자세히 설명하는 요소를를 식별한다.               |
| [aria-dropeffect](https://www.w3.org/TR/wai-aria-1.2/#aria-dropeffect) | deprecated in ARIA 1.1                                       |
| [aria-flowto](https://www.w3.org/TR/wai-aria-1.2/#aria-flowto) | 컨텐츠의 alternate reading order 중 다음 요소를 식별한다. alternate reading order는 사용자의 결정에 의해 보조 기술이 문서의 기본 읽기 순서를 override 한 것을 의미한다. |
| [aria-grabbed](https://www.w3.org/TR/wai-aria-1.2/#aria-grabbed) | deprecated in ARIA 1.1                                       |
| [aria-hidden](https://www.w3.org/TR/wai-aria-1.2/#aria-hidden) | 요소를 접근성 API에 노출시킬 것인지에 대한 여부를 나타낸다.  |
| [aria-keyshortcuts](https://www.w3.org/TR/wai-aria-1.2/#aria-keyshortcuts) | 요소를 활성화 시키거나 포커스를 맞출 수 있는 키보드 단축키를 나타낸다. |
| [aria-label](https://www.w3.org/TR/wai-aria-1.2/#aria-label) | 현재 요소를 레이블하는 문자열을 정의한다.                    |
| [aria-labelledby](https://www.w3.org/TR/wai-aria-1.2/#aria-labelledby) | 현재 요소를 레이블하는 요소를 식별한다.                      |
| [aria-live](https://www.w3.org/TR/wai-aria-1.2/#aria-live)   | 요소가 업데이트 될 것임을 나타낸다. 또한 user-agent, 보조 기술, 사용자가 실시간 영역으로부터 예상할 수 있는 업데이트의 타입을 설명한다. |
| [aria-owns](https://www.w3.org/TR/wai-aria-1.2/#aria-owns)   | DOM 요소 사이의 시각적, 기능적, 맥락적 부모/자식 관계를 정의하기 위해 요소를 식별한다.  DOM 계층 구조를 통해 요소 사이의 부모/자식 관계를 나타낼 수 없을 때 사용된다. |
| [aria-relevant](https://www.w3.org/TR/wai-aria-1.2/#aria-relevant) | 실시간 영역(live region) 안의 accessibility tree가 변경되었을 때, user agent가 실행할 알림을 나타낸다. |
| [aria-roledescription](https://www.w3.org/TR/wai-aria-1.2/#aria-roledescription) | 요소의 역할에 대한 설명을 정의한다.                          |

&nbsp;  

### 3. 위젯 속성(attributes)

아래는 위젯 역할을 가진 요소를 지원하는 목적으로 사용된다. 위젯 속성은 사용자 입력을 받아 요청 작업을 수행하는 UI 요소에 적용될 수 있다.

| 속성                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [aria-autocomplete](https://www.w3.org/TR/wai-aria-1.2/#aria-autocomplete) |                                                              |
| [aria-checked](https://www.w3.org/TR/wai-aria-1.2/#aria-checked) | `checkbox`, `radio` 등 체크 가능한 요소의 상태를 나타내는 속성. |
| [aria-disabled](https://www.w3.org/TR/wai-aria-1.2/#aria-disabled) | 인지할 수 있지만 사용할 수 없는 요소임을 나타내는 상태       |
| [aria-errormessage](https://www.w3.org/TR/wai-aria-1.2/#aria-errormessage) | 자신에 대한 에러 메시지를 나타내는 요소의 참조. (속성)       |
| [aria-expanded](https://www.w3.org/TR/wai-aria-1.2/#aria-expanded) | 자신이 포함하는(제어하는) 그룹 요소가 펼쳐져 있는지에 대한 상태 |
| [aria-haspopup](https://www.w3.org/TR/wai-aria-1.2/#aria-haspopup) | 현재 요소가 `menu` 혹은 `dialog` 같은 팝업 요소를 포함하고 있는지 명시하는 속성 |
| [aria-hidden](https://www.w3.org/TR/wai-aria-1.2/#aria-hidden) | 접근성 API에 현재 요소를 노출시킬 것인지 명시하는 속성       |
| [aria-invalid](https://www.w3.org/TR/wai-aria-1.2/#aria-invalid) | 입력된 값이 어플리케이션의 양식에 맞지 않음을 나타내는 상태  |
| [aria-label](https://www.w3.org/TR/wai-aria-1.2/#aria-label) | 현재 요소의 이름을 나타내는 문자열 속성                      |
| [aria-level](https://www.w3.org/TR/wai-aria-1.2/#aria-level) | 요소의 계층 레벨을 나타내는 속성                             |
| [aria-modal](https://www.w3.org/TR/wai-aria-1.2/#aria-modal) | 요소가 표시될 때 modal 형식인지에 속성                       |
| [aria-multiline](https://www.w3.org/TR/wai-aria-1.2/#aria-multiline) | 텍스트 박스가 여러 줄을 입력 받을 것인지에 대한 속성         |
| [aria-multiselectable](https://www.w3.org/TR/wai-aria-1.2/#aria-multiselectable) | 선택 가능한 후손 요소 중 두 개 이상의 항목을 선택할 수 있는지 나타내는 속성 |
| [aria-orientation](https://www.w3.org/TR/wai-aria-1.2/#aria-orientation) | 요소의 진행 방향(horizontal, vertical)을 나타내는 속성       |
| [aria-placeholder](https://www.w3.org/TR/wai-aria-1.2/#aria-placeholder) | 데이터 입력 시 사용자에게 제공되는 짧은 힌트(단어 혹은 문장) 속성 |
| [aria-pressed](https://www.w3.org/TR/wai-aria-1.2/#aria-pressed) | 토글 버튼이 눌렸는지에 대한 상태                             |
| [aria-readonly](https://www.w3.org/TR/wai-aria-1.2/#aria-readonly) | 수정 불가능한 요소임을 나타내는 속성                         |
| [aria-required](https://www.w3.org/TR/wai-aria-1.2/#aria-required) | 입력이 필수인 요소임을 나타내는 속성                         |
| [aria-selected](https://www.w3.org/TR/wai-aria-1.2/#aria-selected) | 요소가 선택되었는지 나타내는 상태                            |
| [aria-sort](https://www.w3.org/TR/wai-aria-1.2/#aria-sort)   | `table` 혹은 `grid`의 항목이 오름차순 혹은 내림차순으로 정렬되었는지 나타내는 속성 |
| [aria-valuemax](https://www.w3.org/TR/wai-aria-1.2/#aria-valuemax) | range 위젯에서 허용된 최대 값을 나타내는 속성                |
| [aria-valuemin](https://www.w3.org/TR/wai-aria-1.2/#aria-valuemin) | range 위젯에서 허용된 최소 값을 나타내는 속성                |
| [aria-valuenow](https://www.w3.org/TR/wai-aria-1.2/#aria-valuenow) | range 위젯에서 현재 선택된 값을 나타내는 속성                |
| [aria-valuetext](https://www.w3.org/TR/wai-aria-1.2/#aria-valuetext) | range 위젯의 `aria-valuenow` 속성 값의 대체 텍스트 속성      |

