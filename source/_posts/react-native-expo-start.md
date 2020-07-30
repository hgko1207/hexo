---
title: React Native Expo 사용
categories:
  - Web
  - React
tags:
  - React
  - React Native
  - Expo
  - JavaScript
  - Node.js
  - Expo Cli
date: 2019-01-11 16:35:26
thumbnail:
---

# Expo

리액트 네이티브는 리액트 아키텍처를 모바일에 적용한 것으로, ES6 문법과 리액트를 이용해 모바일 어플리케이션을 개발할 수 있도록 해주는 프레임워크입니다. 리액트 네이티브 프로젝트 생성 시 `react-native init <프로젝트 이름>`을 입력하여 사용하였습니다. 이것만으로도 충분하다고 느껴졌는데 다른 강좌를 보던 중에 Expo 툴을 발견하게 되었습니다.

**[Expo](https://expo.io/)**는 리액트 네이티브 어플리케이션의 빌드를 돕는 툴 입니다. 네이티브 API에 접근하는 것도 쉽게 만들어주고, 안드로이드와 iOS 버전을 알아서 빌드해줍니다. 무엇보다 코드를 수정하면 바로 hot reloading 시켜주는 것이 가장 편합니다.

작년 12월 쯤에 리액트 네이티브를 알게 되고 최근에 Expo도 접하게 되면서 찾던 중 처음에는 Expo Xde를 다운받아 사용하라고 하여서 Expo 홈페이지를 찾아봤지만 다운받지 못하였습니다. 그러던 중 xde 지원이 중단되고 대신 Expo dev tool(=expo cli 최신버전)을 설치해서 사용하라고 하는 내용을 보게 되었습니다.

## Expo cli 설치 및 실행

### 1. node.js 설치

이전 글인 **_리액트 시작하기_** 를 참고합니다.
[> [Programming/React/리액트 시작하기] - Node.js 설치: Windows](https://hgko1207.github.io/2019/01/09/react-start/)

### 2. expo-cli 설치

터미널(또는 명령프롬프트) 창을 열고, 다음 명령어를 입력하여 실행합니다.

```bash
$ npm install -g expo-cli
```

### 3. 프로젝트 생성

프로젝트 생성할 때는 `expo init <프로젝트 이름>` 명령어를 사용합니다.
init 입력 후 프로젝트 개발 목적에 맞게 선택 합니다. 그런다음 **_Use Yarn to install dependencies?_** 하는 질문에 **Y** 를 입력하고 엔터를 입력합니다. 그러면 설치가 시작되고 완료 후 프로젝트가 정상적으로 생성이 되었는지 확인합니다.

```bash
$ expo init react-native-project
```

<img width="100%" src="/images/react/react-expo-init.png" alt="프로젝트 생성 선택" title="" >

### 4. 프로젝트 실행

프로젝트를 실행하면 새 탭이 생성되면서 아래 그림처럼 보여집니다.

```bash
$ cd react-native-project
$ expo start
```

<img width="100%" src="/images/react/react-expo-start.png" alt="프로젝트 실행 화면" title="" >

### 5. 모바일 디바이스 연결

- **실제 모바일 디바이스**
  먼저 [Expo](https://expo.io/) 홈페이지에서 계정을 생성합니다. 그런 다음 모바일에서 **_"Expo client"_** 앱을 설치합니다. 그리고 프로젝트 실행 화면에서 **_Publish or republish project..._** 을 클릭하고 내용을 입력 후 **_Publish Project_** 버튼을 클릭합니다.

<img width="100%" src="/images/react/react-expo-start-app.png" alt="모바일 디바이스 연결" title="" >

클릭하는 순간 터미널(또는 명령프롬프트)에 계정 정보를 입력하라는 문구가 뜹니다. 그럼 생성한 계정정보를 입력 후 엔터키를 누르고 프로젝트 실행 화면으로 넘어와서 성공했는지 확인을 합니다.

<img width="100%" src="/images/react/react-expo-start-app1.png" alt="모바일 디바이스 연결 성공 확인" title="" >

**_"Expo client"_** 앱을 실행하고 생성한 계정정보를 입력합니다. 로그인 성공 후 하단에 있는 **_Projects_** 탭을 클릭합니다. 그러면 Publish 성공한 프로젝트가 보입니다. 프로젝트를 클릭하면 우리가 작업한 화면이 보일 것 입니다. 코드를 수정하면 바로 앱에서 변경되는 것을 확인할 수 있습니다.

<img width="95%" src="/images/react/react-expo-start-app2.png" alt="Expo client 앱 화면" title="" >

**이슈사항**은 모바일 디바이스와 연결 시 같은 망의 네트워크여야 하는 것 같습니다. QR Code로 하는 방법도 있는 것 같은데 아직 시도를 못 해봤습니다.

- **에뮬레이터**
  iOS는 Xcode를 설치하고 Android는 Android Studio를 설치하고 AVD manager에서 디바이스를 생성 후 실행시켜줍니다. 그런다음 프로젝트 실행 화면에서 **_"Run on Android device/emulator"_** 또는 **_"Run on iOS simulator"_** 를 클릭합니다. 자동으로 에뮬레이터에 앱이 설치가 되고 실행이 됩니다. 그리고서 실행된 화면을 확인하고 코드를 변경해 보세요. 라이브 리로드 설정이 되어있으면 바로 리로드가 되는 것을 확인할 수 있습니다.<br>
  에뮬레이터 연결은 Expo 뿐만 아니라 앱 개발할 때 자주 사용하기 때문에 따로 설명은 없고 아래 링크에서 가이드를 보면 나와있습니다.<br>
  [> 모바일 클라이언트 : iOS 및 Android 에뮬레이터](https://docs.expo.io/versions/v32.0.0/introduction/installation)

## 참고

- [Expo Quick Start](https://docs.expo.io/versions/v32.0.0/)
- [Expo Xde 지원 중단에 따른 Expo dev tool(Expo cli) 설치 및 실행 방법](http://codinghub.tistory.com/48)
