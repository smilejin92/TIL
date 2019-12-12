# Lists and Keys

### 1. 다중 컴포넌트 렌더

요소들의 집합을 만들어 JSX 내부에 삽입할 수 있다.

아래 예제는 `numbers` 배열을 `map` 메소드로 순회하여 새로운 배열을 생성한다. 생성된 배열은 각 요소에 `<li>` 객체를 담아둔다. 배열을 JSX 내부에서 사용할 수 있다.

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map(number => {
    <li>{number}</li>
});

ReactDOM.render(
	<ul>{listItems}</ul>,
    document.getElementById('root')
);
```



### 2. 목록 컴포넌트

### 3. Keys

key를 따로 정의하지 않으면 React는 index를 디폴트로 사용한다.

### 4. Extracting Components with Keys

`<ListItem key={uuid.v4()}/>`

### 5. Keys Must Only Be Unique Among Siblings

전역에서 unique할 필요는 없다.

key는 props로 전달되지 않는다. key값이 필요한 경우 새로운 prop으로 넘겨야한다.

### 6. map 함수 JSX에 임베드

