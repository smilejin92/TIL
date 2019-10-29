# 문서 객체 모델 (Document Object Model)

## 1. DOM (Document Object Model)

HTML 문법은 중첩 관계를 표현할 수 있다.



## 2. DOM tree

브라우저가 HTML 문서를 로드한 후 파싱하여 생성하는 모델을 의미한다. 객체의 트리로 구조화되어 있기 때문에 DOM tree라 부른다. DOM tree는 CSSOM tree와 함께 Render tree를 만든다.

어트리뷰트와 DOM 요소의 프로퍼티는 1:1 매칭되지 않는다. (1:1인 것도 있고)



## 3. DOM Query / Traversing (요소에의 접근)

### 3.1 하나의 요소 노드 선택(DOM Query)

### 3.2 여러 개의 요소 노드 선택(DOM Query)

### 3.3 DOM Traversing (탐색)

parentNode vs. parentElement (공백까지 다 잡힌다)



## 4. DOM Manipulation (조작)

### 4.1 텍스트 노드에의 접근/수정

### 4.2 어트리뷰트 노드에의 접근/수정

어트리뷰트 객체 안의 기본 값들은 변경되지 않음 (억지로 하지 않는 이상)

value vs. attribute.value

### 4.3 HTML 콘텐츠 조작(Manipulation)

### 4.4 DOM 조작 방식

### 4.5 insertAdjacentHTML()

### 4.6 innerHTML vs. DOM 조작 방식 vs. insertAdjacentHTML()



## 5. sytle



