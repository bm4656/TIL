# JSX

**함수 호출과 객체 생성을 위한 문법적 편의를 제공하는 JavaScript의 확장이다.**

```jsx
const App = () => {
  return (
    <div>
      <p>hello</p>
      <MyComponent>hi</MyComponent>
    </div>
  );
};
```

- HTML과 비슷하게 생겼지만 다른 부분이 있다.
- JSX는 Babel에 의해서 Transcompile 된다.

## JSX 의 장점

1. 개발자 편의성 향상
2. 협업에 용이 / 생산성 향상
3. 문법 오류와 코드량 감소

## JSX 특징 / HTML과 차이점

### 1. HTML 태그 내에 JavaScript 연산

```jsx
const App = () = {
	const a =3;
	const b= 6;
    return <div> {a} + {b} ={a+b} </div>
}
```

### 2. class → className

### 3. 스타일은 object로

```jsx
<div className="first" style={{ padding: 10, color: "red" }}>
  {name}님 안녕하세요. <br />
  반갑습니다.
</div>
```

- 첫 대괄호는 js코드를 쓰겠다는 거고 두번째 대괄호가 object
- \*주의 : 위와 같은 Inline style의 Property name은 cameCase로 적는다.
- https://www.w3schools.com/react/react_css.asp

### 4. 닫는 태그 필수

- 기존 HTML에서는 닫는 태그를 작성하지 않아도 에러가 발생하지 않았고 `<input>, <br> ` 같은 일부 태그의 경우 아예 닫는 태그를 생략하여 코드를 작성해도 되었다.
- 하지만 JSX에서는 닫는 태그를 필수로 작성해야 한다.

### 5. 최상단 element는 반드시 하나

```jsx
//에러
const App = () => {
	return (
		<div>Hello</div> //에러 발생!
		<div>World</div>
	)
}
//올바른
const App = () => {
	return (
	<> {/*React.Fragment */}
		<div>Hello</div>
		<div>World</div>
	</>
	)
}
```

- JSX의 원칙상 최상단 Element는 한 개만 작성이 가능하기 때문에 이를 <div> 또는 <React.Fragment> 를 이용해 감싼다.
- 실제 렌더링 시에는 Fragment 안에 있는 내용만 출력된다.
- <React.Fragment>는 간단히 <> 로 표기가 가능하다.
