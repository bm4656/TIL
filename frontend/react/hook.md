# Hook

컴포넌트에서 **데이터를 관리(State)하고 데이터가 변경될 때 상호작용(Effect)** 을 하기 위해 사용한다.

### Hook의 등장 배경

- 기존에는 컴포넌트 내에서 State와 생명주기를 관리하기 위해서 반드시 클래스 컴포넌트(Class Component)를 사용하여야 했다.
- 그러나 개발자가 느끼기에 다소 복잡한 클래스 컴포넌트(Class Component)를 보완하고 함수 컴포넌트에서 클래스 컴포넌트의 기능을 구현하기 위해 **React 16.8 버전**에 추가된 것이 바로 **Hook**이다.

### 유의사항

- **Hook은 React 함수(컴포넌트, Hook) 내에서만 사용한다.**
- Hook의 이름은 반드시 `use` 로 시작해야한다.
- 최상위 Level에서만 Hook을 호출할 수 있다.
  → if문, for문 내부 또는 콜백함수 내에서 호출하지 말기

## State Hook

```jsx
const App = () => {
  // 일반적인 useState 사용법
  const [state이름, setState이름] = useState(초기값);
};
```

- useState : 컴포넌트 내 동적인 데이터를 관리할 수 있는 hook
- 최초에 useState가 호출될 때 초기값으로 설정, 이후 재 렌더링이 될 경우 무시된다.
- state는 읽기 전용이므로 직접 수정하지 않는다.
  - state를 변경하기 위해서는 setState를 이용한다.
- state가 변경되면 자동으로 컴포넌트가 재 렌더링된다.
  - setState 함수 호출하면 state 값이 변경되었음을 리액트 코어에 알려주는 로직이 마지막에 있고 그 로직이 호출되었을 때 컴포넌트가 다시 그려짐

```jsx
const App = () => {
  const [title, setTitle] = useState('');
  // State를 변경할 값을 직접 입력
  setTitle('Hello');

  // 또는 현재 값을 매개변수로 받는 함수 선언
  // return 값이 state에 반영됨
  setTitle(current => {
    return current + 'World';
  });
};
```

- state를 변경하기 위해서는 setState 함수에 직접 값을 입력하거나
- 현재 값을 매개변수로 받는 함수를 전달한다. 이 때 함수에서 return되는 값이 state에 반영된다.

## Effect Hook

```jsx
const App = () => {
useEffect(EffectCallback, Deps?)
}
```

- Effect Hook을 사용하면 **함수 컴포넌트에서 side effect를 수행**할 수 있습니다.
  → 즉, 어떠한 값이 변할 때마다 내가 설정한 함수가 실행된다.
- 컴포넌트가 최초로 렌더링될 때, 지정한 State나 Prop가 변경될 때마다 **이펙트 콜백 함수가 호출**된다.
- **Deps**: 변경을 감지할 변수들의 집합(배열)
- **EffectCallback**: Deps에 지정된 변수가 변경될 때 실행할 함수

```jsx
const App = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('버튼을 ${count}회 클릭했습니다.');
  }, [count]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>클릭하세요</button>
    </div>
  );
};
```

- Effect Hook을 사용하면 함수 컴포넌트에서 side effect를 수행할 수 있다.
- 컴포넌트가 최초로 렌더링될 때, 지정한 State나 Prop가 변경될 때마다 이펙트 콜백 함수가 호출된다.

### 넘겨준 deps 값이 [ ] 일 때

```jsx
const App = () => {
  useEffect(() => {
		// State가 변경될 때, 컴포넌트를 렌더링할 때
		const intervalId = setInterval(()=>{
			console.log("안녕하세요"); }, 1000);
		// 컴포넌트를 재 렌더링 하기 전에, 컴포넌트가 // 없어질 때
		return () => {
			clearInterval(intervalId);
	}
}, [])
...
```

- 넘겨준 값이 없더라도 컴포넌트가 생성이 될 때 최초로 한 번은 실행이 되기 때문에
  → 컴포넌트가 생성이 될 때 한 번만 실행을 해줘!라는 의미
- useEffect의 이펙트 함수 내에서 다른 함수를 return 할 경우
  → state가 변경되어 컴포넌트가 다시 렌더링되기 전과 컴포넌트가 없어질 때(Destroy) 호출할 함수를 지정

