## 🔆 useRef

> `useRef` 는 .current 프로퍼티로 전달된 인자(initialValue)로 초기화된 **변경 가능한 ref 객체**를 반환합니다. 반환된 객체는 컴포넌트의 전 생애주기를 통해 유지될 것입니다. - React 공식 사이트

- 저장공간이나 DOM 요소에 접근하기 위해 사용되는 React Hook이다.
- useRef는 re-render와 상관없이 값이 유지된다는 특징이 있다.
- 바닐라 자바스크립트에서 querySelector, getElelmentById 등을 이용하여 특정 DOM을 선택하고 조작한다.
- 이를 React에서는 useRef 훅을 사용하여 조작할 수 있다.
  - React는 virtual DOM을 다루기 때문에 `document.getElementById()`으로 접근했을 때 문제가 발생할 수 있다!
  1. 리액트의 컴포넌트는 여러 개의 인스턴스를 가질 수 있다. → id가 중복될 수 있음
  2. ref를 사용하면 내가 정한 스코프에서만 접근 가능 → 전역적으로 ref가 사용되지 않기 때문에 유지보수에 용이함(단방향 데이터 흐름 방해하지 않기 때문)

### 사용 방법

1. useRef() 선언

```tsx
const inputRef = useRef(null);
```

1. 선택하고자 하는 DOM node(virtual DOM element)에 **ref 속성** 추가

```tsx
<input ref={inputRef} type='text' />
```

1. 필요한 곳에서 **변수명.current** 프로퍼티로 꺼내 쓰기

```tsx
<button onClick={() => inputRef.current.focus()}>input으로 포커스 </button>
```

## 🔆 scrollIntoView()

- 호출된 엘리멘트가 있는 위치로 스크롤을 이동시키는 자바스크립트 내장 메서드이다.
- 인자로 true/false값 또는 option 객체를 받을 수 있다.

`scrollIntoView(alignToTop?, scrollIntoViewOptions?)`

- alignIntoTop
  - true : 해당 요소의 제일 상단으로 스크롤 이동, 기본 값
    - `scrollIntoViewOptions: {block: "start", inline: "nearest"}` 와 동일함
  - false: 해당 요소의 제일 하단으로 스크롤 이동
    - `scrollIntoViewOptions: {block: "end", inline: "nearest"}` 와 동일
- **option 객체**
  - `{ behavior: "auto"/”instant/"smooth" }` :스크롤 시 즉시 적용할지, 부드러운 애니메이션 적용할지
  - `{ block:"start"/"center"/"end"/"nearest" }`: 수직 요소에 대한 옵션, 어느 선에서 멈출 지, default = start
  - `{ inline: "start"/"center"/"end"/"nearest" }` , 수평 요소에 대한 옵션, 어느 선에서 멈출 지, default = nearest
