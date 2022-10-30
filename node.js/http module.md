## http 모듈

Node.js에서 가장 기본적이고 중요한 웹 모듈로, 서버나 클라이언트와 관련된 기능을 제공한다.

## http 서버

####createServer()

1. 웹 서버 객체(=http.Server 객체)는 `createServer()` 함수로 생성한다.
   -> 콜백 함수 안에 `req, res` 등록
   즉, 요청의 정보를 담고있는 `request`와 응답의 정보를 담고있는 `response`라는 두 개의 매개변수가 있는 함수를 인자로 받습니다.
2. `response`의 `writeHead()`를 이용해 요청에 응답 헤더 정보를 보낼 수 있다.
   응답 헤더에는 Content-Type과 같은 정보를 포함한다.

3. `response`의 `end()` 함수는 헤더와 본문 데이터를 서버에 전달했음을 알린다. 인자로는 서버에 보낼 본문을 전달한다.

4. http.Server 객체에 `listen()`으로 포트 정보를 전달하여, 연결을 수신하는 HTTP 서버를 시작할 수 있다.

```jsx
// http 모듈을 불러오기
const http = require("http");
// "Hello http!"를 출력하는 서버 객체
http
  .createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.end("Hello http!");
  })
  // 8080포트로 서버를 시작
  .listen(8080);
```

## http 트랜잭션 해부

내용 추가하기
https://nodejs.org/ko/docs/guides/anatomy-of-an-http-transaction/
https://velog.io/@yhe228/node.js-%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-HTTP-server-%EA%B5%AC%EC%B6%95-
HTTP 요청이 서버에 오면 node가 트랜잭션을 다루려고 request 객체를 전달하며 요청 핸들러 함수를 호출한다.
요청을 실제로 처리하려면 listen 메서드가 server 객체에서 호출되어야한다.
대부분은 서버가 사용하고자 하는 포트 번호흫 listen에 전달하는 형태이다.
