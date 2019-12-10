# 5. State & Lifesycle (상태와 생명주기)

3.2의 시계 예제를 다시 살펴보자.

```jsx
function tick() {
    const element = (
    	<div>
        	<h1>Hello, world!</h1>
            <h2>It is {new Date().toLocaletimeString()}.</h2>
        </div>
    );
    ReactDOM.render(element, document.getElementById('root'));
}
setInterval(tick, 1000);
```

지금까지 배운 내용만으로 UI를 업데이트하는 방법은 한 가지 뿐이었다. 상태가 변경될때마다 `ReactDOM.render` 메소드를 호출하여 UI를 다시 그리는 것이다.

이번 장에서는 `Clock` 컴포넌트를 어떻게 모듈/캡슐화 시키는지에 대해 알아볼 것이다. 이 과정을 통해 `Clock` 컴포넌트의 내부에서 어떠한 방법으로 직접 타이머를 설정하고 매초 자신의 상태를 업데이트할 수 있는지에 대해 파해쳐보자.

우선 `Clock` 컴포넌트를 캡슐화해보자.

```jsx
function Clock(props) {
    return (
    	<div>
        	<h1>Hello, world!</h1>
            <h2>It is {props.date.toLocaleTimeString()}.</h2>
        </div>
    );
}

function tick() {
    ReactDOM.render(
    	<Clock date={new Date()} />,
        document.getElementById('root')
    );
}

setInterval(tick, 1000);
```

캡슐화된 `Clock` 컴포넌트에는 한 가지 중요한 부분이 빠져있다. `Clock` 컴포넌트는 스스로 타이머를 설정하고 업데이트할 수 있어야된다는 점이다. 위의 코드는 `setInterval` 함수의 콜백으로 전달된  `tick` 함수가 매초 UI를 새롭게 렌더한다.

가장 이상적인 방법은 아래 코드를 한번만 작성하여 `Clock` 컴포넌트가 자신의 상태를 스스로 관리할 수 있게 하는 것이다.

```jsx
ReactDOM.render(
	<Clock />,
    document.getElementById('root')
);
```

이를 구현하기 위해서는 `Clock` 컴포넌트에 상태(state)를 추가해야한다.

상태는 `props` 객체와 유사하지만, 상태는 `private`하며 컴포넌트에 의해서만 접근이 가능하다.



### 5.1 함수 컴포넌트에서 클래스 컴포넌트로

함수 컴포넌트를 클래스 컴포넌트로 변환하는 과정은 아래와 같다.

1. 함수 컴포넌트와 같은 이름의 클래스를 `React.Component`에 `extends`하여 생성한다.
2. 비어있는 `render` 메소드를 추가한다.
3. 함수 컴포넌트 내부의 코드를 클래스 컴포넌트 `render` 메소드 안으로 옮긴다.
4. `render` 메소드 내부의 `props` 객체를 `this.props`로 변경한다.
5. 이전의 함수 컴포넌트 코드를 삭제한다.

```jsx
class Clock extends React.Component {
    render () {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
            </div>
        );
    }
}
```

위의 예제를 통해 `Clock`은 함수 컴포넌트가 아닌 클래스 컴포넌트로 정의되었다.

`render` 메소드는 `React.Component` 클래스로부터 상속되는 메소드로, 특정 컴포넌트가 관리하는 UI에 업데이트가 발생될 때마다 호출된다.  `<Clock />` Element는 `Clock` 클래스가 반환한 하나의 인스턴스이다. 따라서, `Clock` 클래스 몸체에서 `Clock` 클래스가 반환하는 인스턴스의 지역 상태(local state)와 생명주기 메소드를 정의할 수 있게된다.



### 5.2 지역 상태 추가

`props`객체의  `date` 프로퍼티를 인스턴스의 상태로 설정하는 과정은 아래와 같다.

1. `Clock` 클래스 `render` 메소드의 `this.props.date`를 `this.state.date`로 변경한다.

   ```jsx
   class Clock extends React.Component {
       render() {
           return (
           	<div>
               	<h1>Hello, world!</h1>
                   <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
               </div>
           )
       }
   }
   ```

2. 클래스 컨스트럭터를 정의하여 컨스트럭터 내부에서 `this.state`의 초기 값을 객체로서 설정, `date` 프로퍼티를 할당한다.

   ```jsx
   class Clock extends React.Component {
       constructor(props) {
           super(props);
           this.state = { date: new Date() };
       }
       
       render() {
           return (
           	<div>
               	<h1>Hello, world!</h1>
                   <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
               </div>
           )
       }
   }
   ```

   상위 클래스 `React.Component`의 컨스트럭터에 `props` 객체를 전달하는 점을 유의하자 (클래스의 인스턴스 생성과정 참조).

   ```jsx
   constructor(props) {
       super(props);
       this.state = { date: new Date() };
   }
   ```

   클래스 컴포넌트는 항상 상위 클래스의 컨스트럭터에 `props` 객체를 전달하여 호출해야한다.

