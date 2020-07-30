---
title: React Native Live Reload
categories:
  - Web
  - React
tags:
  - React
  - Android
  - Live Reload
  - JavaScript
date: 2019-01-08 17:59:53
thumbnail:
---

## Live Reload

리액트 네이티브 기반으로 안드로이드 앱 개발을 할 때 자동으로 리로드 되게 하려면 어떻게 해야 할까. 리액트 기반으로 웹 개발을 할 때에는 코드를 수정 시 자동으로 리로드 되었는데 리액트 네이티브로 개발할 때에 자동으로 되지 않아 검색하던 중 아래 내용 처럼 옵션 설정을 하니까 잘 동작하였습니다.

- 명령 프롬프트에서 다음을 입력하여 장치 또는 에뮬레이터에서 앱을 설치하고 실행합니다.
  `$ react-native run-android`
- 에뮬레이터를 클릭하고 CTRL + M ( MacOS의 경우 CMD + M )을 누르거나 실행 중인 응용 프로그램이 있는 Android 장치를 흔들면 됩니다.
- 팝업 메뉴에서 **Enable Live Reload** 옵션을 선택합니다.

<img width="40%" src="/images/react/enable-reload.png" alt="" title="" >
