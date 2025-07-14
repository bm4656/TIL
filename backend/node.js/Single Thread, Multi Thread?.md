## Single Thread, Multi Thread

node.js는 싱글 스레드로 동작하면서 동시에 여러 요청을 처리할 수 있어야한다.

node의 싱글 스레드는 클라이언트로부터 요청을 받으면 그 요청을 다른 일꾼에게 전달한다. 따라서 싱글 스레드는 자유로워지고 두번째 요청을 받을 수 있다. 두번째 요청을 받을 경우 다른 일꾼에게 전달한다. 그리고 여기서 일꾼은 다른 서버 또는 데이터베이스에 쿼리를 날려 요청을 처리한다.
일꾼이 응답을 가져왔다면(서버또는 데이터베이스의 응답을 받아옴) 콜백 함수를 실행하게 된다.
<img width="685" alt="image" src="https://user-images.githubusercontent.com/65716445/210243851-1a161252-bcbb-4fc1-9fbd-967a9aebdc19.png">

> node.js는 싱글 스레드라고 했는데 어떻게 멀티 스레드처럼 일꾼들을 데리고 동작할 수 있는걸까?

node.js는 V8이라는 자바스크립트 엔진과 비동기 작업을 처리하는 `libuv`라는 라이브러리로 이루어져있다.

<img width="708" alt="image" src="https://user-images.githubusercontent.com/65716445/210244027-f92a3d6c-7d6b-425d-b811-9b47403aaca6.png">

비동기 작업을 가능하게 하는 것은 libuv라는 라이브러리에서 non-blocking IO라는 기능을 가능하게 하는 이벤트 루프를 제공하기 때문이다. libuv는 c언어로 개발되었고 시스템 커널을 이용하는데, 커널은 멀티 스레드를 이용한다.
따라서 node.js는 libuv가 멀티스레드로 동작하기 때문에 비동기 처리를 할 수 있다.

- Non Blocking I/O (하나의 요청을 처리하는 동안 다른 요청을 블로킹하지 않는다는 의미)

요청의 흐름을 나타내보면

1. node.js로 요청이 들어오면 들어온 요청은 event queue에 추가한다.
2. node.js의 이벤트 루프는 event queue를 살펴 들어온 요청이 있다면 선착순(first come first served) 요청이 처리한다.
3. 요청은 internal C++ Thread Pool로 보내진다. 이것은 libuv에서 개발된 이벤트 루프의 일부로 여러 요청을 수행할 수 있게 한다. 동시에 이벤트 루프는 event queue에 요청이 있는지 계속해서 확인하면서 요청이 있다면 thread pool로 가져온다.
4. thread pool은 db 또는 file 또는 다른 서버 등에 보낸 요청을 수행한다.
5. 수행을 마치면 콜백 함수를 실행시켜 이벤트 루프로 응답을 전달한다.
6. 이벤트 루프는 응답을 클라이언트에 보낸다.

<br/>

> **용어정리**
> V8 엔진: 자바스크립트 코드를 평가하여 객체등의 동적 데이터가 할당되는 memory heap, context의 실행을 담당하는 하나의 call stack(= execution context stack)을 가진다.
> event loop: pending 상태인 자바스크립트 task와 microtask를 execution context stack에 푸시하여 실행시킨다.
