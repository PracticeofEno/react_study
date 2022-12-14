# react_study
리액트 공부 학습자료
일정 분량 이후의 자료들: https://enocent.notion.site/d274a3deeea1474cbac9d73c6cfe9c41

출처 : [https://nextjs.org/learn/foundations/from-javascript-to-react/essential-javascript-react](https://nextjs.org/learn/foundations/from-javascript-to-react/essential-javascript-react)

# 사용되는 Javascript 개념

## 함수

---

### 함수 표현식

```jsx
const square = function (number) {
  return number * number;
}
const x = square(4); // x gets the value 16
```

이름을 제공하면 함수가 자신을 참조할 수 있고 디버거의 스택 추적에서 함수를 더 쉽게 식별할 수 있습니다.

```jsx
const factorial = function fac(n) {
  return n < 2 ? 1 : n * fac(n - 1);
}

console.log(factorial(3))
```

javascript 조건에 따라 함수를 정의 가능

```jsx
let myFunc;
if (num === 0) {
  myFunc = function (theObject) {
    theObject.make = 'Toyota';
  }
}
```

---

### 함수 호이스팅

```jsx
console.log(square(5)); // 25

function square(n) {
  return n * n;
}
```

JavaScript 인터프리터가 전체 함수 선언을 현재 범위의 맨 위로 끌어올리기 때문에 위의 코드는 다음과 동일합니다.

```jsx
// All function declarations are effectively at the top of the scope
function square(n) {
  return n * n;
}

console.log(square(5)); // 25
```

*함수 호이스팅은 함수 선언* 에서만 작동하고 함수 *표현식* 에서는 작동하지 않습니다 . 아래 코드는 작동하지 않습니다.

```jsx
console.log(square); // ReferenceError: Cannot access 'square' before initialization
const square = function (n) {
  return n * n;
}
```

---

### 함수 호출 범위

전역 범위에 정의된 함수는 전역 범위에 정의된 모든 변수에 액세스할 수 있습니다. 

다른 함수 내부에 정의된 함수는 상위 함수에 정의된 모든 변수와 상위 함수가 액세스할 수 있는 다른 모든 변수에도 액세스할 수 있습니다.

```jsx
// The following variables are defined in the global scope
const num1 = 20;
const num2 = 3;
const name = 'Chamakh';

// This function is defined in the global scope
function multiply() {
  return num1 * num2;
}

multiply(); // Returns 60

// A nested function example
function getScore() {
  const num1 = 2;
  const num2 = 3;

  function add() {
    return `${name} scored ${num1 + num2}`;
  }

  return add();
}

getScore(); // Returns "Chamakh scored 5"
```

중첩 함수 및 클로저

```jsx
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}
const fnInside = outside(3); // Think of it like: give me a function that adds 3 to whatever you give it
const result = fnInside(5); // returns 8
const result1 = outside(3)(5); // returns 8
```

---

### 인수객체 사용

이 함수에 원하는 수의 인수를 전달할 수 있으며 각 인수를 문자열 "목록"으로 연결합니다.

```
function myConcat(separator) {
  let result = ''; // initialize list
  // iterate through arguments
  for (let i = 1; i < arguments.length; i++) {
    result += arguments[i] + separator;
  }
  return result;
}
```

```jsx
// returns "red, orange, blue, "
myConcat(', ', 'red', 'orange', 'blue');

// returns "elephant; giraffe; lion; cheetah; "
myConcat('; ', 'elephant', 'giraffe', 'lion', 'cheetah');

// returns "sage. basil. oregano. pepper. parsley. "
myConcat('. ', 'sage', 'basil', 'oregano', 'pepper', 'parsley');
```

---

### Rest Parameters

나머지 [매개변수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) 구문을 사용하면 무한한 수의 인수를 배열로 나타낼 수 있습니다.

다음 예제에서 함수 `multiply`는 *나머지 매개변수* 를 사용 하여 두 번째부터 끝까지 인수를 수집합니다. 그런 다음 함수는 이들에 첫 번째 인수를 곱합니다.

```jsx
function multiply(multiplier, ...theArgs) {
  return theArgs.map((x) => multiplier * x);
}

const arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```

---

### template literals - 문자열 보간

템플릿 리터럴이 없다면 

```jsx
const a = 5;
const b = 10;
console.log("Fifteen is " + (a + b) + " and\nnot " + (2 * a + b) + ".");
// "Fifteen is 15 and
// not 20."
```

있다면

```
const a = 5;
const b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b}.`);
// "Fifteen is 15 and
// not 20."
```

---
---
# 리액트 개념

### React는 사용자를 대신하여 작업을 수행하는 재사용 가능한 코드 스니펫을 포함하는 라이브러리입니다. 이 경우에는 UI를 업데이트합니다.

React 코드 (선언적)

```jsx
<script type="text/jsx">
  const app = document.getElementById("app")
  ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app)
</script>
```

바닐라 javascript코드 (명령적)

```jsx
<script type="text/javascript">
  const app = document.getElementById('app');
  const header = document.createElement('h1');
  const headerContent = document.createTextNode('Develop. Preview. Ship. 🚀');
  header.appendChild(headerContent);
  app.appendChild(header);
</script>
```

---

### React의 핵심 개념 3가지

- Components
    
    React에서 컴포넌트는 **함수입니다.** `script`태그 안에 다음 과 같은 함수를 작성합니다 `header`.
    
    컴포넌트 생성 두가지 방법
    
    1. React 구성 요소는 일반 HTML 및 JavaScript와 구별하기 위해 대문자로 표시되어야 합니다.
    
    ```jsx
    <script type="text/jsx">
      const app = document.getElementById("app")
    
      function Header() {
      return <h1>Develop. Preview. Ship. 🚀</h1>;
    }
    
    // Capitalize the React Component
    ReactDOM.render(Header, app);
    </script>
    ```
    
    1. 꺾쇠 괄호와 함께 일반 HTML 태그를 사용하는 것과 같은 방식으로 React 구성 요소를 사용합니다 `<>`.
    
    ```jsx
    <script type="text/jsx">
      const app = document.getElementById("app")
    
     function Header() {
      return <h1>Develop. Preview. Ship. 🚀</h1>;
    }
    
    ReactDOM.render(<Header />, app);
    ```
    
- Props
- State

---

### JSX 변수 사용
- Props
1. ‘ . ‘ 표기법을 사용 하는 **객체 속성** 

```jsx
function Header(props) {
  return <h1>{props.title}</h1>;
}
```

1. **템플릿** 리터럴 

```jsx
function Header({ title }) {
  return <h1>{`Cool ${title}`}</h1>;
}
```

1. 함수 의 **반환 값**

```jsx
function createTitle(title) {
  if (title) {
    return title;
  } else {
    return 'Default title';
  }
}

function Header({ title }) {
  return <h1>{createTitle(title)}</h1>;
}
```

1. **삼항 연산자** 

```jsx
function Header({ title }) {
  return <h1>{title ? title : 'Default Title'}</h1>;
}
```

## 사용예

```jsx
function Header({ title }) {
  return <h1>{title ? title : 'Default title'}</h1>;
}

function Page() {
  return (
    <div>
      <Header title="React 💙" />
      <Header title="A new title" />
    </div>
  );
}
```


