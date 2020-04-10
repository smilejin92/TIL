# ARIA는 무엇인가?

**Accessible Rich Internet Applications (ARIA)** 는 장애를 가진 사용자가 웹 컨텐츠와 웹 어플리케이션(특히 자바스크립트를 사용하여 만든)에 더 쉽게 접근할 수 있는 방법을 정의하는 여러 특성을 말한다.

ARIA는 어플리케이션에서 사용되는 상호작용 및 위젯에 대한 정보를 보조 기술(ex. 스크린 리더, 보이스 오버)에 전달하여 HTML을 보강한다. ARIA를 사용하여 HTML4에서의 접근 가능한 내비게이션 랜드마크, 자바스크립트 위젯, 양식 힌트, 에러 메시지, 실시간 컨텐츠 업데이트 등을 접근 가능한 형태로 제공할 수 있다.

>  **주의**
>
> 아래 등장하는 대부분의 위젯들은 HTML5에 통합되었으며, 개발자는 ARIA 대신 사용 목적에 적합한 HTML 시맨틱 요소를 사용하는 것이 바람직하다. 예를 들어, 각 HTML 네이티브 요소는 고유의 역할과 상태, 키보드 접근성을 가지고 있다. 만약 사용 목적에 적합한 시맨틱 요소를 찾지 못한다면, 그때 ARIA를 사용해도 늦지 않다.

&nbsp;  

아래 코드는 프로그래스바 위젯의 마크업이다.

```html
<div id="percent-loaded" role="progressbar" aria-valuenow="75"
     aria-valuemin="0" aria-valuemax="100">
</div>
```

위의 프로그래스바는 `<div>` 요소로 만들어졌으므로 아무런 의미를 가지지 않는다. 안타깝게도, HTML4 환경에서는 프로그래스바를 대체할 시맨틱 요소가 존재하지 않는다. 따라서 ARIA 역할과 속성을 추가하여 프로그래스바에 의미를 부여할 수 있다. 위의 예제에서, `role="progressbar"` 속성은 브라우저에게 해당 요소가 자바스크립트로 구동되는 프로그래스바 위젯이란 것을 알려준다. 또한 `aria-valuemin`, `aria-valuemax` 속성은 각각 프로그래스바의 최소 진행률과 최대 진행률을 나타내며, `aria-valuenow` 속성은 현재 진행률을 나타낸다. 따라서 `aria-valuenow` 속성의 경우 자바스크립트를 통해 동적으로 값을 갱신해주어야 한다.

ARIA 속성을 HTML 마크업에 직접적으로 명시하여 사용할 수도 있지만, 자바스크립트를 통해 ARIA 속성을 추가하여 사용하는 방법도 있다. 위의 프로그래스 바 예제를 자바스크립트 코드로 치환하면 아래와 같다.

```javascript
// 프로그래스 바 탐색
var progressBar = document.getElementById("percent-loaded");

// ARIA 역할 및 상태 부여
progressBar.setAttribute("role", "progressbar");
progressBar.setAttribute("aria-valuemin", 0);
progressBar.setAttribute("aria-valuemax", 100);

// 진행률 업데이트 함수
function updateProgress(percentComplete) {
  progressBar.setAttribute("aria-valuenow", percentComplete);
}
```

> ARIA는 HTML4 이후에 개발되었으므로, ARIA 사용은 HTML4와 XHTML에서 유효성 검사를 통과하지 못한다. 하지만 ARIA를 사용함으로써 얻는 접근성 향상이 이런 사소한(?) 문제보다는 더 가치가 있다.
>
> HTML5에서는 모든 ARIA 속성이 유효하다. 새롭게 등장한 랜드마크 요소(`<main>`, `<header>`, `<nav>` 등)는 고유의 ARIA 역할이 내장되어 있으므로, 굳이 ARIA 역할을 중복해서 사용할 필요가 없다.

&nbsp;   

## 참고 자료

* [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)

