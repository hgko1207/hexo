---
title: '[React] UI 추천'
categories:
  - Programming
  - Frontend
  - React
tags:
  - React
  - Design
  - React UI
  - UI Library
  - 리액트
date: 2020-04-08 17:36:55
thumbnail: /images/thumbnail/react.png
---

**React**로 개발 시 기본적인 디자인을 적용하기 위해 고민이 많이 됩니다. 유료 템플릿 프로젝트를 구매해서 사용할 수 있지만 매번 사는 게 부담이기 때문에 디자인을 하기 무척 힘듭니다.

그래서 검색하던 중에 편리하게 디자인 할 수 있도록 지원해 주는 것들을 몇 가지 찾을 수 있었습니다.

## 1) Ant Design

[![](/images/react/ui/ant.png)](https://ant.design/)

- 리액트와 타입스크립트(Typescript) 기반으로 제작된 UI 라이브러리
- 중국 회사에서 오픈소스화한 라이브러리
- 코드가 리액트 기반이기 때문에 사용하기 편리함

앤트 디자인의 [10가지 디자인 원칙](https://ant.design/docs/spec/proximity)

1. Proximity (근접성)
2. Alignment (정렬)
3. Contrast (대조)
4. Repetition (반복)
5. Make it Direct (직관적으로 만들어라)
6. Stay on the Page (화면에 머물러라)
7. Keep it Lightweight (가볍게 유지하라)
8. Provide an Invitation (가이드를 제공해라)
9. Use Transition (트랜지션을 사용하라)
10. React Immediately (즉각적인 반응)

```shell
$ npm i antd
$ npm i --save @ant-design/icons
```

## 2) Material UI

[![](/images/react/ui/material.png)](https://material-ui.com/)

- 리액트 기반 UI 라이브러리 중에 가장 인기 있고, 성숙한 라이브러리
- 구글 머테리얼 디자인 기반으로 제작

```shell
$ npm install @material-ui/core
```

## 3) React Bootstrap

[![](/images/react/ui/bootstrap.png)](https://react-bootstrap.github.io/)

- 웹 UI 라이브러리로 전세계에서 가장 많이 사용되는 Bootstrap을 리액트 기반으로 변경한 라이브러리
- Bootstrap 3.x 버전을 기반으로 제작된 라이브러리
- Bootstrap 4.x 버전으로 마이그레이션 할 수 있음

```shell
$ npm install react-bootstrap bootstrap
```

## 4) reactstrap

[![](/images/react/ui/reactstrap.png)](https://reactstrap.github.io/)

- Bootstrap 4.x 버전을 기반으로 제작된 라이브러리

```shell
$ npm install --save reactstrap react react-dom
```

## 5) Semantic UI React

[![](/images/react/ui/semantic.png)](https://react.semantic-ui.com/)

- 부트스트랩 만큼이나 인기 있는 Semantic UI의 리액트 버전
- Semantic UI에 jQuery 의존성을 제거하고 순수하게 리액트로만 개발 된 버전

```shell
$ yarn add semantic-ui-react
```
