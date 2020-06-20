# REST API

REST(Representational State Transfer)는 HTTP/1.0과 1.1의 스펙 작성에 참여하였고, 아파치 HTTP 서버 프로젝트의 공동 설립자인 로이 필딩(Roy Fielding)의 2000년 논문에서 처음 소개되었다. 발표 당시의 웹이 HTTP를 제대로 사용하지 못하고 있는 상황을 보고 HTTP의 장점을 최대한 활용할 수 있는 **아키텍쳐**로서 REST를 소개하였다. REST는 HTTP 프로토콜을 의도에 맞게 디자인하도록 유도하고 있다. REST의 기본 원칙을 성실히 지킨 서비스 디자인을 "RESTful"이라고 표현한다.

즉, **REST는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍쳐**이고, REST API는 REST를 기반으로 서비스 API를 구현한 것을 의미한다.

&nbsp;  

## 1. REST API의 구성

REST API는 자원(Resource), 행위(Verb), 표현(Representations)의 3가지 요소로 구성된다. REST는 자체 표현 구조(Self-descriptiveness)로 구성되어 REST API만으로 요청을 이해할 수 있다.

| 구성 요소             | 내용                           | 표현 방법        |
| --------------------- | ------------------------------ | ---------------- |
| 자원(Resource)        | 자원                           | HTTP URI         |
| 행위(Verb)            | 자원에 대한 행위               | HTTP 요청 메소드 |
| 표현(Representations) | 자원에 대한 행위의 구체적 내용 | HTTP 페이로드    |

&nbsp;  

## 2. REST API 설계 방침

**REST에서 가장 중요한 원칙은 두 가지이다.** URI는 리소스를 표현하는 데 집중하고, 행위에 대한 정의는 HTTP 요청 메소드를 통해 하는 것이 REST한 API를 설계하는 중심 규칙이다.

&nbsp;  

**1. URI는 리소스를 표현해야 한다.**

리소스를 식별할 수 있는 이름은 동사보다는 명사를 사용한다. URI는 리소스를 표현하는 데 중점을 두어야 한다. 리소스 이름에 "get" 같은 행위와 관련된 표현이 들어가서는 안된다.

```pseudocode
# bad
GET /getTodos/1
GET /todos/show/1

# good
GET /todos/1
```

&nbsp;  

**2. 리소스에 대한 행위는 HTTP 요청 메소드로 표현한다.**

리소스를 취득하는 경우에는 GET, 리소스를 삭제하는 경우에는 DELETE 메소드를 사용하여 리소스에 대한 행위를 명확히 표현한다. 리소스에 대한 행위는 GET, POST, PUT, PATCH, DELETE와 같은 HTTP 요청 메소드를 통해 표현하며 URI에 표현하지 않는다.

| HTTP 요청 메소드 | 종류           | 목적                  | 페이로드 |
| ---------------- | -------------- | --------------------- | -------- |
| GET              | index/retrieve | 모든/특정 리소스 취득 | X        |
| POST             | create         | 리소스 생성           | O        |
| PUT              | replace        | 리소스의 전체 교체    | O        |
| PATCH            | modify         | 리소스의 일부 수정    | O        |
| DELETE           | delete         | 모든/특정 리소스 삭제 | X        |

```pseudocode
# bad
GET /todos/delete/1

# good
DELETE /todos/1
```

&nbsp;  

## 출처

* [poiemaweb.com - REST API](https://poiemaweb.com/fastcampus/rest-api)

