# ARIA: 역할, 상태, 속성

ARIA는 HTML 요소의 의미(sematics)를 정의한다. 적용된 의미는 역할과(UI 요소의 타입을 정의), 상태 & 속성으로 이루어져 있다. 상태와 속성 정보는 적용된 역할에 따라 달라진다. 이미 만들어진(네이티브) HTML 요소 중 적절한 의미를 가진 요소가 없다면, 개발자는 특정 요소에 ARIA 역할 및 상태 & 속성을 추가하여 해당 요소의 생존 주기(life cycle)동안 접근 가능케 해야한다. ARIA 속성을 사용하는 것은 브라우저의 접근성 API에 추가적인 정보를 노출시키는 것 뿐, DOM에 영향을 주지 않는다.

## 역할(Roles)

### 추상 역할(Abstract roles)

추상 역할은 온톨로지(ontology)에 사용된다. 저자는 **추상 역할을 컨텐츠에 사용하면 안된다**.

| 역할        | 요약                                                         |
| ----------- | ------------------------------------------------------------ |
| command     | 작업을 수행하지만, 입력 데이터를 받지 않는 위젯의 형식       |
| composite   | 자신의 소유인 자식 요소 혹은 후행 요소들을 포함하는 위젯     |
| input       | 데이터를 입력 받을 수 있는 제네릭 타입의 위젯                |
| landmark    | 랜드마크는 페이지의 특정 부문을 보조 기술 사용자가 페이지를 더 쉽게 탐색할 수 있도록 의미론적으로 정의된 섹션을 만드는 역할 |
| range       | 값의 범위를 나타내는 역할                                    |
| roletype    | 다른 모든 역할이 상속되는 기본 역할                          |
| section     | 문서 혹은 어플리케이션의 렌더링 가능한 구조적 역할           |
| sectionhead | 관련된 부문을 분류하거나 요약하는 역할                       |
| select      | 사용자가 선택 항목 그룹에서 선택할 수 있는 양식 위젯         |
| structure   | 문서 구조 요소                                               |
| widget      | 상호작용 가능한 GUI 컴포넌트                                 |
| window      | 브라우저 혹은 어플리케이션 창                                |



### 위젯 역할(Widget roles)

