# react_study
리액트 공부 학습자료

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
