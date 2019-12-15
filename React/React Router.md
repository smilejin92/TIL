# React Router

리액트 라우터는 리액트 컴포넌트를 특정 URL에 맵핑하여, 사용자가 특정 URL로 접근시 맵핑되어 있는 컴포넌트를 렌더할 수 있도록 해주는 모듈이다.

### 설치 방법 (React Router DOM)

```bash
# 리액트 라우터 DOM - 리액트 Web 앱 개발시
npm i react-router-dom --save

# 리액트 라우터 네이티브 - 리액트 네이티브 앱 개발시
# npm i react-router-native

# 리액트 라우터 (dom, native 모두 포함)
# npm i react-router
```



### 예제 1. 기본 라우팅

본 예제는 Home, About, Users 세 개의 페이지를 리액트 라우터로 핸들링하는 예제이다. 각 `<Link>` 컴포넌트를 클릭하면 라우터는 해당 컴포넌트 URL과 매칭되는 `<Route>` 컴포넌트를 렌더한다.

> `<Link>` 컴포넌트는 HTML `<a>` 태그와 `href` 속성을 그대로 사용한다. 따라서 키보드 혹은 스크린 리더 사용자도 해당 링크에 접근이 가능하다.

```jsx
import React from 'react';
import {
    BrowserRouter as Router,
    Switch,
    Route,
    Link
} from 'react-router-dom';

export default function App() {
    return (
    	<Router>
        	<div>
            	<nav>
                	<ul>
                    	<li>
                        	<Link to="/">Home</Link>
                        </li>
                        <li>
                        	<Link to="/about">About</Link>
                        </li>
                        <li>
                        	<Link to="/users">Users</Link>
                        </li>
                    </ul>
                </nav>
                
                {/* <Switch> 컴포넌트는 자신의 하위 요소인 <Route> 컴포넌트 중 사용자가 접근한 URL과 일치하는 가장 첫 번째 <Route> 컴포넌트를 렌더한다. */}
                <Switch>
                	<Route path="/about" component={About} />
                    <Route path="/users" component={Users} />
                    <Route path="/" component={Home} />
                </Switch>
            </div>
        </Router>
    );
}

function Home() {
    return <h2>Home</h2>;
}

function About() {
    return <h2>About</h2>;
}

function Users() {
    return <h2>Users</h2>;
}
```



### 예제 2. 중첩 라우팅

중첩 라우팅이 어떻게 동작하는 지에 대한 예제이다. `App` 컴포넌트의 `/topics` 라우트는 `Topics` 컴포넌트를 로드한다. 이후 `Topics` 컴포넌트가 렌더한 `<Link>` 컴포넌트를 클릭하면 `Topics` 컴포넌트 내부의 라우터가 해당 `<Link>` 컴포넌트에 맵핑되어 있는 URL과 매칭되는 라우트를 렌더한다.

```jsx
import React from 'react';
import {
    BrowserRouter as Router,
    Switch,
    Route,
    Link,
    useRouteMatch,
    useParams
} from 'react-router-dom';

export default function App() {
  return (
  <Router>
    <div>
      <ul>
        <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
        </ul>
          
        <Switch>
          <Route path="/about" component={About} />
          <Route path="/topics" component={Topics} />
          <Route path="/" component={Home} />
        </Switch>
      </div>
    </Router>
  );
}

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Topics() {
  // useRouteMatch: match 객체를 반환한다.
  // match 객체는 <Route path>가 요청된 URL에 어떻게 매치되었는지에 대한 정보를 담고 있다.
  // match 객체는 아래와 같은 프로퍼티를 가지고 있다.
  // params: URL로부터 분리된 key/value 객체. 고정된 경로 이후의 문자열(쿼리 스트링)에 대한 정보를 갖는다.
  // isExact: 요청된 URL과 라우팅된 path가 100% 일치하는지에 대한 정보 (boolean)
  // path: 라우팅에 사용된 path 패턴 (문자열)
  // url: 요청된 URL과 일치하는 부분 (문자열)
  let match = useRouteMatch();
    
  return (
  <div>
    <h2>Topics</h2>
      <ul>
        <li>
          <Link to={`${match.url}/components`}>Components</Link>
        </li>
        <li>
          <Link to={`${match.url}/props-v-state`}>Props v. State</Link>
        </li>
      </ul>
        {/* Topics 페이지는 '/topics' URL 경로에 더해진 추가적인 라우트들을 자신의 <Switch>문 안에 가지고 있다. 아래 두번째 <Route>는 모든 topic에 대한 index 페이지라고 생각하면된다. */}
      <Switch>
        <Route path={`${match.path}/:topicId`} component={Topic} />
        <Route path={match.path}>
          <h3>Please select a topic.</h3>
        </Route>
      </Switch>
    </div>
  );
}

function Topic() {
    // useParams: match 객체의 params 프로퍼티(객체)를 반환한다.
    let { topicId } = useParams();
    return <h3>Requested topic ID: {topicId}</h3>;
}
```



### 주요 컴포넌트

