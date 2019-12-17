Switch문을 쓰지 않으면 Route에 exact를 활용해야한다. 단 에러 페이지를 따로 커스텀할 수 없다.

# Redux

* 오픈 소스 라이브러리
* 앱의 상태를 관리하기 위해 개발됨

* go along with React Router

### When do I need Redux?

* Complex data flows
* Inter-component communication
* Non-hierarchical data (React Router)
* Many actions
* Same data used in multiple components



### 3 main concepts

* Actions - ~한 데이터 변경 요청 (객체)
* Reducers - (함수) 기존 데이터에 대해서 새로운 데이터를 리턴 (파라미터로 받은 action에 대해서만 작업을 수행)
* Store - 저장

...and more

* pure functions
* immutability

환경 구축

```bash
npm uninstall create-react-app -g
npm install create-react-app -g

create-react-app redux
npm install redux --save
npm install react-redux --save
```

