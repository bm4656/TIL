## 리덕스 라이브러리

가장 많이 사용했던 리액트 상태 관리 라이브러리 → 전역 상태관리

- 컴포넌트의 상태 업데이트 관련 로직을 다른 파일로 분리시켜서 더욱 효율적으로 관리
- 미들웨어라는 기능을 제공하여 비동기 작업을 훨씬 효율적으로 관리

### 액션(action)

- 상태에 어떠한 변화가 필요하면 액션(action)이란 것이 발생 → 액션 객체
- type 필드 필수 → 이 값을 액션의 이름

```tsx
{
  type: 'ADD_TODO',
  data: {
    id: 1,
    text: '리덕스 배우기'
}
}
```

### 액션 생성 함수(action creator)

- 액션 객체를 만들어주는 함수

```tsx
function addTodo(data) {
  return {
    type: 'ADD_TODO',
    data,
  };
}

// 화살표 함수로도 만들 수 있습니다.
const changeInput = (text) => ({
  type: 'CHANGE_INPUT',
  text,
});
```

- 어떤 변화를 일으켜야 할 때마다 액션 객체를 만들어야 함.
  - 매번 액션 객체를 직접 작성하기 번거로울 수 있고,
  - 만드는 과정에서 실수로 정보를 놓칠 수도 있으므로 방지를 위해 함수로 관리

### 리듀서(reducer)

- 변화를 일으키는 함수

1. 액션 발생
2. 리듀서가 현재 상태와, 전달받은 액션 객체를 파라미터로 받아옴
3. 두 값을 참고해 새로운 상태로 반환

```tsx
const initialState = {
  counter: 1,
};
function reducer(state = initialState, action) {
  switch (action.type) {
    case INCREMENT:
      return {
        counter: state.counter + 1,
      };
    default:
      return state;
  }
}
```

### 스토어(store)

- 프로젝트에 리덕스를 적용하기 위해 스토어(store)를 만든다.
- 한 개의 프로젝트는 단 하나의 스토어만!
- 현재 애플리케이션 상태와 리듀서가 존재, 그 외에도 몇 가지 중요한 내장 함수

### 디스패치(dispatch)

- 디스패치는 ‘액션을 발생시키는 것’
- 스토어의 내장 함수 중 하나
- `dispatch(action)`과 같은 형태로 액션 객체를 파라미터로 넣어서 호출
- 이 함수가 호출되면 스토어는 리듀서 함수를 실행시켜서 새로운 상태를 만들어 준다.

### 구독(subscribe)

- 스토어의 내장 함수 중 하나

1. subscribe 함수 안에 리스너 함수를 파라미터로 넣어서 호출
2. 이 리스너 함수가 액션이 디스패치되어 상태가 업데이트될 때마다 호출

```tsx
const listener = () => {
  console.log('상태가 업데이트됨');
};
const unsubscribe = store.subscribe(listener);

unsubscribe(); // 추후 구독을 비활성화할 때 함수를 호출
```

> 액션 타입과 액션 생성 함수를 작성 → 리듀서를 작성 → 스토어 생성
