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

# React 시작하기

```bash
npx create-react-app <디렉토리명>
cd <디렉토리명>
npm start
```

- npx : npm 패키지를 1회성으로 내려 받아 실행할 때 사용하는 명령어
- 실행하면 public 디렉토리 속 index.html 파일 뜨고 그 다음 src 안에 파일이 뜬다.

```bash
npm install
//package.json에 정의된 dependency(의존 성 패키지)들을 설치
npm install <패키지명>
//npm 서버로부터 원하는 패키지를 내려 받기
npm start
//프로젝트를 실행(Node.js 서버 이용)
npm build
//프로젝트를 빌드
(Ctrl + C)
//명령을 중지(npm start 후 종료)
```

## 디렉토리 구조

- ./node_modules/ : npm을 이용해 설치한 패키지들 모음
- ./public/ :정적인파일들을모아놓는곳
- ./src/ : 리액트 개발을 위한 파일들을 모아놓는 곳
- ./.gitignore : Git을 이용할 경우에 불필요한 파일을 무시할 수 있도록 하는 설정파일
- ./package.json : 프로젝트에 관한 정보와 사용하는 패키지들을 명세하는 파일
- ./README.md : 프로젝트에 관한 설명을 작성하는 파일

## 라이브러리

```bash
npm install
//package.json 파일 내에 정의된 패키지 모두 설치
npm install <패키지명>
//npm 서버로부터 패키지 내려받기
npm install <패키지명>@<version>
//특정 버전의 패키지 내려받기
npm install <git 레포지토리 주소>
//npm이 아닌 git 레포지토리로부터 패키지 내려받기
```

### package.json

dependencies(의존성) 라는 키 아래에 설치된 패키지 목록이 나열된다.

```json
{ ...
	"dependencies": {
    "@testing-library/jest-dom": "^5.16.4",
    "@testing-library/react": "^13.3.0",
    "@testing-library/user-event": "^13.5.0",
    "prop-types": "^15.8.1",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "styled-components": "^5.3.5",
    "typescript": "^4.7.4",
	},
	...
}
```

- ^(캐럿) : 버전명에 ^과 <,≤,>,≥ 등으로 범위를 나타낼 수 있다.
  - ^ 이것과 관련된 버전 중 가장 최신 버전을 설치해줘!
  - 예) ^1.0.2 : >=1.0.2 <2.0 이나 ^1.0 : >=1.0.0 <2.0

### import

설치한 라이브러리를 프로젝트 내에서 import로 불러온다.

```jsx
import "패키지명";
import something from "패키지명";
import { a, b } from "패키지명";
import * as something from "패키지명";
```

1. CSS나 import하는 것 만으로 역할을 하는 라이브러리인 경우 패키지명을 바로 import 한다.
2. 기본적으로 패키지를 불러와 활용할 때에 는 할당할 이름을 작성한다.
3. 패키지 내의 일부 메소드나 변수만 가져올 때는 구조분해를 하여 가져오는 것이 효율적이다.
4. 패키지에 default로 export되는 객체가 존재하지 않을 경우 \* as 이름 으로 불러올 수 있다.

**CSS**

```jsx
import "./App.css";
//별도의 CSS 파일 작성 후 프로젝트에 적용
//.css 파일명 붙여주어야 함
```
