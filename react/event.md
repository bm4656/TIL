# 이벤트

## 이벤트란

- **이벤트(event)란** 웹 브라우저가 알려주는 HTML 요소에 대한 사건의 발생을 의미한다.
- 사용자**의 행동**에 의해 발생할 수도 있으며 **개발자가 의도한 로직**에 의해 발생할 수도 있다. 이렇게 발생된 이벤트를 자바스크립트를 이용해 대응할 수 있다.
- 이벤트 핸들러 함수에서는 다양한 로직을 처리하고 그 결과를 사용자에 출력하여 알릴 수도 있다.

### 이벤트 처리(핸들링) 방법

1. 핸들링 함수 선언

```jsx
const App = () => {
    const handleClick = () => {
			alert("클릭했습니다.");
		}
return (
	<div>
		<button onClick={() => {handleClick}>클릭하세요</button>
	</div>
	);
};
```

- 별도의 핸들링 함수를 선언하고 element에 넘겨주는 방법

1. 익명 함수로 처리

```jsx
const App = () => {
return (
	<div>
		<button onClick={() => {alert("클릭했습니다.")
		}>클릭하세요</button>
	</div>
	);
);

```

- 이벤트를 할당하는 부분에서 익명함수를 작성하는 방법

### 이벤트 객체

- DOM Element 는 핸들링 함수에 이벤트 object를 매개변수로 전달한다.
- 이벤트 object를 이용하여 이벤트 발생 원인,이벤트가 일어난 Element에 대한 정보를 얻을 수 있다.
- 이벤트 형태(클릭,키 입력등)와 DOM종류(button, form, input 등)에 따라 전달되는 이벤트 object의 내용이 다르기 때문에 유의해야한다.
- https://developer.mozilla.org/ko/docs/Web/API/Event

```jsx
const App = () => {
const handleChange = (event) => {
	console.log(event.target.value)
	+ "라고 입력했네요.");
	}
return (
    <div>
      <input onChange={handleChange} />
		</div>
		);
};
```

### 많이 쓰이는 DOM 이벤트

- **onClick**: Element를 클릭했을 때
- **onChange**: Element의 내용이 변경되었을 때(input의 텍스트를 변경, 파일 선택 등)
- **onKeyDown, onKeyUp, onKeyPress**: 키보드 입력이 일어났을 때
- **onDoubleClick**: Element를 더블 클릭했을 때
- **onFocus**: Element에 Focus되었을 때
- **onBlur**: Element가 Focus를 잃었을 때
- **onSubmit**: Form Element에서 Submit 했을 때

## 컴포넌트 내 이벤트 처리

### \***\*DOM Input 값을 State에 저장하기\*\***

```jsx
const App = () => {
  const [inputValue, setInputValue] = useState("defaultValue");

  const handleChange = (event) => {
    setInputValue(event.target.value);
  };
  return (
    <div>
      <input onChange={hadleChange} defaultValue={inputValue} />
      <br />
      입력한 값은: {inputValue}
    </div>
  );
};
```

- **event** object의 **target**은 이벤트의 원인이 되는Element를 가리킨다.
- 현재 event의 target → input element
  - 입력된 value를 가져와 setState를 하는 모습

### 여러 Input 동시에 처리하기

```jsx
const App = () => {
	const [user, setUser] = useState({ name: "민지",
school: "00대학교" });
	const handleChange = (event) => {
		const { name, value } = event.target;
		const newUser = { ...user };
		newUser[name] = value;
		setUser(newUser);
};
  return (
    <div>
      <input name="name" onChange={handleChange}
value={user.name} />
			<br />
			<input name="school" onChange={handleChange}
value={user.school} />
			<p>
				{user.name}님 : {user.school}에 재학중
			</p>
		</div>
};
```

- State를 여러 개 선언할 수도 있지만 **object**를 활용하여 여러 개의 input을 state로 관리하는 방법이 있다.
- **target**으로부터 **name**을 받아와 해당 **name**의 **key**에 해당하는 **value**를 변경하여 state에 반영한다.

## 다른 컴포넌트로 이벤트 전달

### 컴포넌트간 이벤트 전달하기

- 사용자가 입력한 정보를 현재 컴포넌트가 아닌 부모 컴포넌트에서 활용해야하는 경우 이벤트를 Props로 전달하여 처리한다.

```jsx
const MyForm = ({ onChange }) => {
  return (
		<div>
			<span>이름: </span>
			<input onChange={onChange} />
		</div>
	)
}

const App = () => {
	const [username, setUsername] = useState('')
	return (
		<div>
			<h1>{username}님 환영합니다.</h1>
			<MyForm>
				onChange={(event) => {
				setUsername(event.target.value)
				}}
			/>
	</div>
	)
}
```

### 커스텀 이벤트

- 단순히 DOM 이벤트를 활용하는 것을 넘어서 나만의 이벤트를 만들 수도 있다.

```jsx
const SOS = ({ onSOS }) => {
  const [count, setCount] = useState(0);
  const handleClick = () => {
    if (count >= 2) {
      onSOS();
    }
    setCount(count + 1);
  };
  return <button onClick={handleClick}>세 번 누르면 긴급호출({count})</button>;
};

const App = () => {
  return (
    <div>
      <SOS
        onSOS={() => {
          alert("긴급사태!");
        }}
      />
    </div>
  );
};
```

### 이벤트 명명법

- 직접 이벤트를 만들 때 이름은 자유롭게 설정할 수 있다.
- 보통은 “on” + 동사, “on” + 명사 + 동사 형태로 작성한다.
- 핸들링 함수에 경우 “handle” 을 앞에 붙인다. (“handle” 대신 이벤트명과 동일한 “on”을 앞에 붙여도 무방)

---
