# React Hook

기존의 방법 (state componenet)에서는 리액트 컴포넌트를 상속 받아야만 지역 상태를 관리할 수 있었다.

리액트 훅은 함수의 클로저로 구현되어있다. 자유 변수를 활용하여 상태 관리를 한다.

```jsx
function Example() {
	const [count, setScount] = useState(0);
}
```

| this.setState             | React Hooks 상태 변화 함수                          |
| ------------------------- | --------------------------------------------------- |
| 기존의 상태를 유지 + 병합 | 기존 상태 X, 파라미터로 받은 새로운 상태만 업데이트 |

useReducer, useMemo(함수의 이전 실행 결과 값에 변화가 생기면 실행), useCallback(함수 자체(주소 값까지)를 기억해놓는다)

## Local Storage

