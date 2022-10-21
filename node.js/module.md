## Node.js 모듈

module 이란 '독립된 기능을 갖는 것(함수, 파일)들의 모임' 이다.

Node.js는 module 단위로 각 기능을 분할할 수 있다. module은 파일과 1대1의 대응 관계를 가지며 하나의 모듈은 자신만의 독립적인 실행 영역(Scope)를 가지게 된다. 따라서 클라이언트 사이드 JavaScript 와는 달리 전역변수의 중복 문제가 발생하지 않는다.

모듈은 module.exports 또는 exports 객체를 통해 정의하고 외부로 공개한다. 그리고 공개된 모듈은 require 함수를 사용하여 import한다.

## Node.js 내장객체 module.exports

- module : 현재 모듈의 객체이다.
- 각 모듈마다 있는 private 지역변수는 module로만 접근 가능하다.

### module.exports

- require() 호출 시 반환 받는 변수
- 객체 참조 변수로 현재 모듈의 객체의 주소 값
- 비어 있는 객체가 기본값이며 어떤 것으로도 자유롭게 변경 가능
- `module.exports` 객체는 Node.js에 의해 자동으로 빈객체로 생성된 후 전역 실행 컨텍스트 this에 참조됨
- `exports` 자체는 절대 반환되지 않는다. **_exports는 단순히 module.exports를 참조_**하고 있다. exports를 사용하면 모듈을 작성할 때 더 적은 양의 코드로 작성할 수 있으며 이 변수의 프로퍼티를 사용하는 방법도 안전하고 추천하는 방이다.

### module.exports 와 exports 방법의 차이

exports를 사용할 때는 exports 객체에 프로퍼티를 추가하고,
module.exports를 사용할 때는 module.exports 변수에 아예 새로운 객체를 할당하는 것이다.

따라서 `exports = { }` 이렇게 새로운 값으로 하면 맨 처음 생성된 module.exports 와 다른 객체로 참조된다.

전역 실행 컨텍스트에 this는 자동으로 module.exports의 this로 참조된다.

## Node.js 모듈(Common JS) vs ES6 모듈

`노드에서 각 파일은 비공개 네임스페이스를 가진 독립적인 모듈`(각 파일은 모두 모듈)

노드의 전역 객체 exports는 항상 정의되어있다. (`module.exports`의 기본값은 `exports`가 참조하는 것과 같은 객체이다.)

`ES6의 모듈성은 노드의 모듈성과 같은 개념이다.` 각 파일이 하나의 모듈이며 파일에서 정의한 상수,변수,함수,클래스는 명시적으로 내보내지 않는 한 해당 모듈에서만 사용된다. 모듈에서 값을 내보내면 다른 모듈에서 명시적으로 가져와 사용할 수 있다.

## ES 모듈
