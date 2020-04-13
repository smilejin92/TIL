# ARIA: 역할, 상태, 속성

ARIA는 HTML 요소의 의미(sematics)를 정의한다. 적용된 의미는 역할과(UI 요소의 타입을 정의), 상태 & 속성으로 이루어져 있다. 상태와 속성 정보는 적용된 역할에 따라 달라진다. 이미 만들어진(네이티브) HTML 요소 중 적절한 의미를 가진 요소가 없다면, 개발자는 특정 요소에 ARIA 역할 및 상태 & 속성을 추가하여 해당 요소의 생존 주기(life cycle)동안 접근 가능케 해야한다. ARIA 속성을 사용하는 것은 브라우저의 접근성 API에 추가적인 정보를 노출시키는 것 뿐, DOM에 영향을 주지 않는다.

## 역할(Roles)

### 위젯 역할

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [button](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/button_role) | 클릭될 수 있는 요소에 사용되며, 사용자에 의해 활성화되면 특정 액션(response)을 실행할 수 있어야한다. |
| [checkbox](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role) | true, false, mixed의 체크 가능한 상태를 가진 입력 요소로 사용된다. 해당 역할의 요소는 반드시 `aria-checked` 속성을 사용하여 체크박스의 상태를 보조 기기에 노출시켜야 한다. |
| [gridcell](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Gridcell_Role) | 그리드(grid, table)의 셀(cell)을 만들기 위한 역할이다. HTML `td` 요소의 기능을 흉내내기 위한 목적으로 사용된다. 컨텐츠를 테이블 스타일로 나열할 때 사용할 수 있다. |
| [link](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role) | 하이퍼링크를 생성하는 요소를 식별하기 위해 사용될 수 있다. link 역할을 가진 요소는 탭(tab)을 사용하여 포커스를 받을 수 있어야하며, <kbd>Enter</kbd>키를 통해 링크로 이동할 수 있어야한다. |
| [menuitem](https://w3c.github.io/aria/#menuitem)             | menu 혹은 menubar 역할을 가진 요소의 하위에 옵션 역할로 사용될 수 있다. |
| [menuitemcheckbox](https://w3c.github.io/aria/#menuitemcheckbox) | true, false, mixed의 체크 가능한 상태를 가진 menuitem으로 사용된다. menuitemcheckbox 요소의 `aria-checked` 속성은 해당 요소가 체크되었는지(true), 체크되지 않았는지(false), true와 false가 섞여있는 menuitemcheckbox를 포함하는 하위 메뉴(mixed)의 상태를 표시한다. menu, menubar 혹은 menu, menubar 하위의 group 역할을 가진 요소의 하위에서만 사용될 수 있다. |
| [menuitemradio](https://w3c.github.io/aria/#menuitemradio)   | 선택 가능한 menuitem. 그룹 내 동일한 역할을 가진 요소 중 오직 하나만 체크 가능한 상황에 사용할 수 있다. 그룹 내 하나의 아이템이 선택되면, 이전에 체크된 아이템은 선택해제 상태가 되어야 한다 (`aria-checked="false"`). |
| [option](https://w3c.github.io/aria/#option)                 | listbox 역할을 가진 요소 하위의 선택 가능한 아이템에 사용할 수 있다. option 역할을 가진 요소는 반드시 listbox 역할을 가진 요소, 혹은 listbox 하위의 group 역할을 가진 요소 하위에서만 사용할 수 있다. option 역할을 가진 요소는 암묵적으로 `aria-selected="false"` 속성을 가지고 있다. |
| [progressbar](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_progressbar_role) | 시간이 오래 걸리거나 여러 단계로 이루어진 작업의 진행률를 표시할 때 사용된다. 만약 진행률을 실질적으로 계산할 수 있다면 `aria-valuenow`, `aria-valuemin`, `aria-valuemax` 속성을 사용하여 진행률을 표시해야 한다. |
| [radio](https://w3c.github.io/aria/#radio)                   | 체크 가능한 입력 요소. 그룹 내 동일한 역할을 가진 요소 중 오직 하나만 체크 가능한 상황에 사용할 수 있다. |
| [scrollbar](https://w3c.github.io/aria/#scrollbar)           | 스크롤바는 현재 값(위치)과 이동 가능한 영역의 범위를 나타낸다. 이동 가능한 영역의 범위는 스크롤바의 진행 방향(orientation)에 대해여 스크롤바의 크기와 "thumb"(값을 변경하기 위한 수단)의 위치를 통해 계산된다. `aria-controls` 속성을 사용하여 반드시 스크롤바가 제어하는 영역을 참조해야한다. |
| [searchbox](https://w3c.github.io/aria/#scrollbar)           | 검색을 위한 텍스트 박스.                                     |
| [separator](https://w3c.github.io/aria/#separator)           | 섹션의 컨텐츠 혹은 menuitems의 그룹을 구분/분리할 때 사용한다. separator는 두 가지 용도로 사용될 수 있다. 단순히 시각적 용도로 활용되는 separator와 포커스 받을 수 있는 separator의 위치를 조절하여 위젯의 크기를 조절할 수 있는 용도로 사용된다. 후자의 경우, separator의 현재 위치 정보를 포함하는 `aria-valuenow` 속성을 명시해야한다. |
| [slider](https://w3c.github.io/aria/#slider)                 | 주어진 범위(range) 내에서 사용자가 값을 입력하는 영역. 슬라이더는 현재 값과 선택 가능한 값의 범위를 나타낸다. 선택 가능한 값의 범위는 슬라이더의 크기와 "thumb"(값을 변경하기 위한 수단)의 위치를 통해 계산된다. `aria-valuenow` 속성을 사용하여 반드시 현재 선택된 값에 대한 정보를 제공해야한다. |
| [spinbutton](https://w3c.github.io/aria/#spinbutton)         | 정해진 범위 내의 선택지를 제공할 때 사용된다. 스핀버튼은 대체로 선택된 값을 증가/감소 버튼을 통해 선택지를 하나씩 이동하여 변경할 수 있도록 한다. 스핀버튼 하위에 올 수 있는 요소는 text 박스와 혹은 두 개의 button 요소로 제한되어있다. 다른 방법으로는 text input요소에 스핀버튼 역할을 명시하여 형제 레벨에 두 개의 버튼을 작성해도 된다. |
| [switch](https://w3c.github.io/aria/#switch)                 | on/off 상태를 가진 checkbox 역할. `aria-checked` 속성을 통해 on(true), off(false)의 상태를 명시한다. 스위치 역할은 `aria-checked` 속성 값으로 `mixed`를 사용할 수 없다. 만약 사용한다면, `false`로 인식된다. |
| [tab](https://w3c.github.io/aria/#tab)                       | tablist 하위의 대화형 요소를 의미한다. 활성화되면 tab과 연결된 tabpanel을 표시한다. tab 역할의 요소는 tablist 역할 요소의 자식 요소이거나, tablist의 `aria-owns` 속성에 자신의 id를 포함해야한다. 또한 `aria-controls` 속성의 값으로 해당 tab과 연결된 tabpanel의 id를 사용할 수 있다. |
| [tabpanel](https://w3c.github.io/aria/#tabpanel)             | tab에 관련된 자료를 포함하는 컨테이너 역할. `aria-controls` 혹은 `aria-labelledby` 속성을 통해 특정 tab을 참조할 수 있다. |
| [textbox](https://w3c.github.io/aria/#textbox)               | 자유양식의 텍스트 값을 입력 받는 역할.                       |
| [treeitem](https://w3c.github.io/aria/#treeitem)             | tree 역할 요소의 옵션. treeitem요소 하위에 서브 레벨 tree 요소가 있다면 펼쳐지거나 접힐 수 있다. treeitem을 포함하는 요소는 반드시 group 혹은 tree 역할 속성을 가져야한다. |

&nbsp;  

## 관련 링크

* [Using ARIA: Roles, states, and properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)

