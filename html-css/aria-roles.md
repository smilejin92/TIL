# ARIA: 역할

ARIA는 HTML 요소의 의미(sematics)를 정의한다. 적용된 의미는 역할과(UI 요소의 타입을 정의), 상태 및 속성으로 이루어져 있다. 상태 및 속성 정보는 적용된 역할에 따라 달라진다. 이미 만들어진(네이티브) HTML 요소 중 적절한 의미를 가진 요소가 없다면, 개발자는 특정 요소에 ARIA 역할과 상태 및 속성을 추가하여 해당 요소의 생존 주기(life cycle)동안 접근 가능케 해야한다. ARIA를 사용하는 것은 브라우저의 접근성 API에 추가적인 정보를 노출시키는 것 뿐, DOM에 영향을 주지 않는다.

## 역할 (Roles)

WAI-ARIA 역할(role)은 `role` 속성을 사용해 HTML 요소에 지정된다.

```html
<li role="menuitem">Open file...</li>
```

역할을 부여하는 것은 보조 기술(assistive technologies)에 해당 요소가 어떻게 다루어져야하는 지에 대한 정보를 제공한다. WAI-ARIA 역할을 부여하여 요소의 태생적 의미(native semantics)을 override하면, DOM에 변화는 없지만 [accessibility tree](https://www.w3.org/TR/wai-aria-1.2/#dfn-accessibility-tree)에 변화를 준다.

&nbsp;  

### 1. 추상 역할 (Abstract roles)

추상 역할은 온톨로지(ontology)에 사용된다. **추상 역할을 컨텐츠에 사용하면 안된다**.

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [command](https://www.w3.org/TR/wai-aria-1.2/#command)       | 작업을 수행하지만 입력 데이터를 받지 않는 위젯 형식          |
| [composite](https://www.w3.org/TR/wai-aria-1.2/#composite)   | navigable descendants 혹은 owned children을 포함하는 위젯    |
| [input](https://www.w3.org/TR/wai-aria-1.2/#input)           | 데이터를 입력 받을 수 있는 제네릭 타입의 위젯                |
| [landmark](https://www.w3.org/TR/wai-aria-1.2/#landmark)     | 특정 목적과 관련이 있으며 중요한 내용을 포함하는 **인지 가능한 섹션**. 페이지 요약에 나열되어 사용자가 해당 영역을 쉽게 탐색할 수 있을만한 부문. |
| [range](https://www.w3.org/TR/wai-aria-1.2/#range)           | 값의 범위를 나타내는 요소                                    |
| [roletype](https://www.w3.org/TR/wai-aria-1.2/#roletype)     | 다른 모든 역할이 상속되는 기본 역할(base role)               |
| [section](https://www.w3.org/TR/wai-aria-1.2/#section)       | 문서 혹은 어플리케이션의 렌더링 가능한 구조적 격납 장치(structural containment unit) |
| [sectionhead](https://www.w3.org/TR/wai-aria-1.2/#sectionhead) | 관련된 섹션의 주제를 명명하거나 요약하는 구조                |
| [select](https://www.w3.org/TR/wai-aria-1.2/#select)         | 사용자가 선택 항목 그룹에서 선택할 수 있는 양식 위젯         |
| [structure](https://www.w3.org/TR/wai-aria-1.2/#structure)   | 문서 구조 요소                                               |
| [widget](https://www.w3.org/TR/wai-aria-1.2/#widget)         | 상호작용 가능한 GUI 컴포넌트                                 |
| [window](https://www.w3.org/TR/wai-aria-1.2/#window)         | 브라우저 혹은 어플리케이션 창                                |

&nbsp;  

### 2. 위젯 역할 (Widget roles)

위젯 역할은 독립적인(standalone) UI 위젯, 혹은 복합(composite) 위젯에 포함되는 하위 위젯의 역할로서 사용된다.

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [button](https://www.w3.org/TR/wai-aria-1.2/#button)         | 클릭되거나 눌렸을 때 사용자가 트리거한 액션(user-triggered)을 실행하는 입력 장치 |
| [checkbox](https://www.w3.org/TR/wai-aria-1.2/#checkbox)     | 체크할 수 있는 입력 장치. `true`, `false` 혹은 `mixed` 값을 가질 수 있다. `checkbox` 요소는 반드시 `aria-checked` 속성을 사용하여 자신의 상태를 보조 기기에 노출시켜야 한다. |
| [gridcell](https://www.w3.org/TR/wai-aria-1.2/#gridcell)     | `grid` 혹은 `treegrid` 안의 `cell`. HTML `td` 요소의 기능을 흉내내기 위한 목적으로 사용된다. |
| [link](https://www.w3.org/TR/wai-aria-1.2/#link)             | 내부 혹은 외부 자원의 대화형 참조(interactive reference). 활성화되면 해당 참조로 이동한다. `link` 요소는 <kbd>Tab</kbd>을 사용하여 포커스를 받을 수 있어야하며, <kbd>Enter</kbd>키를 통해 해당 링크로 이동할 수 있어야한다. |
| [menuitem](https://www.w3.org/TR/wai-aria-1.2/#menuitem)     | `menu` 혹은 `menubar`에 포함되는 선택 항목. `menu`, `menubar` 혹은 `menu`, `menubar` 하위의 `group` 요소 안에서만 사용될 수 있다. |
| [menuitemcheckbox](https://www.w3.org/TR/wai-aria-1.2/#menuitemcheckbox) | 체크할 수 있는 `menuitem`. `true`, `false` 혹은 `mixed` 값을 가질 수 있다. `menuitemcheckbox` 요소는 `aria-checked` 속성을 통해 자신의 상태를 표시해야한다. `menu`, `menubar` 혹은 `menu`, `menubar` 하위의 `group` 요소 안에서만 사용될 수 있다. |
| [menuitemradio](https://www.w3.org/TR/wai-aria-1.2/#menuitemradio) | 체크 가능한 `menuitem`. 그룹 내 동일한 역할을 가진 항목 중 오직 한 가지 항목만 선택될 수 있다. `menu`, `menubar` 혹은 `menu`, `menubar` 하위의 `group` 요소 안에서만 사용될 수 있다. |
| [option](https://www.w3.org/TR/wai-aria-1.2/#option)         | `listbox` 안에 선택할 수 있는 항목. `option`은 반드시 `listbox`  혹은 `listbox` 하위의 `group` 요소 안에서만 사용될 수 있다. `option`는 암묵적으로 `aria-selected="false"` 속성을 가지고 있다. |
| [progressbar](https://www.w3.org/TR/wai-aria-1.2/#progressbar) | 시간이 오래 걸리거나 여러 단계로 이루어진 작업의 진행률를 표시하는 요소. 진행률을 실질적으로 계산할 수 있다면 `aria-valuenow`, `aria-valuemin`, `aria-valuemax` 속성을 사용하여 진행률을 표시해야 한다. |
| [radio](https://www.w3.org/TR/wai-aria-1.2/#radio)           | 체크 가능한 입력 장치. 그룹 내 동일한 역할을 가진 항목 중 오직 한 가지 항목만 선택될 수 있다. |
| [scrollbar](https://www.w3.org/TR/wai-aria-1.2/#scrollbar)   | 보기 영역 내에서 컨텐츠 스크롤을 제어하는 그래픽 개체        |
| [searchbox](https://www.w3.org/TR/wai-aria-1.2/#searchbox)   | 검색을 위한 텍스트 상자                                      |
| [separator](https://www.w3.org/TR/wai-aria-1.2/#separator)   | 섹션의 컨텐츠 혹은 `menuitems` 그룹을 구분하는 요소. `separator`는 두 가지 용도로 사용될 수 있다. 단순히 컨텐츠를 시각적으로 구분하는 경우와 위젯의 크기를 조절할 수 있는 구분선으로 사용된다. 후자의 경우, `separator`는 포커스 받을 수 있어야하며 현재 위치 정보를 포함하는 `aria-valuenow` 속성을 포함해야한다. |
| [slider]()                                                   | 주어진 범위(range) 내에서 사용자가 값을 입력하는 영역. 슬라이더는 현재 값과 선택 가능한 값의 범위를 나타낸다. 선택 가능한 값의 범위는 슬라이더의 크기와 "thumb"(값을 변경하기 위한 수단)의 위치를 통해 계산된다. `aria-valuenow` 속성을 사용하여 반드시 현재 선택된 값에 대한 정보를 제공해야한다. |
| [spinbutton](https://www.w3.org/TR/wai-aria-1.2/#spinbutton) | 사용자가 선택할 수 있는 항목의 범위를 나타내는 양식. `spinbutton`은 증가/감소 버튼을 통해 선택된 항목의 값을 한 단계씩 이동하여 값을 변경할 수 있도록 한다. `spinbutton` 하위에 올 수 있는 요소는 `textbox` 혹은 두 개의 `button` 요소로 제한되어있다. 다른 방법으로는 text input 요소에 `spinbutton` 역할을 지정한 후 형제 레벨에 두 개의 버튼을 작성할 수 있다. |
| [switch](https://www.w3.org/TR/wai-aria-1.2/#switch)         | `on`, `off` 상태를 가진 `checkbox`. `aria-checked` 속성을 통해 `on`(true), `off`(false)의 상태를 명시한다. `switch`는 `aria-checked` 속성 값으로 `mixed`를 사용할 수 없다. 만약 사용한다면 `false`로 인식된다. |
| [tab](https://www.w3.org/TR/wai-aria-1.2/#tab)               | `tablist` 하위의 대화형 요소를 의미한다. 활성화되면 `tab`과 연결된 `tabpanel`을 표시한다. `tab` 요소는 `tablist`의 자식 요소이거나, `tablist`의 `aria-owns` 속성에 자신의 `id`를 포함해야한다. 또한 `tab` 요소의 `aria-controls` 속성값으로 자신과 연결된 `tabpanel`의 `id`를 사용할 수 있다. |
| [tabpanel](https://www.w3.org/TR/wai-aria-1.2/#tabpanel)     | `tab`에 관련된 자료를 포함하는 컨테이너 역할. `aria-controls` 혹은 `aria-labelledby` 속성을 통해 특정 `tab`을 참조할 수 있다. |
| [textbox](https://www.w3.org/TR/wai-aria-1.2/#textbox)       | 자유양식의 텍스트 값을 입력 받는 역할.                       |
| [treeitem](https://www.w3.org/TR/wai-aria-1.2/#treeitem)     | `tree`의 옵션 항목. `tree` 요소의 자식(옵션) 요소. `treeitem` 요소 하위에 서브 레벨 `tree` 요소가 있다면, 해당 `treeitem`은 펼쳐지거나 접힐 수 있다. `treeitem`을 포함하는 요소는 반드시 `group` 혹은 `tree` 요소이어야 한다. |

&nbsp;  

### 3. 컴포짓 역할 (Composite role)

컴포짓 역할은 복합(composite) UI 위젯의 역할로서 사용된다. 컴포짓 역할은 대개 하위 위젯을 포함하는 상위의 컨테이너로서 사용된다.

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [combobox](https://www.w3.org/TR/wai-aria-1.2/#combobox)     | `listbox` 혹은 `grid`와 같은 요소를 제어하여, 사용자가 값을 입력하는 것을 돕는 `input` 요소. |
| [grid](https://www.w3.org/TR/wai-aria-practices-1.2/#grid)   | 한 개 이상의 row를 포함하는 컴포짓 위젯. row의 각 cell은 방향 키, <kbd>Home</kbd> 혹은 <kbd>End</kbd> 키 등으로 접근할 수 있어야한다. |
| [listbox](https://www.w3.org/TR/wai-aria-practices-1.2/#Listbox) | 선택 목록을 나타내며 사용자가 한 개 이상의 항목을 선택할 수 있도록 하는 위젯. 한 가지 항목만을 선택할 수 있는 single-select listbox와 여러 옵션을 선택할 수 있는 multi-select listbox로 구분된다. |
| [menu](https://www.w3.org/TR/wai-aria-practices-1.2/#menu)   | 사용자가 선택할 수 있는 행동(actions) 혹은 기능(functions)의 목록. 메뉴 버튼을 활성화하여 메뉴를 펼치는 방법으로 많이 사용된다. |
| [menubar](https://www.w3.org/TR/wai-aria-practices-1.2/#menu) | UI에 지속적으로 노출되어 있는 메뉴이다. 일반적으로 메뉴바는 수평으로 펼쳐져 있으며 UI 상단에 위치하여 빠르게 접근할 수 있는 메뉴. |
| [radiogroup](https://www.w3.org/TR/wai-aria-practices-1.2/#radiobutton) | `radio` 버튼의 그룹                                          |
| [tablist](https://www.w3.org/TR/wai-aria-1.2/#tablist)       | `tab` 요소의 목록. `tabpanel` 요소의 참조 목록.              |
| [tree](https://www.w3.org/TR/wai-aria-practices-1.2/#TreeView) | 계층적 구조를 나타내는 위젯. 계층 구조에 속한 요소는 자식 요소를 포함할 수 있으며, 이러한 요소는 펼쳐지거나 접힐 수 있다 (ex. 파일 탐색기) |
| [treegrid](https://www.w3.org/TR/wai-aria-practices-1.2/#treegrid) |`tree` 요소처럼 펼쳐지거나 접힐 수 있는 row를 포함하는 `grid` |

&nbsp;  

### 4. 문서 구조 역할 (Document structure roles)

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [applicattion](https://www.w3.org/TR/wai-aria-1.2/#application) | 사용자 입력을 요구하는(또한 포커스 가능한) 요소를 한 개 이상 포함하는 문서 구조 요소. `application`에서 사용자 입력이란 키보드 혹은 제스처 이벤트와 같이 일반 `widget` 역할이 지원하는 표준 상호작용 패턴을 따르지 않는 것을 말한다. |
| [article](https://www.w3.org/TR/wai-aria-1.2/#article)       | 문서, 페이지, 혹은 사이트로부터 독립적인 컨텐츠를 포함하는 영역을 정의할 때 사용 |
| [blockquote](https://www.w3.org/TR/wai-aria-1.2/#blockquote) | 외부 자료에서 인용한 컨텐츠를 정의할 때 사용                 |
| [caption](https://www.w3.org/TR/wai-aria-1.2/#caption)       | `figure`, `table`, 혹은 `grid`을 명명하거나 설명하는 visible 컨텐츠. `figure`, `table`, 혹은 `grid` 요소에 `aria-labelledby` 속성 값으로 `caption`의 `id`를 참조해야한다. |
| [cell](https://www.w3.org/TR/wai-aria-1.2/#cell)             | 테이블 형식 컨테이너의 셀(cell). `cell` 요소는 반드시 `row` 요소에 포함되어야 한다. |
| [columnheader](https://www.w3.org/TR/wai-aria-1.2/#columnheader) | 열(column)의 헤더 정보를 포함하는 셀. HTML의 `th` 요소와 구조적으로 동일한 의미를 갖는다. |
| [definition](https://www.w3.org/TR/wai-aria-1.2/#definition) | 용어나 개념을 정의하는 요소                                  |
| [deletion](https://www.w3.org/TR/wai-aria-1.2/#deletion)     | 삭제 처리되었거나 삭제 요청된 컨텐츠를 포함하는 요소         |
| [directory](https://www.w3.org/TR/wai-aria-1.2/#directory)   | **deprecated** in ARIA 1.2                                   |
| [document](https://www.w3.org/TR/wai-aria-1.2/#document)     | 보조 기기 사용자가 읽기 모드로 탐색할 수 있을만한 컨텐츠를 포함하는 요소 |
| [emphasis]()                                                 | 한 개 이상 강조된 문자                                       |
| [feed](https://www.w3.org/TR/wai-aria-1.2/#feed)             | 스크롤 가능한 `article` 목록(list). 스크롤 시 목록 끝에 `article`이 추가되거나 밀려나는 목록에 사용할 수 있는 역할 |
| [figure](https://www.w3.org/TR/wai-aria-1.2/#figure)         | 그래픽 문서, 이미지, 코드 snippet, 혹은 예제 텍스트를 포함하는 인지 가능한 컨텐츠 영역. `figure`의 일부분은 user-navigable 할 수 있다. |
| [generic](https://www.w3.org/TR/wai-aria-1.2/#generic)       | 어떠한 의미도 가지지 않는 무명의 컨테이너 요소               |
| [group](https://www.w3.org/TR/wai-aria-1.2/#group)           | 보조 기기에 제공된 페이지 요약 혹은 목차에 포함되지 않는 UI 객체들의 집합. |
| [heading](https://www.w3.org/TR/wai-aria-1.2/#heading)       | 페이지 부문의 헤딩                                           |
| [img](https://www.w3.org/TR/wai-aria-1.2/#img)               | 이미지를 형성하는 요소들의 컨테이너                          |
| [insertion](https://www.w3.org/TR/wai-aria-1.2/#insertion)   | 추가되었거나 추가 요청된 컨텐츠를 포함하는 요소              |
| [list](https://www.w3.org/TR/wai-aria-1.2/#list)             | `listitem`을 포함하는 영역                                   |
| [listitem](https://www.w3.org/TR/wai-aria-1.2/#listitem)     | `list`의 각 항목                                             |
| [none](https://www.w3.org/TR/wai-aria-1.2/#none)             | [accessibility API](https://www.w3.org/TR/wai-aria-1.2/#dfn-accessibility-api)에 네이티브 role 시맨틱을 맵핑하지 않게 하는 요소 |
| [note](https://www.w3.org/TR/wai-aria-1.2/#note)             | 메인 컨텐츠의 부속 컨텐츠 영역                               |
| [presentation](https://www.w3.org/TR/wai-aria-1.2/#presentation) | [accessibility API](https://www.w3.org/TR/wai-aria-1.2/#dfn-accessibility-api)에 네이티브 role 시맨틱을 맵핑하지 않게 하는 요소 |
| [row](https://www.w3.org/TR/wai-aria-1.2/#row)               | 테이블 형식 컨테이너의 행(row)                               |
| [rowgroup](https://www.w3.org/TR/wai-aria-1.2/#rowgroup)     | 테이블 형식 컨테이너의 row를 한 개 이상 포함하는 구조        |
| [rowheader](https://www.w3.org/TR/wai-aria-1.2/#rowheader)   | row의 헤더 정보를 포함하는 셀                                |
| [separator](https://www.w3.org/TR/wai-aria-1.2/#separator) (포커스 되지 않을 때) | 섹션의 컨텐츠 혹은 `menuitems` 그룹을 구분하는 요소.         |
| [table](https://www.w3.org/TR/wai-aria-1.2/#table)           | 행과 열로 배치된 데이터를 포함하는 영역                      |
| [toolbar](https://www.w3.org/TR/wai-aria-1.2/#toolbar)       | 자주 쓰이는 기능 버튼 혹은 컨트롤의 모음                     |
| [tooltip](https://www.w3.org/TR/wai-aria-1.2/#tooltip)       | 요소에 대한 설명을 표시하는 팝업                             |

meter, paragraph, math, strong, subscript, superscript, term, time,

&nbsp;  

### 5. 랜드마크 역할 (Landmark roles)

랜드마크는 보조 기기를 사용하는 사용자가 페이지를 더 쉽게 탐색할 수 있도록 페이지의 영역을 의미론적으로 정의하는 역할이다.

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [banner](https://www.w3.org/TR/wai-aria-1.2/#banner)         | 페이지별 컨텐츠가 아닌 사이트 지향(site-oriented) 컨텐츠를 담는 랜드마크. 사이트 지향 컨텐츠로는 로고, 사이트 검색 툴 등 주로 사이트 상단에 위치한 요소들을 말한다. |
| [complementary](https://www.w3.org/TR/wai-aria-1.2/#complementary) | 메인 컨텐츠를 보완하도록 설계된 랜드마크지만, 메인 컨텐츠와 분리되어도 의미를 가질 수 있는 컨텐츠의 영역이다. |
| [contentinfo](https://www.w3.org/TR/wai-aria-1.2/#contentinfo) | 상위 문서에 대한 정보가 들어 있는 랜드마크.                  |
| [form](https://www.w3.org/TR/wai-aria-1.2/#form)             | 양식을 이루는 항목과 객체를 포함하는 랜드마크                |
| [main](https://www.w3.org/TR/wai-aria-1.2/#main)             | 문서의 메인 컨텐츠를 포함하는 랜드마크                       |
| [navigation](https://www.w3.org/TR/wai-aria-1.2/#navigation) | 문서를 탐색하기 위한 navigational 요소(ex. 링크)를 모아놓은 랜드마크 |
| [region](https://www.w3.org/TR/wai-aria-1.2/#region)         | 컨텐츠가 충분히 중요하여 사용자가 쉽게 탐색할 수 있고, 페이지 요약에 나열되어 있을만한 영역. |
| [search](https://www.w3.org/TR/wai-aria-1.2/#search)         | 검색 영역을 이루는 항목과 객체를 포함하는 랜드마크.          |

&nbsp;  

### 6. 실시간 영역 역할 (Live Region roles)

아래는 실시간 영역을 나타내는 역할 목록이다. 실시간 영역은 실시간 영역 속성([live region attributes](https://www.w3.org/TR/wai-aria-1.2/#attrs_liveregions))에 의해 변경될 수 있다.

| 역할                                                   | 요약                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| [alert](https://www.w3.org/TR/wai-aria-1.2/#alert)     | 중요한(또한 time-sensitive한) 정보를 담는 실시간 영역.       |
| [log](https://www.w3.org/TR/wai-aria-1.2/#log)         | 순서에 의미가 있는 새로운 정보가 추가되는 실시간 영역. 또한 오래된 정보가 사라질 수 있는 실시간 영역 |
| [marquee](https://www.w3.org/TR/wai-aria-1.2/#marquee) | 중요하지 않은 정보가 자주 변경되는 실시간 영역               |
| [status](https://www.w3.org/TR/wai-aria-1.2/#status)   | 사용자에게 도움을 줄 수 있는(advisory) 정보를 담는 실시간 영역. 하지만 제공되는 정보가 `alert`로 분류될 만큼 중요하지 않을 때 사용. |
| [timer](https://www.w3.org/TR/wai-aria-1.2/#timer)     | 실행 시점으로부터 혹은 종료 시점까지 흐른/남은 시간을 나타내는 실시간 영역. |

&nbsp;  

### 7. 창 역할 (Window roles)

아래 역할은 브라우저 혹은 어플리케이션 안의 창(window)으로 동작하는 요소이다.

| 역할                                                         | 요약                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [alertdialog](https://www.w3.org/TR/wai-aria-1.2/#alertdialog) | 알림 메시지를 포함하는 `dialog`. 최초 포커스는 `dialog` 안의 요소에 맞춰진다. |
| [dialog](https://www.w3.org/TR/wai-aria-1.2/#dialog)         | 웹 어플리케이션 메인 창의 하위 창. HTML 페이지에서 어플리케이션의 메인 창은 웹 문서 전체를 말한다(ex. `body` 요소) |



## 관련 링크

* [Using ARIA: Roles, states, and properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)
* [WAI-ARIA Authoring Practices 1.2](https://www.w3.org/TR/wai-aria-practices-1.2)
* [WAI-ARIA 1.2](https://www.w3.org/TR/wai-aria-1.2)

