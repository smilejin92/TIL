# CSS 속성

HTML 요소의 스타일을 지정하는 CSS 속성의 종류는 크게 두 가지로 나뉜다.

1. 상속이 되는 속성
2. 상속되지 않는 속성

&nbsp;  

## 1. 상속되는 속성

### 폰트 속성
| 속성                                                         | 기본 속성 값       | 요약                                                         |
| ------------------------------------------------------------ | ------------------ | ------------------------------------------------------------ |
| font-family                                                  | 사용자 환경에 따름 | 텍스트의 폰트를 지정                                         |
| font-weight                                                  | normal             | 폰트가 표시되는 굵기를 지정                                  |
| font-style                                                   | normal             | 폰트의 표시 형태를 지정                                      |
| font-size                                                    | medium             | 폰트의 크기를 지정                                           |
| [@font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face) | 사용자 지정 | font-family의 이름과 자원을 정의할 수 있는 규칙              |

&nbsp;  

### 텍스트 속성


| 속성                                                         | 기본 속성 값       | 요약                                                         |
| ------------------------------------------------------------ | ------------------ | ------------------------------------------------------------ |
| text-transform                                               | none               | 텍스트의 대소 문자를 변환하기 위한 속성                      |
| [white-space](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space) | CSS2 - normal &nbsp;  CSS3 - 없음 | 텍스트의 공백과 줄바꿈의 처리 방법을 지정                    |
| tab-size                                                     | 8                  | 탭 크기를 지정                                               |
| line-break                                                   | auto               | 요소 내 줄바꿈 규칙을 지정                                   |
| word-break                                                   | normal             | 줄바꿈을 위한 단어 규칙을 지정                               |
| overflow-wrap                                                | normal             | 단어가 요소 박스의 너비보다 길어질 경우 자동 줄바꿈이 발생하는데, 이때 단어를 나눌지 여부를 지정 |
| [text-align](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align) | start              | 단락 내 텍스트의 가로 방향 정렬 방법을 지정                  |
| text-indent                                                  | 0                  | 단락의 첫 줄 들여쓰기를 지정                                 |
| text-decoration                                              | 없음 | 텍스트를 장식하는 속성으로, CSS3에서 세분화된 하위 속성이 추가됨 |
| text-shadow                                                  | 없음 | 텍스트에 그림자를 지정                                       |
&nbsp;  

### 가시 속성

| 속성 | 기본 속성 값 | 요약 |
| ---- | ------------ | ---- |
|   visibility   |     visible         |    HTML 요소에 의해 만들어진 박스의 화면상 표시 여부를 지정  |
| color | 사용자 에이전트에 따름 | 요소의 전경색을 지정 |
| opacity | 1 | 요소 박스의 투명도를 지정 |

&nbsp;  

## 2. 상속되지 않는 속성

### 레이아웃 속성

