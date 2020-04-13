# ARIA: 역할, 상태, 속성

ARIA는 HTML 요소에 적용될 수 있는 의미(sematics)를 정의한다. 적용된 의미는 역할과(UI 요소의 타입을 정의), 상태 & 속성으로 구분된다. 상태와 속성 정보는 적용된 역할에 따라 달라진다. 이미 만들어진(네이티브) HTML 요소 중 적절한 의미를 가진 요소가 없다면, 개발자는 특정 요소에 ARIA 적절한 역할 및 상태 & 속성을 추가하여 해당 요소의 생존 주기(life cycle)동안 접근 가능케 해야한다. ARIA 속성을 사용하는 것은 브라우저의 접근성 API에 추가적인 정보를 노출시키는 것 뿐, DOM에 영향을 주지 않는다.

## 역할(Roles)

### 위젯 역할

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [button](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/button_role) | 클릭할 수 있는 요소에 사용되며, 사용자에 의해 활성화되면 특정 액션(response)을 실행할 수 있어야한다. |
| [checkbox](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role) | 체크 가능한 대화형(interactive) 컨트롤에 사용된다.           |
| [gridcell](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Gridcell_Role) | 그리드(grid, table)의 셀(cell)을 흉내내기 위한 역할이다. 컨텐츠를 테이블 스타일로 나열할 때 사용할 수 있다. |
| [link](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role) | 하이퍼링크를 생성하는 요소를 식별하기 위해 사용될 수 있다. link 역할을 가진 요소는 탭(tab)을 사용하여 포커스를 받을 수 있어야하며, <kbd>Enter</kbd>키를 통해 링크로 이동할 수 있어야한다. |
| [menuitem](https://w3c.github.io/aria/#menuitem)             | menu 혹은 menubar 역할을 가진 요소의 하위에 옵션 역할로 사용될 수 있다. |
| [menuitemcheckbox](https://w3c.github.io/aria/#menuitemcheckbox) | true, false, mixed의 체크 가능한 상태를 가진 요소에 사용된다. menu, menubar 혹은 menu, menubar 하위의 group 역할을 가진 요소의 하위에서만 사용될 수 있다. |
| [menuitemradio](https://w3c.github.io/aria/#menuitemradio)   | 체크 가능한 menuitem. 동일한 역할을 가진 요소들 중 오직 하나만 체크 가능한 상황에 사용할 수 있다. |
| [option](https://w3c.github.io/aria/#option)                 | listbox 역할을 가진 요소 하위의 선택 가능한 아이템에 사용할 수 있다. option 역할을 가진 요소는 반드시 listbox 역할을 가진 요소 혹은 listbox 하위의 group 역할을 가진 요소 하위에서만 사용할 수 있다. |
| [progressbar](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_progressbar_role) | 시간이 오래 걸리거나 여러 단계로 이루어진 작업의 진행률를 표시할 때 사용된다. 만약 진행률을 실질적으로 계산할 수 있다면 `aria-valuenow`, `aria-valuemin`, `aria-valuemax` 속성을 사용하여 진행률을 표시해야 한다. |
| [scrollbar](https://w3c.github.io/aria/#scrollbar)           |                                                              |
| searchbox                                                    |                                                              |
| separator                                                    |                                                              |
| slider                                                       |                                                              |
| spinbutton                                                   |                                                              |
| switch                                                       |                                                              |
| tab                                                          |                                                              |
| tabpanel                                                     |                                                              |
| textbox                                                      |                                                              |
| treeitem                                                     |                                                              |

&nbsp;  

## 관련 링크

* [Using ARIA: Roles, states, and properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)