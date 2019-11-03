# 자바스크립트 개발 환경과 실행 방법

## 1. 자바스크립트 실행 환경

* 모든 브라우저 및 Node.js 환경에서 실행 가능
* 단, 브라우저와 Node.js는 용도가 다름 (Client-side API vs. Host API)



## 2.웹 브라우저

### 2.1. 웹 브라우저는 어떻게 동작하는가?

* 사용자 (client)가 참조하고자 하는 웹 페이지를 서버 (server)에 요청 (request)하고 서버의 응답 (response)을 받아 (download files like html, css, js - **loading)** 브라우저에 표시함 (through HTTP)

  * HTTP/1.1 - 파일을 하나씩 로드
  * HTTP/2.0 - 파일을 한꺼번에 로드

* HTML, CSS 파일은 **렌더링 엔진**의 HTML 파서와 CSS 파서에 의해 파싱 (parsing)되어 DOM, CSSOM 트리로 변환되고 렌더 트리로 결합됨

  <img src="./images/render-tree-construction.png" style="zoom:50%;" />

* 자바스크립트는 렌더링 엔진이 아닌 **자바스크립트 엔진**이 처리함. 위의 DOM 트리 생성 과정에서, HTML 파서는 script 태그를 만나면 자바스크립트 코드를 실행하기 위해 DOM 생성 프로세스를 중지하고 자바스크립트 엔진으로 제어 권한을 넘김

* 이후 자바스크립트 엔진은 소스 코드를 해석하여 문법적 의미와 구조를 갖는 AST (Abstract Syntax Tree - Syntax Analysis)를 생성.

  * Tokenizing (ex. const, foo, = , 10)
  * Parsing
  * execute

* 다시 HTML 파서로 권한을 넘긴 후 남은 DOM 생성을 재개

* 따라서, 스크립트를 head 영역에 추가하면 DOM 트리 생성이 완료되기전에 실행되기 때문에 body 가장 밑에 추가하는 경우가 바람직하다. 하지만, html 5에서 script 태그에 async / defer 속성을 추가하여 스크립트 실행 시기를 조정할 수 있다.



### 2.2. 개발자 도구 (크롬)

* 패널

  * Elements - 로딩된 웹 페이지의 DOM과 CSS를 편집하여 렌더링된 뷰를 확일할 수 있음.
  * Console - 로딩된 웹 페이지의 에러를 확인하거나 자바스크립트 소스코드에 포함시킨 console.log 메소드의 결과를 확인해 볼 수 있음.
  * **Sources** - 로딩된 웹 페이지의 자바스크립트 코드를 디버깅할 수 있음
  * Network - 로딩된 웹 페이지에 관련한 네트워크 요청 (request) 정보와 퍼포먼스를 확인할 수 있다.
  * Application - 웹 스토리지, 세션, 쿠키를 확인하고 관리할 수 있다.

  

## 3. Node.js

* 프로젝트 규모가 커짐에 따라 외부 라이브러리 (ex. React, jQuery)를 도입하거나 여러 가지 도구 (Babel, Webpack, ESLint)를 사용해야할 필요가 있다. 이때 Node.js와 npm이 필요하다.
* 2009년 **라이언 달 (Ryan Dahl)**이 크롬 V8 자바스크립트 엔진으로 빌드한 런타임 환경 (Runtime Environmnet)
* 브라우저 이외의 환경에서 자바스크립트를 동작시킬 수 있음
* 주로 서버 사이드 애플리케이션 개발에 사용되며, 이에 필요한 모듈, 파일 시스템, HTTP 등 빌트인 API를 제공
* SPA에 적합

### 3.1. npm

* node package manager. 자비스크립트 패키지 매니저

* Node.js에서 사용할 수 있는 모듈을 패키지화하여 모아둔 저장소

* 패키지 설치 및 관리를 위한 CLI 제공

