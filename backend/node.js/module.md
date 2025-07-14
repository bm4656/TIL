## Node.js 모듈

Node.js는 모듈 단위로 각 기능을 분할한다.

- 모듈과 파일은 1:1 대응 관계를 가지며
- 하나의 모듈은 자신만의 독립적인 실행 영역(Scope)를 가진다.
- 따라서 클라이언트 사이드 JavaScript 와는 달리 전역변수의 중복 문제가 발생하지 않는다.

#### module

- module 이란 '독립된 기능을 갖는 것(함수, 파일)들의 모임' 으로 코드를 분리하기 위한 방법이다.
- 패키지는 모듈의 모음이다.
- npm 패키지들은 많은 모듈을 포함하고 있는 코드 모음이다.

모듈은 module.exports 또는 exports 객체를 통해 정의하고 외부로 공개한다. 그리고 공개된 모듈은 require 함수를 사용하여 import한다.

- module -> 현재 모듈의 객체이다.
- 각 모듈마다 있는 private 지역변수는 module로만 접근 가능하다.

## exports

모듈 안에 선언한 모든 것들은 기본적으로 해당 모듈 내부에서만 참조 가능하다.

- 이를 외부에 공개하여 다른 모듈에서 사용할 수 있도록 해주는 것이 export 객체이다.
- 전역 함수 require()로 추출한다.

```jsx
// circle.js
const { PI } = Math;
exports.area = (r) => PI * r * r;
exports.circumference = (r) => 2 * PI * r;

// app.js
const circle = require("./circle.js"); // == require('./circle')

console.log(`지름이 5인 원의 면적: ${circle.area(5)}`);
console.log(`지름이 5인 원의 둘레: ${circle.circumference(5)}`);
```

## module.exports (Node.js 내장객체)

- export 객체는 프로퍼티/메소드를 여러개 정의 할 수 있는 것에 반해 module.exports에는 하나의 값(원시 타입, 함수, 객체)을 할당할 수 있다.
- require()로 할당받은 변수는 module.exports에 할당한 값 자체이다.
- 즉 require() 호출 시 반환 받는 변수 그 자체이다.
- 객체 참조 변수로 현재 모듈의 객체의 주소 값이다.
- 비어 있는 객체가 기본값이며 어떤 것으로도 자유롭게 변경 가능하다.

exports는 module.exports의 참조이며 module.exports의 alias이다. 즉, exports는 module.exports와 같다고 보아도 무방하다.

- `module.exports` 객체는 Node.js에 의해 자동으로 빈 객체로 생성된 후 전역 실행 컨텍스트 this에 참조된다.
- `exports` 자체는 절대 반환되지 않는다. **_exports는 단순히 module.exports를 참조_**하고 있다. exports를 사용하면 모듈을 작성할 때 더 적은 양의 코드로 작성할 수 있으며 이 변수의 프로퍼티를 사용하는 방법도 안전하고 추천하는 방법이다.

```jsx
// foo.js
module.exports = function (a, b) {
  return a + b;
};

// app.js
const add = require("./foo");

const result = add(1, 2);
console.log(result);
```

module.exports는 1개의 값만을 할당할 수 있기에 다음과 같이 객체를 사용하여 복수의 기능을 하나로 묶어 공개하는 방식을 사용할 수 있다.

```jsx
// foo.js
module.exports = {
  add(v1, v2) {
    return v1 + v2;
  },
  minus(v1, v2) {
    return v1 - v2;
  },
};

// app.js
const calc = require("./foo");

const result1 = calc.add(1, 2);
console.log(result1); //3

const result2 = calc.minus(1, 2);
console.log(result2); //-1
```

### module.exports 와 exports 방법의 차이

exports를 사용할 때는 exports 객체에 프로퍼티를 추가하고,
module.exports를 사용할 때는 module.exports 변수에 아예 새로운 객체를 할당하는 것이다.

따라서 `exports = { }` 이렇게 새로운 값으로 하면 맨 처음 생성된 module.exports 와 다른 객체로 참조된다.

전역 실행 컨텍스트에 this는 자동으로 module.exports의 this로 참조된다.

## 코어 모듈과 파일 모듈

- 코어모듈 : Node.js가 기본으로 포함하는 모듈. 패스를 명시하지 않아도 무방하다.
  `const http = require('http');`
- npm의 통해 설치한 외부 패키지 : 패스를 명시하지 않아도 무방하다.
  `const mongoose = require('mongoose');`
- 파일 모듈 : 위 두 종류를 제외한 나머지. 반드시 패스를 명시하여야 한다.
  `const foo = require('./lib/foo');`

참고자료(https://velog.io/@hanblueblue/Node.js-Basic)

## Node.js 모듈(Common JS) vs ES6 모듈

`노드에서 각 파일은 비공개 네임스페이스를 가진 독립적인 모듈`(각 파일은 모두 모듈)

노드의 전역 객체 exports는 항상 정의되어있다. (`module.exports`의 기본값은 `exports`가 참조하는 것과 같은 객체이다.)

`ES6의 모듈성은 노드의 모듈성과 같은 개념이다.` 각 파일이 하나의 모듈이며 파일에서 정의한 상수,변수,함수,클래스는 명시적으로 내보내지 않는 한 해당 모듈에서만 사용된다. 모듈에서 값을 내보내면 다른 모듈에서 명시적으로 가져와 사용할 수 있다.

## ES 모듈
