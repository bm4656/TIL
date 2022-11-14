# React

### SPA(Single Page Application)

최초에 서버로부터 HTML을 전달받고 페이지의 변경이 필요할 때 그 부분을 JSON으로 전달받는다.

이 때 페이지에서 변경된 부분만 계산하여 다시 그린다.

## React

사용자 인터페이스를 만들기 위한 Javascript 라이브러리

### Component

React에서 서비스를 개발하는데 있어 독립적인 단위로 쪼개어 구현

### Virtual DOM\*

가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화하는 프로그래밍 개념

\*Document Object Model

### JSX

JavaScript 내에서 UI를 작성하기 위해 개발자에게 익숙한 환경을 제공, HTML과 유사

JSX를 사용하는 것은 선택사항, 그러나 개발 효율을 위해 사용하는 것을 권장함

### React를 쓰는 이유

**생산성/재사용성**

**풍부한 자료/라이브러리**

**다양성**

## React 특징

### JS + HTML

```jsx
<div>
  <Select>
    {Type.map((item) => (
      <option value={item} key={item}>
        {item}
      </option>
    ))}
  </Select>
</div>
```

{중괄호} 만 열면 자바스크립트 코드 작성이 가능하다.

### 컴포넌트

```jsx
const App = () => {
  const text = "hello world";
  return <span>{text}</span>;
};
```

위와 같은 형태로 하나의 '블록'을 만들어서 필요한 곳에 '조립'하여 개발한다.
리액트 개발 요소의 가장 작은 단위이다.

### State

```jsx
const [data, setData] = useState([]);
```

컴포넌트 내에서 'State'를 이용하여 데이터를 유동적으로 관리한다.
'State'가 변경될 때마다 컴포넌트가 다시 렌더링 된다.