3. `ReactDOM.render` 메소드의 인자`<Clock />` element의 `date` 어트리뷰트를 삭제한다.

   ```jsx
   ReactDOM.render(
   	<Clock />,
       document.getElementById('root')
   );
   ```

   타이머 코드는 나중에 클래스 컴포넌트 내부에 추가할 것이다.



아래 코드 예제는 위의 과정을 모두 거친 `Clock` 컴포넌트의 결과이다.

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```



### 5.3 생명주기 메소드 추가

다량의 컴포넌트를 포함하는 어플리케이션에서는 생명주기가 끝난 컴포넌트가 차지하는 자원(메모리 등)을 되찾는 것이 중요하다.

위에서 구현한 `Clock` 컴포넌트가 렌더되는 것(실제 DOM 요소로 생성되어 HTML에 추가되는 것)을 React에서 마운팅(mounting)이라 표현한다.

또한 `Clock` 컴포넌트가 생성한 DOM이 제거되는 것을 React에서 언마운팅(unmounting)이라 표현한다.

컴포넌트가 마운트/언마운트될 때마다 실행되는 특별한 메소드를 클래스 컴포넌트 내부에 선언할 수 있다.

```jsx
class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = { date: new Date() };
    }
    
    // 마운팅
    componentDidMount() {
        
    }
    
    // 언마운팅
    componentWillUnmount() {
        
    }
    
    render() {
        return (
        	<div>
            	<h1>Hello, World!</h1>
                <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
        )
    }
}
```

이러한 메소드를 생명주기 메소드(lifecycle methods)라 표현한다.

`componentDidMount` 메소드는 컴포넌트의 반환한 React Element가 DOM에 렌더된 직후에 실행되는 메소드이다. 시계의 타이머를 실행시키기 적합한 장소이다.

```jsx
componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
}
```

위의 코드에서 타이머 아이디를 `this`에 프로퍼티로 정의한 것을 주목해보자 (`this.timerID`).

`this.props`와 `this.state`는 React에서 특별한 의미를 가지지만, 그 외 경우에는 클래스에 추가적으로 필드를 추가할 수 있다. 단, 클래스 필드를 추가하는 경우 해당 필드는 데이터의 흐름에 영향을 주지 않는 필드여야한다. (ex. 타이머 아이디)

타이머는 `componentWillUnmount` 메소드 안에서 소멸된다.

```jsx
componenetWillUnmount() {
    clearInterval(this.timerID);
}
```

마지막으로 매초 `this.state`의 `date` 프로퍼티를 업데이트할 `tick` 메소드를 `Clock` 컴포넌트 안에 정의해보자. `tick` 메소드는 `this.setState` 메소드를 사용하여 컴포넌트의 지역 상태를 업데이트한다.

```jsx
class Clock extends React.Componenet {
    constructor(props) {
        super(props);
        this.state = {date: new Date()};
    }
    
    componentDidMount() {
        this.timerID = setInterval(() => this.tick(), 1000);
    }
    
    componentWillUnmount() {
        clearInterval(this.timerID);
    }
    
    tick() {
        this.setState({ date: new Date() });
    }
    
    render() {
        return (
        	<div>
            	<h1>Hello, world!</h1>
                <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
        );
    }
}

