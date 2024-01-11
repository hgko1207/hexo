---
title: React Study(1)
categories:
  - Programming
  - Frontend
  - React
tags:
  - React
  - Study
  - 리액트
  - JavaScript
  - ES6
date: 2020-03-24 10:39:16
thumbnail: /images/thumbnail/react.png
---

# React 세미나😊(1)

최근 React를 다시 공부하게 되면서 올해 초에 회사에서 세미나를 하게 되었다. 물론 기초이지만 React 에 관심을 다시 가지게 되는 계기가 되었다.

## React란?

[React](https://ko.reactjs.org/)는 페이스북에서 제공해 주는 프런트엔드 라이브러리다. 사용자 인터페이스(User Interface)에 집중하며, Virtual DOM을 통해 속도와 편의를 높이고, 단방향 데이터 플로우를 지원하여 [보일러플레이트 코드](http://web-front-end.tistory.com/27)를 감소 시켜준다. React 는 싱글 페이지 애플리케이션(SPA)이나 모바일 애플리케이션을 개발할 때 사용할 수 있다.

#### 특징

- 컴포넌트 기반 아키텍처
  - 템플릿 언어가 아닌 자바스크립트로 컴포넌트 작성
  - 특정 관심사에 집중된 기능 블록 (관심사의 분리)
- One Way Data flow(단방향 데이터 흐름 지향)
- React 는 데이터의 흐름이 한 방향으로만 흐흔다.
- 데이터가 내려가기만 하고 밑에서 데이터를 올릴 수 없다.
- 그래서 부모의 데이터를 바꿔주기 위해서는 `state`를 이용해야 한다.
- Virtual DOM - React는 가상의 DOM을 만들어서 진짜 DOM 과 비교하여 변경 사항이 있을 경우 전체를 새롭게 만드는 것이 아니라 변경된 부분만 진짜 DOM 에 반영하는 방식으로 작업을 수행한다. 그럼으로써 애플리케이션의 효율성과 속도를 높일 수 있게 된다.
- JSX 문법

#### 리액트 JS를 하기 위해 알아야 할 것

- Javascript(ES6)
- HTML
- CSS

### 1. Fundamentals(기초)

**React**에서 많이 사용되는 자바스크립트 ES6 문법 기초를 먼저 알아보자.

- 기존에 우리가 웹 개발에서 많이 보던 자바스크립트는 2009년 12월에 나온 **ECMAScript5(ES5)** 버전이다. 최근 Node.js, react에서는 2015년 6월에 업데이트된 **ECMAScript6(ES6)** 문법의 자바스크립트를 사용하고 있다.
- ES6 문법을 사용하면서 처음에는 익숙해지기 어려웠지만 사용할 수록 코드가 간결해지고 깔끔해지면서 가독성이 좋아졌고, 모듈 별로 개발하면서 코드 관리가 쉬워졌다.
- 현재는 ES8까지 업데이트 되었지만 몇 가지 걸림돌이 있어 넘어가지 않고 있다.

아래에는 바뀐 ES6 문법과 많이 사용되는 기능들이다.

#### 1.1. var -> let & const

_const_ 는 블록 범위이며 값이 지정되면 나중에 바꿀 수 없다. 또한, 재 선언 될 수도 없다.
_let_ 은 블록 범위이며 값이 지정되어도 값을 바꿀 수 있다.

```js
const name = 'eden';
let tel = '010-0000-0000';
```

#### 1.2. Arrow Functions

함수는 간결해지고 코드는 짧아졌다.
Argument가 하나 일 때는 괄호가 필요 없다.(유일한 규칙)

```js
// ES5
function sayHello(name) {
	reutn "Hello " + name;
}
// ES6
const sayHello = name => "Hello " + name;
const sayHello = (name, something) => "Hello " + name + something;
```

#### 1.3. [Template Literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

``(backticks) 사용

```jsx
const name = 'eden';
// ES5
console.log('Hello ' + name);
// ES6
console.log(`Hello ${name}`);
```

#### 1.4. Object Destructuring (비구조화)

적은 코드를 사용해서 더 깔끔하게 보이도록 한다.

```js
const human = {
  name: 'Ko',
  lastName: 'HyeongGyun',
  nationality: 'Korea',
  favFood: {
    dinner: 'Samgyupsal',
  },
};

// ES5
const name = human.name;
const lastName = human.lastName;
const difName = human.nationality;
const dinner = human.favFood.dinner;
// ES6
const {
  name,
  lastName,
  nationality: difName,
  favFood: { dinner },
} = human;

console.log(name, lastName, difName, dinner);
```

#### 1.5. Spread Operator

Iterable Object(열거 가능한 오브젝트)를 하나씩 전개한다.
표현방식 […iterable], 변수 앞에 '…' 찍어서 선언한다.
변수뿐만 아니라 Argument, Function에서도 쓰인다.

```js
const days = ['Mon', 'Tues', 'Wed'];
const otherDays = ['Thu', 'Fri', 'Sat'];
const allDays = [...days, ...otherDays, 'Sun'];
console.log(allDays);

결과: ['Mon', 'Tues', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
```

#### 1.6. Classes

constructor 메서드도 사용할 수 있고 extends를 통해서 클래스 상속도 가능하다.

```js
class Human {
  constructor(name, lastName) {
    this.name = name;
    this.lastName = lastName;
  }
}

class Baby extends Human {
  cry() {
    console.log('cry');
  }
  sayName() {
    console.log(`My name is ${this.name}`);
  }
}

const myBaby = new Baby('mini', 'me');
console.log(myBaby.cry(), myBaby.sayName());
```

#### 1.7. [Array.map](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

요소를 일괄적으로 변경한다.

```js
const days = ['Mon', 'Tues', 'Wed', 'Thu', 'Fri'];
const smilingDays = days.map((day) => `😂 ${day}`);
console.log(smilingDays);

결과: ['😂 Mon', '😂 Tues', '😂 Wed', '😂 Thu', '😂 Fri'];
```

#### 1.8. [Array.filter](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

요소를 걸러내어 배열로 true/false 반환, 없으면 빈 배열을 반환한다.

```js
const numbers = [123, 5, 15, 67, 241, 54, 1, 6, 23, 90];
const otherNumbers = numbers.filter((number) => number > 15);
console.log(otherNumbers);
```

#### 1.9. forEach, includes, push

```js
let posts = ['Hi', 'Hello', 'Bye'];

if (!posts.includes('new')) {
  posts.push('new');
}
posts.forEach((post) => console.log(post));
```

## CodeSandbox

- 웹 기반 자바스크립트 에디터 서비스를 제공하는 사이트
- 간단한 소스 코드 테스트를 할 때 사용하면 편리하다.
- [codesandbox.io](https://codesandbox.io/s/es6-fundamentals-d4i70)

## 참고

- https://velog.io/@stampid/React%EB%9E%80
- https://velog.io/@kyusung/react-summary
- https://hgko1207.github.io/2019/01/09/react-start/
- https://sanghaklee.tistory.com/54
- http://woowabros.github.io/experience/2017/12/01/es6-experience.html
- https://blog.asamaru.net/2017/08/14/top-10-es6-features/
- https://velog.io/@decody/map-%EC%A0%95%EB%A6%AC
