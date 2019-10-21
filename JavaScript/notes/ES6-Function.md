# ES6-Function

## 3. 화살표 함수

### 3.1 화살표 함수 정의

선언문이 없고 모두 표현식

매개변수 `=>` 코드블록

```javascript
// 매개변수가 한 개일때
// function foo(a) {
// return a;
// }
const foo = a => a;

// 매개변수가 두 개 이상일때
// function foo(a, b) {
// return a + b;
// }
const foo = (a, b) => a + b;

// 매개변수가 두 개 이상이고 문이 2개 이상일때
// function foo(a, b) {
// const c = 10;
// return a + b + c;
// }
const foo = (a, b) => {
  const c = 10;
  return a + b + c;
};
```

