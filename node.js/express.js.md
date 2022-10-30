## Express.js 시작하기

Express.js 는 Node.js 의 가장 유명한 웹 프레임워크이다.

- 필요에 따라 유연하게 구조 설정이 가능하다.
- 다양한 미들웨어를 통해 필요한 기능을 간단하게 추가할 수 있다.
- 모든 동작이 명시적으로 구성되기 때문에 웹 프레임워크의 동작 방식을 이해하기 가장 좋은 프레임워크이다.

### 1. npm init

Express.js를 처음부터 작성할 수 있는 방법이다. (직접 모든 구조를 작성)

```jsx
//터미널에서
$mkdir my-express
$cd my-express.js
$npm init
$npm i express

my-express(폴더이름임)
├── index.js
├── node_modules
├── package-lock.json
└── package.json

//index.js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.send("hello express!");
});
app.listen(3000, () => {
  console.log("server started");
});

//package.json 스크립트 부분 추가 해주기
"scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },

//이후 다시 터미널에서
$npm start // 서버 시작 localhost:3000
ctrl+c // 서버 종료
```

### 2. express-generator

Express.js는 express-generator 라고 하는 **프로젝트 생성기**를 제공한다.

- express-generator를 사용하면 프로젝트의 **기본구조를 자동으로 생성**해준다.
- **빠르게 프로젝트를 시작**하기 좋은 방법으로 생성된 프로젝트는 **npm start** 로 실행 가능하다.

```jsx
$npm i -g express-generator
$express my-server //자동으로 디렉토리만들어지고 그 안에 자동으로 파일도 생성됨
$cd my-server
$npm i //필요한 패키지 모두 설치
$npm start //서버 실행
```

### 3. npx + express-generator

npx를 사용하여 express-generator 를 설치하지 않고, 바로 사용 가능하다. express-generator는 프로젝트 생성 이후엔 사용되지 않기 때문에, npx를 사용하는 것도 좋은 방법이다.

```jsx
$npx express-generator my-web
$cd my-web
$npm i
$npm start
```

## Express.js 의 구조

```jsx
my-web
├── app.js //Express.js 의 가장 기본이 되는 파일, 웹 어플리케이션의 기능을 정의
├── bin
│   └── www //Express.js 실행 부분을 담당, 포트와 실행 오류 등을 정의
├── package.json //프로젝트 의존성 및 스크립트 정의
├── public //코드를 통하지 않고, 직접 제공되는 파일 디렉터리
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes //라우팅 파일 디렉터리
│   ├── index.js
│   └── users.js
└── views //HTML Template 디렉터리
    ├── error.jade
    ├── index.jade
    └── layout.jade
```

## Express.js 의 동작 방식

express-generator로 만들어진 프로젝트 디렉터리에 접근하여
**npm start** 로 Express.js 프로젝트를 실행하면 **localhost:3000 에 접속**하여 Welcome to Express 페이지를 확인할 수 있다.

