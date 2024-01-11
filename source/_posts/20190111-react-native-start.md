---
title: '[React Native] 시작하기'
categories:
  - Programming
  - Mobile
  - React Native
tags:
  - React
  - React Native
  - JavaScript
  - 리액트
date: 2019-01-11 13:20:56
thumbnail: /images/thumbnail/react.png
---

## React Native 란
리액트는 페이스북이 웹 개발을 쉽게 하기 위해 만든 기술입니다. 리액트 네이티브는 리액트의 접근 방법을 모바일로 확장하는 페이스북의 오픈소스 프로젝트입니다.

기존의 하이브리드 앱은 WebView에 화면을 만들어 놓고 모바일 앱에서 접근하는 것이었기 때문에 퍼포먼스가 떨어지고, 모바일 앱과의 괴리감이 있었습니다. 리액트 네이티브는 실제 네이티브 UI를 사용하여 모바일 앱을 구현합니다. 퍼포먼스는 올라가고 괴리감도 사라지게 됩니다.

리액트 네이티브를 사용하면 JavaScript를 사용하여 모바일 앱을 제작할 수 있습니다. 리액트와 동일한 디자인을 사용하여 선언적 구성 요소에서 풍부한 모바일 UI를 구성할 수 있습니다.

출처: [배고픈사자의 React Native [리액트 네이티브]](http://starvinglion-rn.tistory.com/2)

## 장점

- **높은 생산성**
  리액트를 사용하여 개발해 보신분이라면 처음부터 빠르게 개발을 시작할 수 있습니다. 아니라면 처음에 당연히 러닝커브(Learning Curve)는 필요합니다. 그렇지만 Swift, Java 또는 Kotlin, Objective-C를 배우는 것보다 자바스크립트 언어 하나로 작성하기 때문에 생산성이 당연히 좋다고 생각합니다. 그리고 iOS와 Android를 동시에 개발할 수 있다는 점이 매우 큰 장점입니다.

- **라이브 리로딩**
  리액트 네이티브를 사용하면 앱을 더 빠르게 빌드할 수 있습니다. 기존 앱을 개발할 때는 변경되면 다시 빌드를 해야 했지만 리액트 네이티브로 개발할 때 다시 컴파일 하는 대신 즉시 앱을 다시 로드할 수 있습니다. 코드를 수정해서 저장만 하면 변경된 내용을 바로 확인할 수 있어 실제 개발시간을 확실히 단축시킬 수 있습니다.

- **필요한 경우 원시 코드 사용**
  리액트 네이티브는 Swift, Java 또는 Objective-C로 작성된 구성 요소와 원활하게 결합합니다. 애플리케이션의 몇 가지 측면을 최적화해야하는 경우 네이티브 코드로 간단하게 작성할 수 있습니다.

## 단점

- **개발자료 부족**
  시작된지 얼마 되지 않는 프로젝트라서 검색을 하였을 때 확실히 자료가 적은 것 같습니다. 더군다나 영어 자료는 있는데 한글로 된 자료는 더욱 없다고 느껴집니다.

- **힘든 유지보수**
  플랫폼 기기에 대한 문제가 생기면 원인을 찾기가 힘든 것 같습니다. 그리고 국내에 리액트 네이티브 개발자가 많이 없다고 들었습니다. 만약에 리액트 네이티브로 개발을 완료하고 퇴사를 하게 되면 후임자나 유지보수를 해야 하는 개발자를 구해야 하는데 특히 소규모 회사들은 더욱 어렵다고 느껴집니다.

## 비고

위의 단점이 있더라도 장점이 크다고 느껴지고 흥미가 있어 리액트 네이티브에 대해 공부하고 앞으로 있는 새로운 프로젝트에서 사용해 볼 예정입니다.

리액트 네이티브 설치와 실행 및 환경설정은 워낙 정리가 잘 되어있는 블로그가 많아서 따로 정리를 하지 않았습니다. 아래 참고에 되어 있는 링크를 따라가면 window, macOS 환경에서의 설치와 ios, android 플랫폼에서 실행할 수 있도록 잘 설명되어 있습니다. 그리고 리액트 네이티브에 대한 내용과 장단점에 대해서도 참고 링크를 보면 자세하게 볼 수 있습니다.

## 참고

- [React Native 설치와 실행(hello world)](http://yuddomack.tistory.com/entry/1React-Native-%EC%84%A4%EC%B9%98%EC%99%80-%EC%8B%A4%ED%96%89hello-world?category=754156)
- [[RN] React-Native 시작하기](https://medium.com/@jang.wangsu/rn-react-native-%EC%8B%9C%EC%9E%91-3aab881f574f)
- [React Native](https://github.com/facebook/react-native)
- [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started)
- [[RN] React-Native의 장단점은?](https://medium.com/@jang.wangsu/rn-react-native%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90%EC%9D%80-6e8a2396eea1)
