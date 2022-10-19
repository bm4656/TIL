# Callback

자바스크립트의 호스트 환경이 제공하는 여러 함수를 사용하면 비동기(asynchronous) 동작을 스케줄링 할 수 있다. (원하는 때에 동작이 시작하도록 할 수 있는 것이다.)

### 비동기 처리

현재 실행 중인 작업이 종료되지 않은 상태라고 해도 다음 작업을 곧바로 실행하는 방식이다.

- 즉, 현재 실행 중인 코드가 종료되기 전에 다음 라인의 코드를 실행하는 것 의미한다.
- 프로미스, 콜백 함수를 호출하는 함수 등 → 비동기적 실행
- 대표적으로 setTimeout을 이용하면 비동기 처리를 할 수 있다.

예를 들어, 3을 1초 뒤에 출력, 기다리는 동안 4가 출력되도록 하려면?

```javascript
console.log(1);
console.log(2);

setTimeout(() => {
  console.log(3);
}, 1000);

console.log(4);
```

## setTimeout

스케줄링에 사용되는 가장 대표적인 함수이다.

- setTimeout은 타이머를 식별할 때 사용하는 양의 정수 값을 반환한다.
- clearTimeout을 이용하면 타이머를 초기화할 수 있다.

**커피 주문 예제**

```javascript
const orderCoffee = (menu) => {
  console.log(`${menu} 나왔습니다.`);
};
//커피를 3잔 주문, 1초 뒤 아메리카노,
//그 1초 뒤 카라멜, 그 1초 뒤에 카페라떼
setTimeout(() => {
  orderCoffee("아메리카노");
  setTimeout(() => {
    orderCoffee("카라멜 프라푸치노");
    setTimeout(() => {
      orderCoffee("카페라떼");
    }, 1000);
  }, 1000);
}, 1000);
```

## callback 함수

함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수이다.

- 콜백 함수를 인자로 전달할 때는 함수의 이름만 넣어야 한다.
- 콜백 함수 가지고 있는 함수를 고차 함수라고도 한다.
- 어떤 특정한 시점에 호출되는 함수이다.

**예제**

```javascript
console.log("아메리카노 나왔습니다.");
setTimeout(() => {
  console.log("카라멜 프라푸치노 나왔습니다.");
}, 6000);

function order(callback) {
  setTimeout(() => {
    //callback()
    console.log("카라멜 프라푸치노 나왔습니다.");
    callback();
  }, 3000);
}

order(function () {
  console.log("아메리카노 나왔습니다.");
});

/*
	아메리카노 나왔습니다.
	카라멜 프라푸치노 나왔습니다.
	아메리카노 나왔습니다.
	카라멜 프라푸치노 나왔습니다.
*/
```

## 콜백 지옥

1초 뒤에 두 숫자를 더한 값을 반환해주는 함수에서 나온 결과를 가지고 또 다시 함수를 호출하는 방법은?

```javascript
function func(a, b) {
  setTimeout(() => {
    return a + b;
  }, 1000);
}
console.log(func(1, 2)); //undefined

let res1 = func(1, 2);
let res2 = func(res1, 3);

console.log(func(res2, 4)); //undefined -> console.log는 기다려주지 않아
```

func 함수는 비동기 동작을 하기 때문에 위 코드는 정상적으로 동작하지 않는다.
이를 해결하려면 콜백 함수를 이용해 계산된 결과를 매개변수인 콜백 함수로 넘겨주어야 한다.

```javascript
function callbackFunc(a, b, cb) {
  setTimeout(() => {
    return cb(a + b);
  }, 1000);
}

callbackFunc(1, 2, (res1) => {
  callbackFunc(res1, 3, (res2) => {
    callbackFunc(res2, 4, (res3) => {
      console.log(res3);
    });
  });
});
//10
```

위와 같은 상황을 **콜백 지옥**이라고 부른다.

깊은 중첩 코드가 만들어내는 패턴을 소위 ‘콜백 지옥(callback hell)’ 혹은 '멸망의 피라미드(pyramid of doom)'라고 부르는 것이다.

콜백 지옥의 예를 하나 더 들자면,
이름, 나이, 주소가 저장된 데이터를 비동기적으로 가져와야한다고 해보자.

```javascript
function getName(cb) {
  setTimeout(() => {
    cb("bomin");
  }, 2000);
}

function getAge(cb) {
  setTimeout(() => {
    cb(24);
  }, 2000);
}

function getAddress(cb) {
  setTimeout(() => {
    cb("Seoul");
  }, 2000);
}
```

위 정보를 console.log 한 번으로 출력해야한다면?

```javascript
getName((name) => {
  getAge((age) => {
    getAddress((address) => {
      console.log(name, age, address);
    });
  });
});
```

위 코드처럼 콜백함수 안에 콜백 함수를 반복하여 호출해야 name, age, address를 한꺼번에 접근할 수 있다.

- 비동기 함수가 3개 쓰이고, 각 2초씩 걸리기 때문에 6초 뒤에 Elice 6 Seoul이라는 log가 나온다. 비동기 함수 3개인데도 코드가 복잡하다.

이러한 콜백 지옥을 해결하기 위해 **프로미스**라는 개념이 등장하였다.

- 콜백 에러 핸들링과 추가 내용
  (https://ko.javascript.info/callbacks)
