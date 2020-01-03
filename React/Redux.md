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

---

단일 스토어에 상태 데이터를 저장하므로써 컴포넌트간 데이터 교환을 가능케함

action - 입금/출금 등 명세서 개념 (거래 명세서, 요청)

dispatcher - 은행 창구 직원 (현재 잔고와 action을 reducer에게 전달함)

reducer - dispatcher가 전달한 action의 종류에 따라 현재 잔고를 action에 맞게 수정, store에 저장

`combineReducers` - 여러가지 reducer를 하나로 합쳐주는 redux 모듈의 함수. 객체로 reducer를 묶어 전달한다.



### Redux DevTools

input tag (value vs. defaultValue)





1. src/index.js에서 App 컴포넌트를 public/index.html의 루트 태그 하위에 렌더한다.
2. App 컴포넌트는 요청된 URL에 맵핑된 컴포넌트를 렌더한다.
3. URL, 컴포넌트간 맵핑 관계를 정의하는 Router 컴포넌트 상위에 Provider 컴포넌트가 정의되어있다.
4. Provider 컴포넌트는 하위 컴포넌트에 redux store의 정보를 주입한다 (state와 dispatch 등). 단, 하위 컴포넌트에서 redux store의 정보를 사용하려면 redux connect 함수로 해당 컴포넌트와 redux 스토어를 연결시켜야한다.
5. 앱 최초 실행시 `/`로 접근하였으므로 Main 컴포넌트가 렌더된다. Main 컴포넌트는 Logo, SearchBar, VideoList 컴포넌트를 렌더한다.
6. SearchBar 컴포넌트는 사용자 입력 값이 변경될 때마다 src/actions에서 정의된 search action creator에 사용자 입력 값을 전달하여 새로운 action을 생성한다. search action creator는 dispatch함수에 바인드되어 있으므로 앞서 생성한 새로운 action을 dispatch 함수에 인수로 전달하여 호출한다 (mapDispatchToProps).
7. 6에서 호출된 dispatch는 search 리듀서에 자신이 전달받은 action을 그대로 넘겨준다 (질문. 어떻게 search 리듀서한테 제대로 전달하는지? 다른 reducer랑 안햇갈리고 - combineReducer 때문에 가능. 단, 리듀서마다 다루는 액션의 타입은 유니크해야한다.).
8. search 리듀서는 store의 현재 상태와 dispatch에게 전달받은 action을 통해 새로운 상태를 반환한다.
9. 검색어가 업데이트되었으므로 VideoList 컴포넌트는 업데이트된 검색어에 대한 결과를 화면에 렌더한다.
10. 