1. 브라우저에서 localhost:3000 접속
2. app.js → app.use('/', indexRouter);
3. routes/index.js→router.get('/', ...
4. routes/index.js → res.render('index', ...
5. views/index.jade
   → 웹 페이지 “Welcome to Express” 화면

### 1. app.js

```jsx
var express = require('express');
...
var app = express();
```

app.js에서는 express() 로 생성되는 app 객체를 확인할 수 있다.

- **app 객체 → Express.js 기능을 담은 객체**
- **Express.js의 모든 동작은 app 객체에 정의된다!**

### 2. app 객체 주요 기능

- **app.use()**
  middleware 를 사용하기 위한 함수
- **app.listen()**
  http 서버를 생성해주는 함수, express-generator 를 사용하면 http.createServer를 사용하는데
  app.listen 함수로 대체할 수 있다.
- **app.locals**
  app에서 사용할 공통 상수, Express.js 에선 global 변수를 선언하지 않고 이 값을 사용할 수 있다.

## 라우팅

라우팅이란 HTTP 요청 URL에 해당하는 알맞은 응답의 경로를 미리 설정하는 것을 말한다.<br>
Express.js 는 다양한 라우팅 방식을 제공하는데, 크게 app 라우팅과 Express.Roueter 를 통한 라우팅으로 나누어진다.

### 1. app 라우팅

```jsx
app.get("/", (req, res) => {
  res.send("GET /");
});
app.post("/", (req, res) => {
  res.send("POST /");
});
app.put("/", (req, res) => {
  res.send("PUT /");
});
app.delete("/", (req, res) => {
  res.send("DELETE /");
});
app.all("/all", (req, res) => {
  res.send("ANY /");
});
```

- app 객체에 직접 get, post, put, delete 함수를 사용하여 HTTP method로 라우팅 할 수 있다.

- HTTP method 함수의 첫 번째 인자 → 이 라우팅을 실행할 URL

- 마지막 인자 → 라우팅이 실행될 때 작동하는 함수

- all 함수를 사용하면 HTTP method에 상관없이 라우팅이 가능하다.

### 2. Express.Router

app 라우팅을 통해서는 라우팅의 핵심인 그룹화를 지원하지 않는다. Express.Router 를 통해 라우팅을 모듈화 할 수 있다.

```jsx
const express = require("express");
const router = express.Router();

router.get("/", (req, res, next) => {
  res.send("respond with a resource");
});

module.exports = router;
```

- 작성된 라우터 모듈을 app 에 use함수로 연결하여 사용할 수 있다.

- router 객체에도 하위 라우터를 use 함수로 연결하여 사용할 수 있다.

```jsx
--- ./app.js
const userRouter = require('./routes/users');
const app = express();
//웹페이지의 '/users' 경로로 들어오는 그 이하의 모든 url에 대해서는 userRouter에서 처리하겠다.
app.use('/users', userRouter);

--- ./routes/users.js
const petRouter = require('./pets');
const router = express.Router();
//'/users' 하위 경로 중 '/pets' 경로는 petRouter에서 처리하겠다.
router.use('/pets', petRouter);

module.exports = router;
```

## 라우팅 - path parameter

Express.js 라우팅은 **path parameter**를 제공한다. path parameter를 사용하면, **주소의 일부를 변수처럼 사용**할 수 있다.

Ex)
/users/**:id** /users/123, /users/456 등으로 접속했을 때 라우팅 적용<br>
/boards/**:from\*\***:to\*\* /board/123-456 등으로 접속했을 때 라우팅 적용

### 1. Request Handler

라우팅에 적용되는 함수를 **Request Handler**라고 부른다.
HTTP요청과 응답을 다룰 수 있는 함수로 설정된 **라우팅 경로에 해당하는 요청**이 들어오면 Request Handler **함수가 실행**된다.

```jsx
router.get("/:id", (req, res) => {
  const id = req.params.id;
  res.send(`hello ${id}`);
});
```

- router 나 app의 HTTP method 함수의 가장 마지막 인자로 전달되는 함수이다.
- 설정된 라우팅 경로에 해당하는 요청이 들어오면 Request Handler 함수가 실행된다.
- 요청을 확인하고 응답을 보내는 역할을 한다.

### 2. Request Handler - Request 객체

HTTP 요청 정보를 가진 객체로 HTTP 요청의 path parameter, query parameter, body, header 등을 확인 할 수 있다.

- **req.params** -> URL 표현 중 /path/:id 에서:id 를 req.params.id 로 사용할 수 있다.
- **req.queries** -> URL 표현 중 /path?page=2 에서page 부분을 req.queries.page 로 사용할 수 있다.
- **req.body** -> 일반적으로 POST 요청의 요청 데이터를 담고 있다. req.body 에 요청 데이터가 저장되어 들어온다.
- **req.get('')** -> HTTP Request 의 헤더 값을 가져올 수 있는데, req.get('Authorization') 등으로 값을 가져온다.

### 3. Request Handler – Response 객체

HTTP 응답을 처리하는 객체로 HTTP 응답의 데이터를 전송하거나, 응답 상태 및 헤더를 설정할 수 있다.

- **res.send()** -> text 형식의 HTTP 응답을 전송함
- **res.json()** -> json 형식의 HTTP 응답을 전송함
- **res.render()** -> HTML Template 을 사용하여 화면을 전송함
- **res.set()** -> HTTP 응답의 헤더를 설정함
- **res.status()** -> HTTP 응답의 상태 값을 설정함
- 보내는 데이터 형식이 json인 경우 `res.send`보다 `res.json`을 사용하는 것이 좋다. 함수가 실행되는 로직이 아래와 같은데, `res.json`의 실행 횟수가 더 적기 때문에 효율적이다. - `res.send`: res.send → res.json → res.send - `res.json`: res.json → res.send
  💡 Express.js는 app 객체를 시작으로 모든 동작이 이루어지는데 app 객체나 Express.Router를 사용하여 라우팅을 구현하고, Request Handler를 통해 HTTP 요청,응답을 처리한다.

## 계층적 구조의 라우터

계층적 구조의 라우터를 사용할 때, 라우터의 선언 시

`Router({ mergeParams: true })`

를 사용해야, 이전 라우터에서 전달된 path parameter 를 사용할 수 있다.

```jsx
// index.js
const express = require("express");

const userRouter = require("./routes/users");

const app = express();
// "/" 경로에 아무런 설정을 하지 않으면, 첫 실행 시 Cannot GET /가 나타난다.
app.get("/", (req, res) => {
  res.send("OK");
});

/* 라우터를 '/users' 경로에 연결 */
app.use("/users", userRouter);

app.listen(8080);

// routes/users.js
//Router를 이용해 GET 요청 처리하는 API를 라우팅
const { Router } = require("express");

const router = Router();

router.get("/", (req, res) => {
  res.send("GET /users");
});

/* /:userId/pets 경로에 petsRouter 연결 */
const petsRouter = require("./pets");
router.use("/:userId/pets", petsRouter);

module.exports = router;

// routes/pets.js
const { Router } = require("express");

const router = Router({ mergeParams: true });

/* GET 라우팅 추가 */
router.get("/", (req, res) => {
  const { userId } = req.params;
  res.send(`Pets of user ${userId}`);
});
module.exports = router;
```
