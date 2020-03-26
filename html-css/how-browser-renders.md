# 브라우저의 동작 원리

## 서버에 요청

## DOM

1. 브라우저는 html, body, div 등 html 요소를 만나면 자바스크립트 객체(Node)로 변환 / 생성한다.
2. 1에서 생성한 Node를 트리 구조로 관리하여 Node 사이의 관계를 표시한다 (DOM Tree). 

## CSSOM

1. DOM Tree 생성 후 브라우저는 외부, 내장, 인라인, user-agent 등 모든 css 속성을 읽어들인다.
2. 사용자가 지정한 스타일 정보를 user agent 스타일에 덮어 씌운다. 이때 css 선택자 우선 순위가 결정된다.
3. 사용자 지정 혹은 user-agent 스타일에서 다루지 않은 HTML 요소들에 대해서는 W3C CSS 스탠다드 기본 스타일이 적용된다. (이때 사용되는 기본 CSS 속성 값 중 **상속이 되는 스타일은 하위 요소에게 상속되어진다.** 예를 들어 특정 html 요소의 color와 font-size 속성이 지정되지 않았다면 부모 요소로부터 상속 받는다.)
4. CSS Object Model을 생성한다. (DOM tree와 비슷한 tree 구조)
5. 트리의 각 node는 특정 DOM 요소의 스타일 정보를 가지고 있다 (눈에 보이는 DOM에 대해서만)
6. 상속될 속성이 상속되고, style이 compute된다.

## Render Tree

1. DOM 트리와 CSSOM 트리가 결합되어 만들어진다.
2. 브라우저는 눈에 보이는 요소의 레이아웃을 계산하여 해당 요소를 그려내기 위해 render 트리를 사용한다. (렌더 트리가 형성되지 않으면 페인팅도 할 수 없다)
3. 렌더트리는 화면에 그려질 요소에 대한 정보만 담기 때문에 pixel matrix에 영역을 차지하지 않는 node에 대한 정보를 가지고 있지 않다 (ex. head 요소, display: none). display: none 요소는 렌더트리에 존재하지 않고, visibility: none 혹은 opacity: 0 요소는 렌더트리에 존재한다.

## Rendering 과정

렌더트리까지 형성되면 각 요소를 화면에 출력하기 시작한다.

### 1. Layout operation

브라우저는 렌더트리의 각 노드의 레이아웃을 생성한다. 레이아웃은 각 노드의 사이즈(px 단위로)와 출력될 위치(position)로 구성돼있다. 이 과정을 다른 말로는 reflow 혹은 browser reflow라고 한다. 스크롤, 윈도우 사이즈 조정, DOM 노드를 조작할 때마다 발생한다.

### 2. Paint operation

렌더 트리의 각 요소들은 서로를 overlap하거나, 자신의 모습과 위치를 자주 변하게 하는 속성을 가지고 있을 수 있기 때문에 브라우저는 각 요소에 대해 layer를 생성한다.