아래 역할 속성은 독립적인(standalone) UI 위젯, 혹은 상위(composite) 위젯에 포함되는 하위 위젯의 역할로서 사용된다. 

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [button](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/button_role) | 클릭될 수 있는 요소에 사용된다. 사용자에 의해 활성화되면 특정 액션(response)을 실행할 수 있어야하며, 키보드 포커스를 받을 수 있어야한다. |
| [checkbox](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role) | `true`, `false` 혹은 `mixed`의 상태를 입력 받을 수 있는 체크 가능한 요소로 사용된다. `checkbox` 요소는 반드시 `aria-checked` 속성을 사용하여 자신의 상태를 보조 기기에 노출시켜야 한다. |
| [gridcell](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Gridcell_Role) | 그리드(grid, table)의 셀(cell)을 만들기 위한 역할이다. HTML `td` 요소의 기능을 흉내내기 위한 목적으로 사용된다. 컨텐츠를 테이블 스타일로 나열할 때 사용할 수 있다. |
| [link](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role) | 하이퍼링크를 생성하는 요소를 식별하기 위해 사용될 수 있다. `link` 역할을 가진 요소는 탭(tab)을 사용하여 포커스를 받을 수 있어야하며, <kbd>Enter</kbd>키를 통해 해당 링크로 이동할 수 있어야한다. |
| [menuitem](https://w3c.github.io/aria/#menuitem)             | `menu` 혹은 `menubar` 역할을 가진 요소의 하위에 옵션 역할로서 사용될 수 있다. |
| [menuitemcheckbox](https://w3c.github.io/aria/#menuitemcheckbox) | `true`, `false` 혹은 `mixed`의 상태를 입력 받을 수 있는 체크 가능한 `menuitem`으로 사용된다. `menuitemcheckbox` 요소는 `aria-checked` 속성을 통해 자신의 상태를 표시해야한다. `menu`, `menubar` 혹은 `menu`, `menubar` 하위의 `group` 역할을 가진 요소의 하위에서만 사용될 수 있다. |
| [menuitemradio](https://w3c.github.io/aria/#menuitemradio)   | 선택 가능한 `menuitem`. 그룹 내 동일한 역할을 가진 요소 중 오직 한 가지 요소만 선택되어야하는 상황에 사용될 수 있다. 그룹 내 한 가지 요소가 선택되면, 이전에 선택된 요소는 선택해제 상태가 되어야 한다 (`aria-checked="false"`). |
| [option](https://w3c.github.io/aria/#option)                 | `listbox` 요소 하위의 선택 가능한 요소에 사용할 수 있다. `option` 역할은 반드시 `listbox` 요소, 혹은 `listbox` 하위의 `group` 요소 하위에서만 사용될 수 있다. `option` 요소는 암묵적으로 `aria-selected="false"` 속성을 가지고 있다. |
| [progressbar](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_progressbar_role) | 시간이 오래 걸리거나 여러 단계로 이루어진 작업의 진행률를 표시할 때 사용된다. 만약 진행률을 실질적으로 계산할 수 있다면 `aria-valuenow`, `aria-valuemin`, `aria-valuemax` 속성을 사용하여 진행률을 표시해야 한다. |
| [radio](https://w3c.github.io/aria/#radio)                   | 선택 가능한 입력 요소. 그룹 내 동일한 역할을 가진 요소 중 오직 한 가지 요소만 선택되어야 하는 상황에 사용될 수 있다. |
| [scrollbar](https://w3c.github.io/aria/#scrollbar)           | 스크롤바는 현재 값(위치)과 이동 가능한 영역의 범위를 나타낸다. 이동 가능한 영역의 범위는 스크롤바의 진행 방향(orientation)에 대하여 스크롤바의 크기와 "thumb"(위치를 변경하기 위한 수단)의 위치를 통해 계산된다. `aria-controls` 속성을 사용하여 반드시 스크롤바가 제어하는 영역을 참조해야한다. |
| [searchbox](https://w3c.github.io/aria/#scrollbar)           | 검색을 위한 텍스트 박스.                                     |
| [separator](https://w3c.github.io/aria/#separator)           | 섹션의 컨텐츠 혹은 `menuitems`의 그룹을 구분/분리할 때 사용한다. `separator`는 두 가지 용도로 사용될 수 있다. 단순히 시각적 용도로 활용되는 `separator`와 위젯의 크기를 조절할 수 있는 구분선으로 사용된다. 후자의 경우, 포커스 받을 수 있어야하며 현재 위치 정보를 포함하는 `aria-valuenow` 속성을 포함해야한다. |
| [slider](https://w3c.github.io/aria/#slider)                 | 주어진 범위(range) 내에서 사용자가 값을 입력하는 영역. 슬라이더는 현재 값과 선택 가능한 값의 범위를 나타낸다. 선택 가능한 값의 범위는 슬라이더의 크기와 "thumb"(값을 변경하기 위한 수단)의 위치를 통해 계산된다. `aria-valuenow` 속성을 사용하여 반드시 현재 선택된 값에 대한 정보를 제공해야한다. |
| [spinbutton](https://w3c.github.io/aria/#spinbutton)         | 정해진 범위 내의 선택지를 제공할 때 사용된다. `spinbutton`은 대체로 선택된 값을 증가/감소 버튼을 통해 선택지를 하나씩 이동하여 변경할 수 있도록 한다. `spinbutton` 하위에 올 수 있는 요소는 `textbox`와 혹은 두 개의 `button` 요소로 제한되어있다. 다른 방법으로는 text input 요소에 `spinbutton` 역할을 지정한 후 형제 레벨에 두 개의 버튼을 작성할 수 있다. |
| [switch](https://w3c.github.io/aria/#switch)                 | on/off 상태를 가진 checkbox 역할. `aria-checked` 속성을 통해 `on`(true), `off`(false)의 상태를 명시한다. `switch` 역할은 `aria-checked` 속성 값으로 `mixed`를 사용할 수 없다. 만약 사용한다면, `false`로 인식된다. |
| [tab](https://w3c.github.io/aria/#tab)                       | `tablist` 하위의 대화형 요소를 의미한다. 활성화되면 `tab`과 연결된 `tabpanel`을 표시한다. `tab` 요소는 `tablist` 요소의 자식 요소이거나, `tablist`의 `aria-owns` 속성에 자신의 `id`를 포함해야한다. 또한 `aria-controls` 속성의 값으로 해당 `tab`과 연결된 `tabpanel`의 `id`를 사용할 수 있다. |
| [tabpanel](https://w3c.github.io/aria/#tabpanel)             | `tab`에 관련된 자료를 포함하는 컨테이너 역할. `aria-controls` 혹은 `aria-labelledby` 속성을 통해 특정 `tab`을 참조할 수 있다. |
| [textbox](https://w3c.github.io/aria/#textbox)               | 자유양식의 텍스트 값을 입력 받는 역할.                       |
| [treeitem](https://w3c.github.io/aria/#treeitem)             | `tree` 요소의 자식(옵션) 요소. `treeitem` 요소 하위에 서브 레벨 `tree` 요소가 있다면, 해당 `treeitem`은 펼쳐지거나 접힐 수 있다. `treeitem`을 포함하는 요소는 반드시 `group` 혹은 `tree` 요소이어야 한다. |

&nbsp;  

### 컴포짓 역할(Composite role)

아래 역할은 복합(composite) UI 위젯의 역할로서 사용된다. 아래 역할은 대체로 하위 위젯을 포함하는 상위의 컨테이너로서 사용된다.

| 역할       | 요약                                                         |
| ---------- | ------------------------------------------------------------ |
| combobox   | 사용자가 입력할 수 있는 값의 목록을 팝업으로 가지고 있는 input 위젯. 팝업은 `listbox`, `grid`, `tree` 혹은 `dialog` 요소로 이루어진다. |
| grid       | 방향 키, <kbd>Home</kbd> 혹은 <kbd>End</kbd> 키 등으로 하위 정보 혹은 대화형 요소를 탐색할 수 있도록 하는 컨테이너형 위젯 |
| listbox    | 선택지 목록을 나타내며 사용자가 한 개 이상의 옵션을 선택할 수 있도록 하는 위젯. 한 가지 옵션만을 선택할 수 있는 single-select listbox와 여러 옵션을 선택할 수 있는 multi-select listbox로 구분된다. |
| menu       | 사용자에게 행동(actions) 혹은 기능(functions)과 같은 선택 목록을 제공하는 위젯. 메뉴 버튼을 활성화하여 메뉴를 펼치는 방법으로 많이 사용된다. |
| menubar    | UI에 지속적으로 노출되어 있는 메뉴이다. 일반적으로 메뉴바는 수평으로 펼쳐져 있으며 UI 상단에 위치하여 빠른 접근을 가능케한다. |
| radiogroup | 한 가지 버튼만을 선택할 수 있는 버튼들의 집합.               |
| tablist    | `tab` 요소의 목록. `tabpanel` 요소의 참조 목록               |
| tree       | 계층적 구조를 표시하는 위젯. 계층 구조에 속한 요소는 자식 요소를 포함할 수 있으며, 이러한 요소는 펼쳐지거나 접힐 수 있다 (ex. 파일 탐색기) |
| treegrid   | 표 정보로 구성된 계층적 데이터 그리드. 표 정보는 편집 가능하거나 대화형이어야 한다. |

&nbsp;  

### 문서 구조 역할(Document structure roles)



## 관련 링크

* [Using ARIA: Roles, states, and properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)

