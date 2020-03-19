# Introduction to HTML5

**인터넷**: 전세계를 연결하고 있는 국제 정보통신망
**www (World Wide Web)**: 인터넷에 연결된 컴퓨터를 통해 사람들이 정보를 공유할 수 있는 정보공간

## 인터넷의 시작

* 미국 국방성에서 시작
* ARPA (Advanced Research Projects Agency) 창설
* 1969년 현재 웹의 모태가 되는 ARPNET 개발
* 현재 우리가 웹 브라우저로 보고 있는 웹을 **팀 버너스리**가 개발

## 웹의 역사

### 제 1차 웹 브라우저 전쟁

* 1993년 미국 일리노이 공과대학의 연구기관 NCSA에서 최초의 GUI 웹 브라우저인 **모자이크** 발표
* 모자이크 핵심 개발자 **마크 안데르센**은 이후 **넷스케이프 커뮤니케이션** 설립, 넷스케이프 네비게이터 발표
* 하지만 Microsoft의 **인터넷 익스플로러(IE)**의 점유율을 따라잡지 못한 채 붕괴

<img src="https://user-images.githubusercontent.com/32444914/77056133-6041bd80-6a15-11ea-881e-9a10f0daa6be.png" style="zoom:50%; text-align: center;" />

### 플러그인

* 웹 표준을 지정하는 **W3C**는 빠른 속도로 발전하는 웹에 대응하지 못함
* 이에 불만을 느끼던 웹 브라우저 벤더들은 **플러그인**을 개발

**플러그인**: 웹 브라우저와 연동되는 특정 프로그램을 사용자 PC에 추가로 설치하여 웹 브라우저의 기능을 확장하는 방법 (ex. ActiveX, Adobe Flash)

### 웹 2.0의 시대

* 사용자가 함께 새로운 컨텐츠를 창조하는 시대 (ex. Youtube, Wikipedia)
* 2000년대 초반 ActiveX를 기반으로 기업의 **Web Application** 제작
* Flash를 기반으로 애니메이션 제작 (ex. 졸라맨)

<img src="https://user-images.githubusercontent.com/32444914/77057125-d1ce3b80-6a16-11ea-8668-6993035babfa.jpg" style="zoom:75%; text-align: center;" />

### WHATWG

* 인터넷 익스플로러(IE)는 W3C의 표준 웹 브라우저가 됨
* 모든 웹 사이트에 플러그인이 들어가면서 웹 사이트들이 무거워짐
* 이에 IE를 제외한 웹 브라우저 제공 기업들은(ex. Apple, Mozilla, Opera) 새로운 웹 표준 기관 **WHATWG**를 설립, 새로운 웹 표준으로 **Web Application 1.0**을 작성
* 이후 W3C는 Web Application 1.0을 HTML5 표준으로 변경, WHATWG와 **HTML W/G** 결성

> **WHATWG**
>
> Web Hypertext Application Technology Working Group의 줄임말
>
> **HTML W/G**
>
> HTML Working Group의 줄임말

### 제 2차 웹 브라우저 전쟁

* 2010년 전후로 Microsoft와 W3C가 함께 작성한 웹 표준 XHTML 2.0이 붕괴
* 다른 웹 브라우저는 모두 최신 표준을 지원하는데, IE는 지원하지 못하는 역현상 발생
* Mozilla, Chrome, Opera 등 모든 웹 브라우저가 빠른 속도로 업데이트 (2019년 기준 Chrome 승)
* 2016년 1월, Microsoft는 IE 10 이하의 버전 지원을 중단

## HTML5를 공부해야하는 이유

* 스마트 디바이스 시대가 되며 다양한 OS 등장 (각 디바이스 OS에 맞는 프로그램을 따로 개발해야함)
* 웹에서 동작하는 프로그램은 예외 (모든 디바이스에서 사용 가능)
* HTML5를 활용하면 Web을 넘어 Desktop 앱까지 개발 가능함 (ex. Electron, React Native)

<img src="https://user-images.githubusercontent.com/32444914/77058344-a77d7d80-6a18-11ea-8f2a-9848a23eb54b.png" style="zoom:67%;" />

### React Native

* 2012년 전후로 Adobe PhoneGap을 사용해 HTML5로 모바일 앱을 만드는 시도가 다양히 이루어짐
* **Facebook**은 PhoneGap에 만족하지 못하고 모바일 앱을 만들 수 있게하는 새로운 엔진 개발
* React Native를 사용하면 HTML5로 개발했을 때 내부적으로 안드로이드와 아이폰에 맞는 Native Code로 변환됨
* Facebook, Instagram, Skype, Uber 모두 React Native로 개발됨

<img src="https://user-images.githubusercontent.com/32444914/77058756-35f1ff00-6a19-11ea-9202-7378e873a59f.png" alt="react-native" style="zoom:60%;" />

### 그래서 HTML이 뭔가요?

<img src="https://user-images.githubusercontent.com/32444914/77059384-2de68f00-6a1a-11ea-92da-fbd4661d4184.png" alt="html5" style="zoom:50%;" />

HyperText Markup Language에 줄임말로서, 페이지의 제목, 문단, 표, 이미지, 동영상 등을 정의하고 그 구조와 의미리를 부여하는 마크업 언어로 웹의 구조를 담당한다. 2007년 3월 W3C가 공개적으로 XHTML 2.0의 실패를 인정한 후 새롭게 HTML을 개발하기로 결정하면서 WHATWG의 표준안을 대부분 수용하여 HTML5가 탄생하게 되었다.

> Markup Language
>
> 마크업 언어는 문서가 화면에 표시되는 형식을 나타내거나 데이터의 논리적인 구조를 명시하기 위한 규칙들을 정의한 언어의 일종이다. 데이터를 기술한 어어라는 점에서 프로그래밍 언어와는 차이가 있다.

## 참고 자료

* [HTML5 Markup](https://github.com/seulbinim/PDF/blob/master/HTML5.pdf)
* [입문자에게 추천하는 HTML, CSS 첫걸음](https://heropy.blog/2019/04/24/html-css-starter/)
* 내가 읽은 책 뭐였더라?
