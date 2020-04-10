# ARIA 사용

본 포스트는[ Accessible Rich Internet Applications (WAI-ARIA) 1.2](https://www.w3.org/TR/wai-aria-1.2/) 명세를 바탕으로 작성된 **HTML 요소에 접근성 정보를 추가하는 방법에 대한 가이드라인**이다. 접근성 정보를 추가하여 장애를 가진 사용자가 웹 컨텐츠와 웹 어플리케이션에 더 쉽게 접근할 수 있게 할 수 있다. 아래는 HTML5에서의 WAI-ARIA 사용 방법이 서술되어 있다. 이러한 방법은 특히 Ajax, HTML, JavaScript 및 관련 기술로 구현된 동적인 UI 제어에 도움이 된다.

## ARIA 사용 규칙

### 1. ARIA 사용의 첫 번째 규칙

만약 사용 목적에 맞는 HTML 요소 혹은 속성이 **이미 존재한다면**, **그대로 사용한다.**

**이 규칙이 적용되지 않는 경우는?**

* 사용하고자 하는 기능이 [HTML](https://html.spec.whatwg.org/multipage/)에 존재하지만, 구현되지 않은 경우
* 사용하고자 하는 기능이 HTML에 존재하고, 구현되었지만 [접근성 지원](https://www.html5accessibility.com/)이 안되는 경우
* 

