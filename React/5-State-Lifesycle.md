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

지금까지 배운 내용만으로 UI를 업데이트하기 위해서는 한 가지 방법 뿐이었다. 상태가 변경될때마다 `ReactDOM.render` 메소드를 호출하여 UI를 다시 그리는 것이다.

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

캡슐화된 `Clock` 컴포넌트에는 한 가지 중요한 부분이 빠져있다. `Clock` 컴포넌트는 자신의 내부에서 직접 타이머를 설정하고 업데이트 해야된다는 점이다. 위의 코드는 `setInterval` 함수의 콜백으로 전달된  `tick` 함수가 매초 UI를 새롭게 그려낸다.

가장 이상적인 방법은 아래 코드를 한번만 작성하여 `Clock` 컴포넌트가 자신의 상태를 스스로 관리하는 것이다.

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
3. 함수 컴포넌트 내부의 코드를 클래스 컴포넌트 `render` 메소드 내부로 옮긴다.
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

위의 예제를 통해 `Clock` 컴포넌트는 함수 컴포넌트가 아닌 클래스 컴포넌트로 정의되었다.

`render` 메소드는 업데이트가 발생될 때마다 호출된다. 단, `<Clock />` Element는 이전과 같은 DOM 노드 내에서 렌더되어야한다.  `<Clock />` Element는 `Clock` 클래스가 반환한 하나의 인스턴스이다. 따라서, `Clock` 클래스 몸체에서 `Clock` 클래스가 반환하는 인스턴스의 지역 상태(local state)와 생명주기 메소드를 정의할 수 있게된다.



### 5.2 클래스의 지역 상태 

`props`객체의  `date` 프로퍼티를 (미래에 생성될) 인스턴스의 상태로 옮기는 과정은 아래와 같다.

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

2. 클래스 컨스트럭터를 정의하여 컨스트럭터 내부에서 `this.state`를 초기 값을 설정한다.

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

   상위 클래스 `React.Component`의 컨스트럭터에 `props` 객체를 전달하는 점을 유의하자.

   ```jsx
   constructor(props) {
       super(props);
       this.state = { date: new Date() };
   }
   ```

   클래스 컴포넌트는 항상 상위 클래스의 컨스트럭터에 `props` 객체를 전달하여 호출해야한다.

3. `<Clock />` element의 `date` 프로퍼티를 삭제한다.

   ```jsx
   ReactDOM.render(
   	<Clock />,
       document.getElementById('root')
   );
   ```

   타이머 코드는 나중에 클래스 컴포넌트 내부에 추가할 것이다.



아래는 위의 과정을 모두 거친 결과 코드이다.

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



### 5.3 클래스의 생명주기 메소드

다량의 컴포넌트를 포함하는 어플리케이션에서는, 생명주기가 끝난 컴포넌트가 차지하는 자원(메모리 등)을 되찾는 것이 중요하다.

위에서 구현한 `Clock` 컴포넌트가 렌더될 때마다 타이머를 실행하는 과정을 React에서 마운팅(mounting)이라 표현한다.

또한 `Clock` 컴포넌트가 생성한 DOM이 제거될 때마다 타이머를 멈추는 과정을 React에서 언마운팅(unmounting)이라 표현한다.

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