ReactDOM.render(<Clock />, document.getElementById('root'));
```

위 코드의 실행 순서를 정리하면 아래와 같다.

1. `<Clock />` 컴포넌트가 `ReactDOM.render`에 전달되면, `Clock` 컴포넌트의 컨스트럭터가 호출된다. `Clock`은 현재 시간을 표시해야하므로, `this.state` 객체에 현재 시간을 담아 둘 프로퍼티를 초기화 해놓는다.
2. 이어서 `Clock` 컴포넌트의 `render` 메소드가 호출된다. 이 과정을 통해 React는 화면에 어떠한 요소가 출력되어야 하는지 알게된다. 그리고 React는 DOM을 `Clock`의 `render` 메소드가 반환하는 요소와 일치하도록 업데이트한다.
3. `Clock`이 반환한 결과가 DOM에 주입되면, React는 `componentDidMount` 메소드를 호출한다. `componentDidMount` 메소드 내부에서 `tick` 메소드가 매초 실행되게끔 `setInterval`함수를 호출한다.
4. 매초 브라우저에서 `tick` 메소드를 호출한다. `tick` 메소드 내부에서 `setState` 메소드를 사용하여 `Clock` 컴포넌트의 지역 상태(`this.state.date`)를 업데이트한다. `setState`가 실행되면, React는 상태가 변화되었음을 감지하여 `render` 메소드를 다시 호출한다. 이 과정을 통해 React는 화면에 어떠한 요소가 출력되어야 하는지 알게된다. 새롭게 호출된 `render` 메소드 내부의 `this.state.date`은 이전(1초전)과 값이 다르며, 렌더된 결과 역시 업데이트된 시간을 포함한다.
5. `Clock` 컴포넌트가 DOM에서 제거된다면, React는 `componentWillUnmount` 메소드를 호출하여 타이머를 종료시킨다.



### 5.4 올바른 상태 관리

`setState` 메소드 사용에 대한 세 가지 유의사항이 있다.

#### 1. 상태를 직접 조작해서는 안된다.

예를 들어, 아래 코드는 컴포넌트의 `render` 메소드를 호출하지 않는다.

```jsx
// 잘못된 예제
this.state.comment = 'Hello';
```

대신, `setState`를 사용하면 `render` 메소드가 호출된다.

```jsx
// 올바른 예제
this.setState({ comment: 'Hello' });
```

`this.state`에 직접 값을 할당할 수 있는 곳은 컨스트럭터 내부 뿐이다.



#### 2. 상태 업데이트는 비동기적으로 수행될 수도 있다.

`this.props`와 `this.state`는 비동기적으로 업데이트될 수 있기 때문에, 다음 상태를 계산하기 위해 현재 상태의 값에 의존해서는 안된다.

예를 들면, 아래의 코드는 `counter`를 업데이트하는 데 실패할 수도 있다.

```jsx
// 잘못된 예제
this.setState({ counter: this.state.counter + this.props.increment })
```

이러한 상황을 피하기 위해서는 객체 대신 함수를 인자로 받는 `setState`의 두 번째 양식을 사용하면된다. 인자로 전달되는 함수의 인자로는 첫번째 인수와 두 번째 인수로 각각 이전의 상태(state)와 업데이트가 발생하는 시점의 props를 두 번째 인수로 전달 받는다.

```jsx
// 올바른 예제
this.setState((state, porps) => ({
    counter: state.counter + props.increment
}));
```



#### 3. 상태 업데이트는 Merge된다.

`setState`를 호출하면, React는 `setState`에 전달된 객체를 현재 상태에 병합(merge)한다.

예를 들어, 상태가 여러 개의 독립적인 프로퍼티를 포함한다고 했을때,

```jsx
constructor(props) {
    super(props);
    // 상태에는 posts와 comments 같은 독립적인 프로퍼티가 담겨있다.
    this.state = {
        posts: [],
        comments: []
    }
}
```

`setState`를 구분하여 각 프로퍼티를 업데이트할 수 있다.

```jsx
componentDidMount() {
    fetchPosts().then(res => {
        this.setState({ posts: res.posts })
    });
    
    fetchComments().then(res => {
        this.setState({ comments: res.comments })
    });
}
```

`setState`의 인자로 전달된 객체는 `this.state` 객체에 병합될 때 자신이 포함하는 프로퍼티만을 변경한다. 예를 들어, `this.setState({comments})`는 `this.state.posts`를 변경하지 않고, `this.state.comments`만을 완전히 대체한다.



### 5.5 데이터는 아래로 흐른다.

부모와 자식 컴포넌트 모두 어떠한 컴포넌트가 stateful(상태를 가지고 있는) 혹은 stateless(상태를 가지지 않는)한지 알 수 없다. 또한 어떠한 컴포넌트가 함수형인지 클래스형인지에 대해 알 필요도 없다.

위와 같은 이유 때문에 상태(state)는 종종 local(지역의) 혹은 encapsulated(캡슐화된)라고 불린다. 상태는 상태를 직접 소유하고 있는 컴포넌트에서만 접근이 가능하다.

컴포넌트는 컴포넌트의 상태를 하위 컴포넌트의 props 객체로 전달할 수 있다.

```jsx
<h2>It is {this.state.date.toLocalTimeString()}.</h2>
```

위 예제는 사용자 정의 컴포넌트에서도 동일하게 동작한다.

```jsx
<FormattedDate date={this.state.date} />
```

`FormattedDate` 컴포넌트는 `date`을 props로서 전달 받는다. `FormattedDate` 컴포넌트는 전달 받은 `date`이 `Clock` 컴포넌트의 상태인지 혹은 `props`인지에 대해 전혀 알 수 없다.

```jsx
function FormattedDate(props) {
    return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

이러한 하위 요소로의 데이터 전달 방법을 "top-down" 혹은 "unidirectional (단방향)" 데이터 플로우라고 한다. 예를 들어, a라는 상태와 a를 소유하고 있는 컴포넌트 A가 있다고 가정해보자.  a에서 파생된 데이터 혹은 UI는 A의 하위 컴포넌트에만 영향을 줄 수 있다.

