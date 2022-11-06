## HTML 요소 삽입하기

- 요소 삽입하기 : 현재의 html에 요소(element)를 추가하는 것

```html
// index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="vie1. wport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
    <script src="scripts.js" defer></script>
  </head>
  <body>
    <div class="box">
      <button class="button" id="button">요소 추가하기</button>
      <div id="placeForElements"></div>
    </div>
  </body>
</html>
```

```css
/* style.css */
.box {
  width: 100vw;
  text-align: center;
  margin-top: 3rem;
  background-color: #bdbdbd;
}

.button {
  font-size: 3rem;
}
```

```jsx
//scripts.js
// 요소 모음
const button = document.querySelector("#button");
const placeForElements = document.querySelector("#placeForElements");

// 이벤트 추가
button.addEventListener("click", addElement);

// 이벤트에 사용될 함수
function addElement() {
  const element = `<h1>추가된 요소</h1>`;

  placeForElements.insertAdjacentHTML("beforeend", element);
}
```

위에 예제에서는

1. div 안에 h1 요소가 주입된다.
2. 주입하는 함수는 `insertAdjacentHTML()`이다.

주입할 떄, 주입할 요소는 2가지 종류가 가능하다.

- 문자열 : `"<h1>추가된 요소</h1>"`
- Node(요소)객체 : `document.createElement('h1')`

### 요소 주입하는 함수들

```jsx
타겟.innerHTML += 요소          -> 요소는 문자열, 혹은 Node 객체 모두 가능
타겟.appendChild(요소)          -> 요소는 Node 객체만 가능
타겟.append(요소)               -> 요소는 문자열, 혹은 Node 객체 모두 가능
타겟.insertAdjacentHTML('beforeend', 요소)       -> 요소는 문자열만 가능
```

- 위에 어떤 함수를 써도, 타겟에 요소를 주입한다는 점은 같다.
- 하지만 보통 다음과 같은 규칙으로 선택한다.(퍼포먼스;코드 실행속도 등을 고려했을 때)
  - 문자열 형태를 주입 -> `insertAdjacentHTML()`
  - Node 객체 형태를 주입 -> `appendChild()`

### insertAdjacentHTML

`insertAdjacentHTML(포지션, 문자열 요소)`

- 포지션은 주입 위치를 의미하며 4종류 -> 거의 beforeend만 사용한다.
- 포지션: beforebegin, afterbegin, beforeend, afterend

#### 예제로 알아보기

1. 주입 전

```html
<body>
  <div id="original" style="border: 1px solid">오리지널</div>
</body>
```

2. 주입

```jsx
const original = document.querySelector("#original");

// 문자열 형태 요소
const a = "<p>a</p>";
const b = "<p>b</p>";
const c = "<p>c</p>";
const d = "<p>d</p>";

original.insertAdjacentHTML("beforebegin", a);
original.insertAdjacentHTML("afterbegin", b);
original.insertAdjacentHTML("beforeend", c);
original.insertAdjacentHTML("afterend", d);
```

3. 주입 후

즉, 요소 안에 주입할 때는 **b or c** 를 사용한다.
보통 요소의 마지막에 주입하기 때문에 **c**를 사용한다.

-> 따라서 `beforeend`를 많이 사용하게 된다.
