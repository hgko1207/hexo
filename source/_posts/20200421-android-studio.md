---
title: '[Android Studio] 설치 및 주요 기능'
categories:
  - Programming
  - Mobile
  - Android
tags:
  - Android
  - Android Studio
date: 2020-04-21 09:49:50
thumbnail: /images/thumbnail/androidstudio.png
---

## 1. Android Studio 다운로드 및 설치

아래 경로에서 최신 버전의 Android Studio를 다운받아 설치합니다. 현재 최신은 3.6.3 버전입니다.

[![](/images/studio/download.png)](https://developer.android.com/studio)

설치를 완료하고 다음 화면이 오픈되면 이제 개발을 시작할 수 있습니다.

![](/images/studio/start.png)

## 2. 프로젝트 생성

1. **Start a new Android Studio Project** 선택
2. Slelect a Project Templat
   - Empty Activity 선택
3. Configure Your Project
   - Name: HelloApp
   - Package: com.hgko.helloapp
   - Language: Java or Kotlin
   - Minimum SDK: API 26: Android 8.0(Oreo)
4. **Finish** 버튼 클릭하면 아래처럼 프로젝트가 생성됩니다.

![](/images/studio/project.png)

## 3. 실행

### 1) 스마트폰 연결 시

1. 스마트폰에서 USB 디버깅 설정
   설정 > 빌드 번호 6번 터치 -> 개발자 옵션 화성화(메뉴가 보임) > USB 디버깅 활성화 선택
2. 스마트폰 케이블 연결
3. logcat에서 디바이스 연결 확인

### 2) 가상 디바이스 사용 시

1. **Tools > AVD Manager**
2. Create Virtual Device... 클릭
3. Select Hardware
   - 적당한 디바이스를 선택한다.
   - 예) Phone > Pixel XL
4. System Image
   - Android 버전을 선택
5. **Finish** 버튼 클릭

스마트폰 또는 가상 디바이스를 연결 후 상단 툴바에서 장비를 선택 후 `Run`을 클릭하면 컴파일이 되며, 앱이 설치되고 구동됩니다.

<img width="95%" src="/images/studio/run.png" alt="" title="" >

## 4. SDK 설치

**Tools > SDK Manager** 에서 설치 현황 및 안드로이드 버젼별 SDK 설치/삭제/업데이트 등을 수행할 수 있습니다.

<img width="100%" src="/images/studio/sdk.png" alt="" title="" >

## 5. Device File Explorer

연결된 장비(스마트폰 or 가상 디바이스)의 파일 시스템을 탐색하는 뷰를 제공합니다.
**View > Tool Windows > Device File Explorer** 메뉴를 클릭하여 아래와 같이 Device File Explorer 뷰를 오픈합니다.

<img width="90%" src="/images/studio/deviceFile.png" alt="View > Tool Windows > Device File Explorer 메뉴" title="" >

<img width="90%" src="/images/studio/deviceExplorer.png" alt="Device File Explorer 뷰" title="" >

디바이스 파일 중에 특히 다음과 같은 경로들이 유용합니다.

**1) data/data/app_name/**
내부 저장소에 저장괸 입의 데이터 파일 경로

**2) sdcard/**
외부 사용자 SD 카드에 저장된 파일(사진 등) 경로

## 6. 주요 단축키

참고 : [Android 스튜디오 단축키](https://developer.android.com/studio/intro/keyboard-shortcuts?authuser=1&hl=ko)

| 설명                | 단축키                       |
| ------------------- | ---------------------------- |
| 기본 코드 완성      | Ctrl+Space                   |
| 스마트 코드 완성    | Ctrl+Shift+Enter, Ctrl+Enter |
| 자동 Import         | Alt+Enter                    |
| 주석                | Ctrl+/                       |
| 블록 주석           | Ctrl+Shift+/                 |
| 빌드                | Ctrl+F9                      |
| 복사                | F5                           |
| 코드 서식 자동 지정 | Ctrl+Alt+L                   |
| 자동 들여 쓰기      | Ctrl+Alt+I                   |

## 7. 자동 import 설정

**Alt + Enter**를 입력하지 않아도 클래스 사용시 자동으로 import 문을 추가해 주는 기능입니다.
**File > Settings > Editor > General > Auto Import** 에서 다음과 같이 "Add unambiguous..."와 "Optimize imports..." 를 체크합니다.

<img width="100%" src="/images/studio/import.png" alt="" title="" >

## 8. 새로운 개념/기능

### 1) ART VM

안드로이드는 이전 가지는 DVT에서 구동되었으나 현재는 ART라는 VM을 이용합니다. ART는 JIT(Just In Time, 실행 시 컴파일 방식으로 2.2 버젼부터 지원)을 지원하는 VM들과 달리 앱이 설치 시 전체 바이트 코드가 기계어로 컴파일되는 AOT(Ahead Of Time)를 이용하므로 획기적으로 성능이 개선되었습니다.

### 2) App Bundle

안드로이드 앱 내보내기에 기존 APK 파일 외에 앱 번들이 추가되었습니다. Google Play의 새로운 앱 제공 모델인 Dynamic Delivery는 App Bundle을 사용하여 각 사용자의 기기 설정에 최적화된 APK를 생성하고 제공하므로, 사용자는 앱 실행에 필요한 최소한의 코드와 리소스만 다운로드하면 됩니다.

개발자가 더 이상 다양한 기기를 지원하기 위해 여러 개의 APK를 빌드하고 서명하고 관리할 필요가 없으며 사용자는 더 작고 최적화된 앱을 다운로드할 수 있습니다.

또한 앱 프로젝트에 동적 기능 모듈을 추가하여 App Bundle에 포함할 수 있습니다.
모듈의 일부 기능과 자원(동영상, 이미지 등)들은 사용자가 처음 앱을 다운로드하고 설치할 때 포함되지 않도록 할 수 있습니다.

나중에 앱에서 Play Core 라이브러리를 사용하여 이러한 모듈을 동적 기능 APK로 다운로드하도록 요청할 수 있습니다.

정리하면 App Bundle로 내보내기를 추천합니다.
