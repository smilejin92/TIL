# Composition vs. Inheritance

## Containment

* 일부 컴포넌트는 자신의 children이 무엇인지 미리 알 수 없다 (ex. generic "boxes" component).
* 이러한 컴포넌트들은 자식 요소를 아웃풋에 전달하기 위해 `children` prop을 사용한다.

```react
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

이러한 방법은 다른 컴포넌트가 JSX를 중첩하여 임의의 children을 전달할 수 있도록 한다.

```react
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

`<FancyBorder>` 하위의 JSX 태그들은 `FancyBorder` 컴포넌트의 `children` prop으로 전달된다.

&nbsp;  

## Specialization

* generic한 컴포넌트를 재사용하여 special한 컴포넌트를 작성하는 경우 (ex. `Dialog` 컴포넌트 -> `WelcomeDialog` 컴포넌트)
* HOC
* more specific한 컴포넌트가 more generic한 컴포넌트를 렌더할 때 props/children을 설정

```react
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}

class SignUpDialog extends React.Component {
  state = {login: ''};

  handleChange = (e) => {
    this.setState({login: e.target.value});
  }

  handleSignUp = () => {
    alert(`Welcome aboard, ${this.state.login}!`);
  }
  
  render() {
    return (
      <Dialog title="Mars Exploration Program"
              message="How should we refer to you?">
        <input value={this.state.login}
               onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>
          Sign Me Up!
        </button>
      </Dialog>
    );
  }
}
```

&nbsp;  

## 그래서 Inheritance는?

* props와 composition만으로 기존의 컴포넌트를 customize하기 충분하고, 또한 안전하다.
* 컴포넌트에 전달되는 props에 원시 값, 리액트 요소, 함수 등 다양한 데이터를 바인딩할 수 있다.
* 컴포넌트 사이의 non-UI 기능을 재사용하고 싶다면 자바스크립트 모듈로 분리하면 된다.

&nbsp;  