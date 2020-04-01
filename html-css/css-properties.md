# CSS 속성

HTML 요소의 스타일을 지정하는 CSS 속성의 종류는 크게 두 가지로 나뉜다.

1. 상속이 되는 속성
2. 상속되지 않는 속성

&nbsp;  

## 상속되는 속성

<div class="properties">

| 속성                                                         | 기본 속성 값       | 요약                                                         |
| ------------------------------------------------------------ | ------------------ | ------------------------------------------------------------ |
| font-family                                                  | 사용자 환경에 따름 | 텍스트의 폰트를 지정                                         |
| font-weight                                                  | normal             | 폰트가 표시되는 굵기를 지정                                  |
| font-style                                                   | normal             | 폰트의 표시 형태를 지정                                      |
| font-size                                                    | medium             | 폰트의 크기를 지정                                           |
| [@font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face) | 사용자 지정 | font-family의 이름과 자원을 정의할 수 있는 규칙              |
| text-transform                                               | none               | 텍스트의 대소 문자를 변환하기 위한 속성                      |
| [white-space](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space) |                    | 텍스트의 공백과 줄바꿈의 처리 방법을 지정                    |
| tab-size                                                     | 8                  | 탭 크기를 지정                                               |
| line-break                                                   | auto               | 요소 내 줄바꿈 규칙을 지정                                   |
| word-break                                                   | normal             | 줄바꿈을 위한 단어 규칙을 지정                               |
| overflow-wrap                                                | normal             | 단어가 요소 박스의 너비보다 길어질 경우 자동 줄바꿈이 발생하는데, 이때 단어를 나눌지 여부를 지정 |
| [text-align](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align) | start              | 단락 내 텍스트의 가로 방향 정렬 방법을 지정                  |
| text-indent                                                  | 0                  | 단락의 첫 줄 들여쓰기를 지정                                 |
| text-decoration                                              |                    | 텍스트를 장식하는 속성으로, CSS3에서 세분화된 하위 속성이 추가됨 |
| text-shadow                                                  |                    | 텍스트에 그림자를 지정                                       |
| visibility | visible | HTML 요소에 의해 만들어진 박스의 화면상 표시 여부를 지정 |
| color | 사용자 에이전트에 따름 | 요소의 전경색을 지정 |
| opacity | 1 | 요소 박스의 투명도를 지정 |
|  | |  |
|  | |  |
|  | |  |
|  | |  |
|  | |  |
|  | |  |

</div>

&nbsp;  

## 상속되지 않는 속성

| 속성                                                         | 기본 속성 값   | 요약                                                         |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ |
| [display](https://developer.mozilla.org/en-US/docs/Web/CSS/display) | inline         | HTML 요소의 표현 방식을 지정                                 |
| padding                                                      |                | content 영역과 border 사이의 안쪽 여백을 지정                |
| border                                                       |                | 요소 박스의 테두리를 지정                                    |
| [margin](https://developer.mozilla.org/en-US/docs/Web/CSS/margin) |                | border를 기준으로 다른 요소와의 바깥쪽 여백을 지정. 속성 값으로 음수를 사용할 수 있으며, 상하로 인접한 박스의 display 속성 값이 block인 경우, 마진 겹침(Margin Collapsing) 현상이 발생함 |
| width                                                        | auto           | 요소의 너비를 지정                                           |
| height                                                       | auto           | 요소의 높이를 지정                                           |
| min-width                                                    | 0              | 요소의 최소 너비를 지정                                      |
| min-height                                                   | 0              | 요소의 최소 높이를 지정                                      |
| max-width                                                    | 0              | 요소의 최대 너비를 지정                                      |
| max-height                                                   | 0              | 요소의 최대 높이를 지정                                      |
| [overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow) | visible        | 컨텐츠가 요소의 영역을 벗어나는 경우의 처리 방법을 지정      |
| background-color                                             | transparent    | 요소의 배경색을 지정                                         |
| background-image                                             |                | 요소 박스의 배경 이미지를 지정. CSS3에서는 하나의 요소 박스에 여래 개의 배경 이미지를 지정할 수 있으며, 그라디언트(gradient) 효과를 지정할 수 있음. 속성 값은 아래 gradient 테이블을 참고. |
| background-repeat                                            | repeat         | 배경 이미지의 반복 여부를 지정                               |
| background-attachment                                        | scroll         | 배경 이미지의 고정 여부를 지정                               |
| background-position                                          | 0 0            | 배경 이미지의 위치를 지정                                    |
| background-clip                                              | border-box     | 배경 속성이 적용되는 영역을 지정                             |
| background-origin                                            | border-box     | 배경 이미지의 시작점을 지정                                  |
| background-size                                              | auto           | 배경 이미지의 크기를 지정                                    |
| background                                                   | 세부 속성 참조 | 배경 관련 속성을 일괄적으로 지정                             |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |
|                                                              |                |                                                              |

&nbsp;  

## bakground-image: gradient

| 속성 값                                                      | 요약                                             |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [linear-gradient(angle, color-stop)](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient) | 선형 그라디언트 효과를 지정                      |
| [radial-gradient(shape, size, position, color-stop)](https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient) | 원형 그라디언트 효과를 지정                      |
| [repeating-linear-gradient(angle, color-stop)](https://developer.mozilla.org/en-US/docs/Web/CSS/repeating-linear-gradient) | 색상 변환이 반복되는 선형 그라디언트 효과를 지정 |
| [repeating-radial-gradient(shape, size, position, color-stop)](https://developer.mozilla.org/en-US/docs/Web/CSS/repeating-radial-gradient) | 색상 변환이 반복되는 원형 그라디언트 효과를 지정 |