## 이외의 Hooks

### useMemo

- 변수 메모제이션
- 지정한 State나 Props가 변경될 경우 해당 값을 활용해 **계산된 값을 메모이제이션**하여 재렌더링 시 불필요한 연산을 줄인다.
- useMemo의 연산은 **렌더링 단계**에서 이루어지기 때문에 렌더링 과정과 무관하게 시간이 오래 걸리는 로직을 작성하지 않는 것을 권장한다.

```jsx
const App = () => {
	const [firstName, setFirstName] = useState('민지')
	const [lastName, setLastName] = useState('김')

// 이름과 성이 바뀔 때마다 풀네임을 메모이제이션
const fullName = useMemo(() => {
	return ′${firstName} ${lastName}′
	}, [firstName, lastName])
}
```

### useCallback

- **함수**를 **메모이제이션**하기 위해 사용하는 Hook
- 컴포넌트가 재렌더링될 때 불필요하게 함수가 다시 생성되는 것을 방지
- useMemo(()⇒fn,deps) 와 useCallback(fn,deps)는 같다.

```jsx
const App = () => {
	const [firstName, setFirstName] = useState('민지')
	const [lastName, setLastName] = useState('김')
// 이름과 성이 바뀔 때마다
// 풀네임을 return하는 함수를 메모이제이션
const getfullName = useCallback(() => {
	return ′${firstName} ${lastName}′
}, [firstName, lastName])
  return <>{fullname}</>
}
```

### useRef

- **컴포넌트 생애 주기 내에서 유지**할 ref 객체를 반환한다.
- 일반적으로 React에서 **DOM Element에 접근**할 때 사용한다(DOM Element의 **ref 속성**을 이용)
- useRef에 의해 반환된 ref 객체가 **변경되어도** 컴포넌트가 **재렌더링되지 않는다.**
- ref 객체는 **.current**라는 프로퍼티를 가지며 이 값을 자유롭게 변경할 수 있다.

```jsx
const App = () => {
  const inputRef = useRef(null);
  const onButtonClick = () => {
    inputRef.current.focus();
  };
  return (
    <div>
      <input ref={inputRef} type='text' />
      <button onClick={onButtonClick}>input으로 포커스 </button>
    </div>
  );
};
```

### 일반 변수 선언과 useRef()의 차이

- useRef Hook 은 DOM 을 선택하는 용도 외에, 컴포넌트 안에서 조회 및 수정 할 수 있는 변수를 관리하는 것이 있다.

- useRef 로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않는다. 리액트 컴포넌트에서의 상태는 상태를 바꾸는 함수를 호출하고 나서 그 다음 렌더링 이후로 업데이트 된 상태를 조회 할 수 있는 반면, useRef 로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있다.

- 컴포넌트는 그 컴포넌트의 state나 props가 변경될 때마다 호출되는데(re-rendering), 함수형 컴포넌트는 일반 자바스크립트 함수와 마찬가지로 호출될 때마다 함수 내부에 정의된 로컬 변수들을 초기화합니다.

- 따라서 `const nextId = { current: 4 };` 의 nextId.current는 함수가 호출될 때마다 4이다.

- 반면 useRef로 만들어진 객체는 React가 만든 전역 저장소에 저장되기 때문에 함수를 재 호출하더라도 마지막으로 업데이트한 current 값이 유지된다.

[참고자료](https://react.vlpt.us/basic/12-variable-with-useRef.html)

## 커스텀 Hook

- 자신만의 Hook을 만들면 컴포넌트 로직을 함수로 뽑아내어 재사용할 수 있다.
- UI 요소의 재사용성을 올리기 위해 컴포넌트를 만드는 것 처럼, 로직의 재사용성을 높이기 위해서는 Custom Hook을 제작한다.

```jsx
function useMyHook(args) {
  const [status, setStatus] = useState(null);
  // ...
  return status;
}
```

- 한 로직이 여러 번 사용될 경우 함수를 분리하는 것 처럼 Hook을 만드는 것일 뿐, 새로운 개념은 아니다.
- Hook의 이름은 ‘use’로 시작.
- 한 Hook 내의 state는 공유되지 않는다.