| 속성                                                         | 기본 속성 값 | 요약                                                         |
| ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| [display](https://developer.mozilla.org/en-US/docs/Web/CSS/display) | inline       | HTML 요소의 표현 방식을 지정                                 |
| [position](https://developer.mozilla.org/en-US/docs/Web/CSS/position) | static       | 요소 박스의 배치 방식을 지정                                 |
| top                                                          | auto         | position 속성 값이 static이 아닌 경우, 해당 요소의 Y좌표를 지정할 때 사용할 수 있는 속성((X, 0) 기준) |
| left                                                         | auto         | position 속성 값이 static이 아닌 경우, 해당 요소의 X좌표를 지정할 때 사용할 수 있는 속성((0, Y) 기준) |
| bottom                                                       | auto         | position 속성 값이 static이 아닌 경우, 해당 요소의 Y좌표를 지정할 때 사용할 수 있는 속성((X, MAX_Y) 기준) |
| right                                                        | auto         | position 속성 값이 static이 아닌 경우, 해당 요소의 X좌표를 지정할 때 사용할 수 있는 속성((MAX_X, Y) 기준) |
| [z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) | auto         | position 속성 값이 static이 아닌 요소들의 영역이 겹쳤을 경우, 겹치는 순서를 지정하는 속성 |
| [float](https://developer.mozilla.org/en-US/docs/Web/CSS/float) | none         | 일반적인 흐름에서 분리된 요소를 부모 영역을 기준으로 배치하는 속성 |
| [clear](https://developer.mozilla.org/en-US/docs/Web/CSS/clear) | none         | float 속성의 선언으로 요소의 배치 위치에 영향을 받게 된 경우, 이를 해제하고자 할 때 사용하는 속성 |

&nbsp;  

### 여백 속성

| 속성                                                         | 기본 속성 값   | 요약                                                         |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ |
| [padding](https://developer.mozilla.org/en-US/docs/Web/CSS/padding) | 세부 속성 참조 | content 영역과 border 사이의 안쪽 여백을 지정                |
| border                                                       | 세부 속성 참조 | 요소 박스의 테두리를 지정                                    |
| margin                                                       | 세부 속성 참조 | border를 기준으로 다른 요소와의 바깥쪽 여백을 지정. 속성 값으로 음수를 사용할 수 있으며, 상하로 인접한 박스의 display 속성 값이 block인 경우, **마진 겹침(Margin Collapsing)** 현상이 발생함 |

&nbsp;  

### 사이즈 속성

| 속성       | 기본 속성 값 | 요약                                    |
| ---------- | ------------ | --------------------------------------- |
| width      | auto         | 요소의 너비를 지정                      |
| height     | auto         | 요소의 높이를 지정                      |
| min-width  | 0            | 요소의 최소 너비를 지정                 |
| min-height | 0            | 요소의 최소 높이를 지정                 |
| max-width  | 0            | 요소의 최대 너비를 지정                 |
| max-height | 0            | 요소의 최대 높이를 지정                 |
| box-sizing | content-box  | 요소 박스의 크기를 결정하는 방식을 지정 |

&nbsp;  

### 배경 속성

| 속성                  | 기본 속성 값                                                 | 요약                                                         |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| background-color      | transparent                                                  | 요소의 배경색을 지정                                         |
| background-image      | 없음                                                         | 요소 박스의 배경 이미지를 지정. CSS3에서는 하나의 요소 박스에 여래 개의 배경 이미지를 지정할 수 있으며, [그라디언트(gradient)](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient) 값을 지정할 수 있음. |
| background-repeat     | repeat                                                       | 배경 이미지의 반복 여부를 지정                               |
| background-attachment | scroll                                                       | 배경 이미지의 고정 여부를 지정                               |
| background-position   | 0 0                                                          | 배경 이미지의 위치를 지정 (X, Y)                             |
| background-clip       | [border-box]((https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip)) | 배경 속성이 적용되는 영역을 지정                             |
| background-origin     | border-box                                                   | 배경 이미지의 시작점을 지정                                  |
| background-size       | auto                                                         | 배경 이미지의 크기를 지정                                    |
| background            | 세부 속성 참조                                               | 배경 관련 속성을 일괄적으로 지정                             |

&nbsp;  

### 테두리 속성

| 속성          | 기본 속성 값   | 요약                                                 |
| ------------- | -------------- | ---------------------------------------------------- |
| border-color  | currentcolor   | 요소 박스의 테두리 선 색상을 지정                    |
| border-style  | none           | 요소 박스 테두리의 선 스타일을 지정                  |
| border-width  | none           | 요소 박스 테두리의 선 굵기를 지정                    |
| border-radius | 세부 속성 참조 | 요소 박스의 테두리 선을 둥근 모서리 형태로 지정      |
| border        | 개별 속성 참조 | 테두리 선 속성을 일괄적으로 지정할 수 있는 단축 속성 |



### 테이블 속성

| 속성         | 기본 속성 값   | 요약                                          |
| ------------ | -------------- | --------------------------------------------- |
| column-width | auto           | 테이블 구성 시 열의 너비를 지정               |
| column-count | auto           | 테이블 구성 시 열의 개수를 지정               |
| columns      | 개별 속성 참조 | 열의 너비와 개수를 일괄 지정하는 단축 속성    |
| column-span  | none           | 테이블 구성 시 여러 열을 차지하는 요소를 지정 |

&nbsp;  

### animation 속성

| 속성 | 기본 속성 값 | 요약 |
| ---- | ------------ | ---- |
| @keyframes                | 사용자 정의                                                  | animation 속성에 적용할 키프레임을 생성하기 위한 규칙        |
| animation-name            | none                                                         | @keyframes 규칙으로 생성한 애니메이션 이름을 지정하여 해당 애니메이션이 실행되도록 하는 속성 |
| animation-duration        | 0s                                                           | animation-name 속성으로, 실행된 애니메이션 진행 시간을 지정  |
| animation-timing-function | ease                                                         | 애니메이션 진행속도의 변화 형태를 지정하는 속성. transition-timing-function 속성 값과 동일하다. |
| animation-iteration-count | 1 | 애니메이션의 반복 횟수를 지정 |
| animation-direction | normal | 애니메이션의 진행 방향을 지정 |
| animation-play-state | running | 애니메이션의 진행 및 정지 상태를 지정 |
| animation-delay | 0s | 애니메이션이 실행되기 전 지연 시간을 초 단위(s)로 지정 |
| animation-fill-mode | none | 애니메이션 실행 이전이나 이후에 애니메이션 효과를 표시할지의 여부를 지정하는 속성 |
| animation | 개별 속성 값 참조 | 애니메이션과 관련된 속성 값들을 일괄 지정하기 위한 대표 속성 |

&nbsp;  

### transition 속성

| 속성 | 기본 속성 값 | 요약 |
| ---- | ------------ | ---- |
| transition-property                                          | all                                                          | 요소에 지정된 속성을 변환하고자 할 때 사용                   |
| transition-duration                                          | 0s                                                           | 변환이 진행되는 시간을 지정                                  |
| transition-timing-function                                   | ease                                                         | 속성이 변환될 때 진행 속도의 형태를 지정                     |
| transition-delay                                             | 0s                                                           | 변환이 진행되기 전 지연되는 시간을 지정                      |
| transition                                                   | 개별 속성 값 참조                                            | transition 관련 속성 값들을 일괄 적용하는 대표 속성          |

&nbsp;  

### flex 속성

| 속성            | 기본 속성 값   | 요약                                                         |
| --------------- | -------------- | ------------------------------------------------------------ |
| flex-direction  | row            | 요소 박스의 배치 방향을 지정                                 |
| flex-wrap       | nowrap         | flex item이 한 줄 또는 여러 줄로 배치될 것인지를 지정        |
| flex-flow       | 세부 속성 참조 | flex-direction 속성과 flex-flow 속성을 일괄적으로 지정할 수 있는 대표 속성 |
| order           | 0              | 요소 박스의 배치 순서를 지정                                 |
| flex-grow       | 0              | flex item 크기를 조정하는 속성. flex container 크기에 대해 flex item에 확대 비율을 지정함 |
| flex-shrink     | 1              | flex item 크기를 조정하는 속성. flex container 크기에 대해 flex item에 축소 비율을 지정함 |
| flex-basis      | auto           | flex item의 기준 크기를 지정하는 속성. width 속성의 값으로 올 수 있는 값과 동일함 |
| flex            | 세부 속성 참조 | flex-grow, flex-shrink, flex-basis 속성을 일괄적으로 지정할 수 있는 대표 속성 |
| justify-content | flex-start     | flex item의 메인 축 정렬 방식을 지정하기 위한 속성. 정렬 방식에 따라 flex-item의 start 영역과 end 영역이 결정된다. |
| align-items     | stretch        | flex item의 교차 축(cross axis) 정렬 방식을 지정하기 위한 속성. |
| align-self      | auto           | 특정 flex-item의 배치 속성을 교차 축(cross-axis)에 대하여 지정. align-items 속성을 override 함. |

&nbsp;  

### 기타 속성

| 속성                                                         | 기본 속성 값 | 요약                                                         |
| ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| [overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow) | visible      | 컨텐츠가 요소의 영역을 벗어나는 경우의 처리 방법을 지정      |
| text-overflow                                                | clip         | 요서 박스의 너비가 고정되어 있고, 요소 박스 내 텍스트의 박스의 크기를 넘는 경우 overflow된 텍스트를 처리하는 속성. |
| [clip](https://developer.mozilla.org/en-US/docs/Web/CSS/clip) | auto         | 요소 박스의 특정 영역만 나타나도록 지정                      |
| [transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform) | none         | 요소 박스를 변형하는 속성으로, 2차원 3차원 변형이 가능하며, 변형 형태별로 함[수 타입의 속성 값](https://developer.mozilla.org/en-US/docs/Web/CSS/transform#Values)을 가짐. 이때 속성 값은 공백으로 구분하여 여러 개의 속성 값을 가질 수 있음. |
| box-shadow                                                   | none         | 요소 박스의 그림자를 지정                                    |
| content                                                      | none         | 가상 요소인 :before 혹은 :after의 컨텐트를 지정하는 속성     |
| outline                                                      | mendium      | outline-width, outline-style, outline-color 속성을 일괄적으로 지정하는 단축 속성. border 속성과는 별개로 요소의 외곽선을 표시 |
| outline-offset                                               | 0            | 요소의 바깥쪽 영역과 외곽선 사이의 간격을 지정하는 속성.     |
| cursor                                                       | auto         | HTML 요소 위에 마우스가 오버될 때 마우스 포인터의 모양을 지정 |

&nbsp;  

## 참고 자료

* [CSS3](https://github.com/seulbinim/PDF/blob/master/HTML5.pdf)

