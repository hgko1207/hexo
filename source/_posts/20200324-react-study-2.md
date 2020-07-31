---
title: React Study(2)
categories:
  - Web
  - React
tags:
  - React
  - Study
  - 리액트
  - JavaScript
  - ES6
date: 2020-03-24 10:41:09
thumbnail: /images/thumbnail/react.png
---

# React 세미나😊(2)

### 2. Project Setup

#### 2.1. Requirements

먼저 Node.js가 설치되어 있어야 합니다.
Node.js 공식 다운로드 페이지([https://nodejs.org/ko/download/](https://nodejs.org/ko/download/))에서 Window Installer를 다운로드하고 설치합니다.

```Bash
# 설치 버전정보 확인
$ node -v
$ npm -v
```

에디터로는 MS에서 제공하는 Visual Studio Code(VS Code)를 사용합니다. vscode는 크로스 플랫폼 에디터로 다양한 언어를 서포트 하며, IntelliSense와 Git 기능, 그리고 Extension을 이용한 확장 기능을 제공하고 있습니다.
설치방법은 https://code.visualstudio.com/ 에 접속하여 다운로드 후 설치하면 됩니다.

> React 개발에 좋은 Extension는 **ESLint**, **Prettier**, **vscode-styled-components**, **Auto Close Tag**, **React-Native/React/Redux snippets for es6/es7** 등 다양하게 있어 설치하고 사용하면 됩니다.

#### 2.2. Creating React App

기존에는 Webpack, Babel 등 필요한 모듈들을 직접 설치하고 설정하느라 상당한 시간이 소요가 되었습니다. 2016년에 React 작업 환경을 명령어 하나로 설정 할 수 있는 공식 도구가 나오면서 개발자들과 입문자들에게 많은 도움이 되었습니다.

먼저 프로젝트 생성을 합니다.

```Bash
# npm 5.2.0+ 설치해야 한다.
# 최신 npm 버전에는 npx가 설치되어 있다.
$ npm install npx -global

$ npx create-react-app test-project

$ cd test-project
$ code .
```

설치가 완료되면 Visual Studio Code 편집기로 프로젝트를 엽니다.
![프로젝트 구조](https://hgko1207.github.io/images/react/react-open.png '프로젝트 구조')
처음 프로젝트가 설치되면 여러가지 파일이 생성되는데 초기 세팅을 위해 불필요한 파일을 제거하는 것이 좋습니다. `src` 폴더에서 App.js, index.js 파일을 제외한 파일을 제거하고 import된 코드를 제거합니다.

### 3. React 개발

#### 3.1. JSX

JSX (JavaScript eXtension)는 자바스크립트 언어 문법의 확장입니다. 자바스크립트 안에서 HTML 문법을 사용해서 화면을 구성할 수 있게 도와주는 문법으로, React 개발에 엄청난 도움을 줍니다.

```jsx
import React, { Component } from 'react';

class HelloMessage extends React.Component {
  render() {
    return (
      // JSX 문법
      <div>Hello {this.props.name}</div>
    );
  }
}

export default HelloMessage;
```

아래는 스타일링의 여러가지 방법입니다.

1. class 대신 className을 사용합니다.
2. 스타일 속성은 중괄호 ({}) 안에 객체 형태로 표시하며 단어 사이의 '-'를 없애는 대신 카멜케이스(Camel Case)를 사용해 CSS 프로퍼티는 나타냅니다.
3. `styled-components`는 리액트 CSS-in-JS 관련 라이브러리 중에서 가장 잘나가는 라이브러리로써 자바스크립트 파일 안에 CSS를 작성하는 형태입니다.

```jsx
// App.js
import React, { Component } from 'react';
import styled from 'styled-components';
import './App.css';

const Content = styled.div`
  background-color: 'blue';
  font-size: 16px;
`;

function App() {
  return (
    <div>
      <div className="App"></div>
      <div style={{ backgroundColor: 'black', fontSize: '12px', color: 'white' }}></div>
      <Content />
    </div>
  );
}
```

```css
// App.css
.App {
  background-color: white;
  font-size: 16px;
  color: black;
}
```

JSX는 꼭 지켜야 할 몇몇 제한이 있습니다.

1. JSX를 사용하는 스크립트 파일은 상단에 React 라이브러리를 꼭 불러와야 합니다.
   ```jsx
   import React from 'react';
   ```
2. 열어 놓은 태그는 꼭 닫아야 합니다.
   ```jsx
   # 에러
   <hello>
   # 정상 동작
   <hello></hello> or <hello />
   ```
3. 최상위 태그는 꼭 1개여야 합니다.
   ```jsx
   <Fragment>
     <header>
       <h1>header</h1>
     </header>
     <main>
       <h1>main</h1>
     </main>
   </Fragment>
   ```

#### 3.2. Component 기반 구조

React는 Component 기반 라이브러리입니다. 하나의 코드로 작성하는 것이 아니라 여러 부분을 분할해서 만들기 때문에 코드의 재사용성과 유지보수성이 증가 됩니다.

```html
<html>
  <head>
    <title>홈페이지</title>
  </head>
  <body>
    <header>
      <!-- 헤더 내용 -->
    </header>
    <div class="content-list">
      <!-- 콘텐츠 리스트 -->
    </div>
    <footer>
      <!-- 푸터 내용 -->
    </footer>
  </body>
</html>
```

위와 같은 html코드가 있다고 해봅시다. 이를 React로 만들게 되면 다음과 같습니다.

```jsx
import React, { Component } from 'react';
import Header from './component/Header';
import Footer from './component/Footer';
import ContentList from './component/ContentList';

class App extends Component {
  render() {
    return (
      <div>
        <Header />
        <ContentList />
        <Footer />
      </div>
    );
  }
}

export default App;
```

Header나 Footer, ContentList 등은 컴포넌트로 만들고, 이를 조립해서 루트 컴포넌트를 만드는 방식입니다. 컴포넌트의 종류로는 `클래스형(stateful)`과 `함수형(stateless)`으로 나누어집니다.

#### 3.3. Props

`props`란 부모 컴포넌트에서 자식 컴포넌트로 전달해 주는 데이터를 말합니다.
`props`는 읽기 전용 데이터라고 생각하면 됩니다. 자식 컴포넌트에서 전달 받은 `props`를 변경이 불가능하고 `props`를 전달해준 최상위 부모 컴포넌트만 `props`를 변경할 수 있습니다.

#### 3.4. State

`state`는 동적인 데이터를 다룰 때 사용합니다. 사용자와의 상호작용을 통해 데이터를 동적으로 변경을 해야 할 때 사용합니다.  
`state`는 `클래스형 컴포넌트`에서만 사용할 수 있는데 각각의 `state`는 독립적이라  
다른 컴포넌트의 직접적인 접근은 불가능하다.

#### 3.5 LifeCycle API

LifeCycle API는 컴포넌트가 DOM 위에 생성되기 전 후 및 데이터가 변경되어 상태를 업데이트하기 전 후로 실행되는 메소드들 입니다. 자원낭비를 줄이기 위하여 코드를 최적화 할 때 사용됩니다. 많이 사용하는 LifeCycle 메소드들은 `constructor`, `componentDidMount`, `render`, `shouldComponentUpdate` 입니다.

## 참고

- [VS Code 기본 세팅](https://gomcine.tistory.com/entry/VS-Code-%EA%B8%B0%EB%B3%B8-%EC%84%B8%ED%8C%85?category=624630)
- [vscode 추천 익스텐션(Extensions)과 세팅](https://caesiumy.github.io/2019/04/02/vscode-recommended-extensions/)
- [craete-react-app github](https://github.com/facebook/create-react-app)
- [React 시작하기](https://reactjs-kr.firebaseapp.com/docs/installation.html)
- [[npm] 🤔npx란 무엇인가?](https://geonlee.tistory.com/32)
- [JSX 소개 - React](https://reactjs-kr.firebaseapp.com/docs/introducing-jsx.html)
- [누구든지 하는 리액트 3편: JSX](https://velopert.com/3626)
- [리액트 Styled Components - 1편](https://velog.io/@taewo/%EB%A6%AC%EC%95%A1%ED%8A%B8-Styled-Components-76jsolbaf8)

## 강의

- https://academy.nomadcoders.co/
- https://www.opentutorials.org/module/4058
