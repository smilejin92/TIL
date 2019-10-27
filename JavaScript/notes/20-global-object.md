# 전역 객체

전역 객체(Global Object)는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체이다. 전역 객체는 클라이언트 사이드 환경(브라우저)에서는 `window`, 서버 사이드 환경(Node.js)에서는 `global` 객체를 의미한다.

**전역 객체의 프로퍼티**

* 표준 빌트인 객체(Object, String, Number, Function 등)
* **호스트 객체**(클라이언트 Web API, Node.js의 호스트 API)
* `var` 키워드로 선언한 전역 변수와 전역 함수



**전역 객체의 특징**

* 개발자가 의도적으로 생성할 수 없다.
* 전역 객체의 프로퍼티를 참조할 때 `window`를 생략할 수 있다.
* 모든 표준 빌트인 객체(Object, String, Number 등)를 **프로퍼티**로 갖고 있다.
* 자바스크립트 실행 환경 (브라우저, Node.js)에 따라 추가적으로 프로퍼티와 메소드를 갖는다.
* `var` 키워드로 선언한 전역 변수와 선언하지 않은 변수에 값을 할당한 암묵적 전역 변수, 그리고 전역 함수를 프로퍼티로 가진다.
