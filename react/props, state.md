# Props(Properties)

## props

- 컴포넌트 활용 시 부모 Element로부터 자식 Element로 데이터를 전달해 주기 위해서 사용하는데, 기본적으로 컴포넌트에 원하는 값을 넘겨줄 때 사용한다.
- 넘겨줄 수 있는 값은 변수, 함수, 객체, 배열 등 JavaScript의 요소라면 제한이 없다.
- 주로 컴포넌트의 ‘재사용’을 위해 사용한다.

```jsx
//컴포넌트 생성
const Welcome = props => {
  return <h1>{props.name}</h1>;
};
//컴포넌트 사용
const App = () => {
  return (
    <div>
      <Welcome name='민지' />
      <Welcome name='해린' />
      <Welcome name='하니' />
    </div>
  );
};
```

### props는 읽기 전용이다.

- props의 값을 임의로 변경해서 사용하지 말기
- 만약 변경해서 사용하고 싶다면 새로운 변수를 생성하기

```jsx
//Don't
const Welcome = props => {
  props.name = props.name + '님';
  return <h1>Hello, {props.name}</h1>;
};
//Do
const Welcome = props => {
  const username = props.name + '님';
  return <h1>Hello, {username}</h1>;
};
```

### DOM Element의 Attributes

- 기본적인 DOM Element(div, span 등)들의 Attribute는 camel case로 작성한다.
  예: tabIndex, className 등
- 그러나 ‘data-’ 또는 ‘aria-’(접근성 관련)로 시작하는 Attribute는 예외이다.
  예: data-type, aria-label 등
- HTML의 Attribute와 다른 이름을 가지는 Attribute가 있다.
  class → className, for → htmlFor 등
- HTML의 Attribute와 다른 동작 방식을 가진 Attribute가 있다.
  checked(defaultChecked), value(defaultValue), style 등
- React에서만 쓰이는 새로운 Attribute가 있다.
  key, dangerouslySetInnerHTML 등

### HTML과 다른 방식의 React Attribute

```jsx
(<input type="checkbox" checked={false} />
```

- HTML에서 checked 또는 value는 해당 값이 **‘초기값’**으로 쓰이지만
  React 내에서는 **현재 값**을 의미한다.
- 즉, 위 예시처럼 checked 값이 **false**로 고정돼있는 경우에 사용자가 checkbox를 클릭하여도 값의 변화가 일어나지 않는다.
- 만약 ‘초기값’의 의미로 checked 또는 value를 사용하고 싶다면
  defaultChecked, defaultValue Attribute를 설정한다.

### \***\*React에서만 쓰이는 새로운 Attribute(key)\*\***

```jsx
const Names = () => {
  const names = [
    { key: '1', value: '민수' },
    { key: '1', value: '영희' },
    { key: '1', value: '길동' },
  ];
  return (
    <div>
      {names.map(item => (
        <li key={item.key}>{item.value}</li>
      ))}
    </div>
  );
};
```

- Key는 React가 어떤 항목을 변경, 추가 또는 삭제할 지 식별하는 것을 돕는다.
- Key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부 Element에 지정해야 한다.
- Key는 배열 안에서 형제 사이에서 고유해야 하고 전체 범위에서 고유할 필요는 없다.
- 두 개의 다른 배열을 만들 때 동일한 key 를 사용할 수 있다.

# State

## state

- State는 컴포넌트 내에서 유동적으로 변할 수 있는 값을 저장한다.
- 개발자가 의도한 동작에 의해 변할수도 있고 사용자의 입력에 따라 새로운 값으로 변경될 수도 있다.
- State 값이 변경되고 재렌더링이 필요한 경우에 React가 자동으로 계산하여 변경된 부분을 렌더링한다.

```jsx
import { useState } from 'react';
function Example() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>버튼을 {count}번 누름</p>
      <button onClick={() => setCount(count + 1)}>클릭</button>
    </div>
  );
}
```

### state 값을 직접 변경하지 않는다.

- state 값을 직접 변경하게 되면 React가 컴포넌트를 다시 렌더링할 타이밍을 알아차리지 못한다.
- 반드시 setState 함수를 이용해 값을 변경!
- setState 함수를 호출할 때 React에게 “다시 렌더링 해주세요~” 라는 명령이 내려진다.

```jsx
//Don't
function Example() {
	const [count, setCount] = useState(0);
  return (
    <div>
			<p>버튼을 {count}번 누름</p>
			<button onClick={() => {count = count + 1;}>
				클릭
      </button>
    </div>
	);
}
```

### state를 변경하는 두 가지 방법

1. setState 내에 변경할 값을 넣기

```jsx
const [count, setCount] = useState(0);
setCount(count + 1);
```

1. setState에 함수를 넣기

```jsx
const [count, setCount] = useState(0);
setCount(current => {
  return current + 1;
});
```

- 함수를 넣는 경우 함수가 **반환(return)하는 값으로 State가 변경된다.**
- 위처럼 **현재 값을 기반으로 State를 변경하고자 하는 경우** 함수를 넣는 방법을 권장한다.

### Object를 갖는 State를 만들 때 주의사항

```jsx
//Don't
const [user, setUser] = useState({ name: '민지', grade: 1 });
setUser(current => {
  current.grade = 2;
  return current;
});
```

- 위의 경우 React가 State의 변경을 감지하지 못한다.
- user object 안의 내부의 값은 변경되었지만 user 자체는 변경되지 않았기 때문이다.
- 따라서 기존 user의 내용을 **새로운 object(사본)**에 담고 grade를 변경해야한다.

```jsx
const [user, setUser] = useState({ name: '민지', grade: 1 });
setUser(current => {
  const newUser = { ...current };
  newUser.grade = 2;
  return newUser;
});
```
