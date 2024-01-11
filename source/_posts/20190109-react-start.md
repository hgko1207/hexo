---
title: '[React] 설치 및 설정 방법'
categories:
  - Programming
  - Frontend
  - React
tags:
  - React
  - JavaScript
  - Node.js
  - VSCode
  - 리액트
date: 2019-01-09 14:10:34
thumbnail: /images/thumbnail/react.png
---

## 리액트란

**React**는 사용자 인터페이스를 만들기 위해 페이스북과 인스타그램에서 개발한 오픈소스 자바스크립트 라이브러리로써, 사용자 인터페이스(User Interface)에 집중하며, Virtual DOM을 통해 속도와 편의를 높이고, 단방향 데이터플로우를 지원하여 [보일러플레이트 코드](http://web-front-end.tistory.com/27)를 감소시켜, 많은 사람들이 React를 MVC의 V를 고려하여 선택한다. 즉, React는 지속해서 데이터가 변하는 대규모 어플리케이션의 구축이라는 하나의 문제를 풀기 위해서 만들어졌다. 아래는 React에서 장점들이다.

- **단순함** : 당신의 어플리케이션이 어떤 주어진 시점에 어떻게 보여야 할지를 단순하게 표현함으로써, React는 그 데이터들이 변할 때, 자동적으로 모든 UI 업데이트들을 관리할 것이다.
- **선언적인 문법** : 데이터가 변할 때, React는 개념적으로 ‘새로고침’ 버튼을 눌러서, 변화된 부분을 알아채 업데이트하게 된다.
- **구성적인 컴포넌트 개발** : React는 재사용가능한 컴포넌트들을 개발하기 위한 모든 것이다. 사실, React로 당신이 할 수 있는 오직 한 가지는 컴포넌트를 개발하는 것이다. 그것들은 캡슐화되어있기 때문에, 컴포넌트들은 재사용될 수 있고, 테스트될 수 있으며, 관심의 분리(seperation of concerns)를 지키게 해 준다.

## 설치하기

리액트를 설치하고 프로젝트를 만들어 보자.
리액트 프로젝트를 만들 때는 Node.js 와 npm을 반드시 먼저 설치해야 한다. Node.js는 크롬 V8 자바스크립트 엔진으로 빌드한 자바스크립트 런타임이다. 2009년 Node.js를 출시한 이후 자바스크립트는 웹 브라우저 영역 외에 웹 서버는 물론, 모바일 애플리케이션, 데스크톱 애플리케이션 영역에서도 엄청나게 활약할 수 있게 되었다.

### 1. Node.js 설치: Windows

Node.js 공식 다운로드 페이지(https://nodejs.org/ko/download/)에서 Windows Installer를 다운로드하고 설치한다.

[![Windows Installer를 클릭하여 다운로드](/images/react/nodejs-download.png)](https://nodejs.org/ko/download/)

설치가 끝나면 터미널(또는 명령프롬프트) 창을 열고, 다음 명령어를 실행하여 제대로 설치했는지 확인한다.

```shell
$ node -v
v10.15.0
```

### 2. 에디터 설치

리액트 애플리케이션을 만들면서 코드를 수정할 때는 코드 에디터를 설치하여 사용하는 것이 편하다. 브래킷(Bracket), 아톰, VS Code를 써본 결과 모든 운영체제를 지원하는 **VS Code**를 사용하고 있다.

VS Code 공식 다운로드 페이지(https://code.visualstudio.com/Download)에서 운영체제에 맞는 버전을 설치한다. 여기서는 Windows 버전을 설치한다. 이 에디터는 macOS, Window, 리눅스를 모두 지원한다.

[![Visual Studio Code 다운로드](/images/react/vscode-download.png)](https://code.visualstudio.com/Download)

### 3. create-react-app 설치

**create-react-app** 도구는 npm으로 설치할 수 있다. 패키지를 설치하는 방법은 두 가지가 있는데, 첫 번째는 지역적으로 설치하는 것이고, 두 번째는 전역적으로 설치하는 것이다. create-react-app은 커맨드라인 도구라서 모든 디렉터리에서 필요하므로 전역적으로 설치한다.

```shell
$ npm install -g create-react-app
```

## 프로젝트 생성

프로젝트 생성할 때는 `create-react-app <프로젝트 이름>` 명령어를 사용한다.

```shell
$ create-react-app test-react
$ cd test-react
$ npm start
```

`npm start` 실행하여 완료했다면 http://localhost:3000/ 로 접속하여 확인한다.

<img width="75%" src="/images/react/react-run.png" alt="초기 프로젝트 페이지" title="" >

## 프로젝트 구조

VS Code를 실행하여 만들어진 test-react 프로젝트를 열면 다음과 같은 구조로 만들어져 있다. 이미 modules 가 설치되어 있고, 의존성 패키지는 대부분 `node_modules/react-scripts` 모듈 내에 선언되어 있다. `src` 폴더안에 있는 파일들을 추가하고 수정하면서 개발을 하면 된다.

![프로젝트 구조](/images/react/react-open.png)

## 정리

리액트에 관심이 생겨 책을 읽고 검색한 내용들을 모아서 리액트에 대한 설명부터 설치, 프로젝트 실행까지 간략하게 설명하였다. 현재는 리액트를 공부하면서 정리하는 단계라서 현업에서 리액트 라이브러리를 사용하면서 겪는 이슈사항이나 팁은 추후에 정리할 예정이다.

## 참고

- [React 시작하기](http://webframeworks.kr/getstarted/reactjs/)
- [[ReactJs] create-react-app으로 react 시작하기](https://blueshw.github.io/2017/06/20/create-react-app/)
- [[React] 1. 리액트 시작하기](https://blog.sonim1.com/174)
- [개발 관련 강좌 사이트](https://www.inflearn.com/)
- [리액트를 다루는 기술 출간 / 집필후기](https://velopert.com/3697)
