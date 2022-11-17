# Component

**1. React에서 페이지를 구성하는 최소단위이다.**

**2. Component의 이름은 대문자로 시작한다.**

**3. Class Component / Function Component**

**4. Controlled Component / Uncontrolled Component**

### Component

```jsx
const Mycomponent = {{ children }} => {
    return <div style= {{ padding:20, color: 'yellow' }}>
	            {children}
	    </div>;
}
```

위처럼 Component를 만들고 다른 component에서 자유롭게 활용(아래)할 수 있다.

```jsx
const App = () => {
	return (
		<div>
			<p>hello<p/>
			<MyComponent>hi</MyComponent>
		</div>
	);
}
```

Component의 이름은 대문자로 시작한다. HTML 요소와 구분하기 위한 리액트의 약속이다.

## Class Component 와 Function Component

```jsx
//Class Component
class Hello extends Component {
  render() {
    const { name } = this.props;
    return <div>{name}님 안녕하세요.</div>;
  }
}

//Function Component
const Hello = (props) => {
  const { name } = props;
  return <div>{name}님 안녕하세요.</div>;
};
```

- 초기 React의 Component는 모두 Class Component 였다.
- 이후 v16 부터 새로운 Function Component와 Hooks 개념이 발표되었으며 현재는 Function Component가 주로 사용되고 있다.

### Class Component 의 특징

- Class 개념 → JAVA 개발자에게 친숙한 형태
- React의 생명주기를 파악하기 쉽다. → ([https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/))

## Component의 특징

```jsx
<MyComponent user={{ name: "보민" }} color="purple">
  <div>안녕하세요.</div>
</MyComponent>
```

- 컴포넌트에 Attribute에 해당하는 부분 → Props(Properties)
- 컴포넌트 안에 작성된 하위 Element → children
- children도 결국엔 props 중 하나이다.

```jsx
const Mycomponent = (props) => {
	const  {user, color, children } = props
	return (
		<div style = {{color}}>
		<p>{user.name}님의 하위 element는 </p>
	            {children}
	    </div>;
	)
}
```

- 상위 Element로부터 전달받은 props를 활용하는 코드
- 이 컴포넌트의 자식(children)요소 역시 props로부터 값을 받아오는 것을 볼 수 있다.

1. **컴포넌트 끼리 데이터를 주고 받을 땐 Props**
2. **컴포넌트 내에서 데이터 를 관리할 땐 State**
3. **데이터는 부모→자식으로만 전달**
