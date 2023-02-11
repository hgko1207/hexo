---
title: 이클립스 플러그인 추가
categories:
  - Programming
  - Eclipse RCP
tags:
  - Eclipse
  - RCP
  - Java
  - Plugin
  - 이클립스
  - 자바
date: 2019-01-07 18:25:03
thumbnail: /images/thumbnail/rcp.png
---

# Eclipse Piug-in 추가

Eclipse에 플러그인을 추가하는 방법에는 두 가지가 있습니다. 첫 번째 방법은 플러그인을 직접 복사해서 설치하는 방법이고, 두 번째 방법은 Eclipse에서 제공하는 Software Update Manager를 활용하는 방법입니다.

### 직접 복사하는 방법

설치하고자하는 플러그인을 Eclipse_home/plugin 디렉토리에 복사한 다음 Eclipse를 재시작하면 새롭게 설치된 Eclipse 플러그인 기능을 활용할 수 있습니다.

### Software Update Manager를 활용하는 방법

Eclipse에서 제공하는 Software Update Manager 기능은 플러그인을 개발한 곳에서 이 기능을 사용할 수 있도록 지원하지 않으면 사용할 수 없습니다.

Eclipse에서 `Help->Install New Software`로 이동 후 설치 할 플러그인 URL를 입력하여 다운받습니다.

또 다른 방법은 `Help->Eclipse Marketplace`로 이동 후 설치 플러그인을 검색 후 다운받습니다.

# 이클립스 RCP

## Piug-in 구조

모든 플러그인의 실제 동작에 대한 정의는 코드에 들어있지만, 플러그인의 종속성과 서비스는 `MANIFEST.MF`와 `plugin.xml` 파일에서 선언합니다. 이런 구조 덕분에 플러그인 코드가 당장 필요한 순간이 되어서야 로딩되는 늦은 로딩(lazy loading)이 가능하며, 이에 따라 이클립스의 시동 시간과 메모리 사용량을 줄일 수 있습니다.

이클립스 시동될 때는 플러그인 로더가 각 플러그인에 대한 `MANIFEST.MF`와 `plugin.xml` 파일 전부를 훑어본 다음, 플러그인에 대한 정보를 포함하는 구조체를 구성합니다.

## Piug-in 선언(MANIFEST.MF)

각 번들 내역서 내에는 이름, ID, 버전, 플러그인 클래스, 프로바이더에 대한 항목이 들어 있습니다.

### 1. Piug-in ID

플러그인 ID(Bundle-SymbolicName)는 단 하나의 플러그인을 식별하기 위해 설계된 것이며 일반적으로 자바 패키지 이름 규약(예: com.<회사명>.<제품명>)을 이용해 구성됩니다.

### 2. Piug-in 버전

플러그인에 지정된 버전(Bundle-version)은 항상 3개의 수를 점으로 구분해 나열한 것 입니다. 첫 번째 수는 주 버전(major version)을 의미하며 두 번째는 부 버전(minor version), 세 번째는 서비스 레벨을 의미합니다.

### 3. Piug-in 이름과 제공자

이름과 제공자는 둘 다 사람이 읽기 위한 텍스트이므로 어떻게 입력하든지 상관없고 또한 유일할 것일 필요도 없습니다.

### 4. Piug-in 클래스 선언

모든 플러그인은 필요한 경우에 플러그인 클래스(Bundle-Activator)를 지정할 수 있습니다.

### 5. Piug-in 런타임

`MANIFEST.MF` 파일의 Bundle-ClassPath 선언에는 플러그인 코드에 포함된 라이브러리(\*.jar 파일) 를 콤마(‘ , ‘)로 구분해 나열합니다. Bundle-ClassPath에서 정의한 라이브러리에 들어있는 패키지를 다른 플러그인에서 접근 할 수 있게 지정하려면 ExportPackage 선언을 써서 접근 가능하게 할 패키지를 콤마 구분 목록으로 지정합니다.

### 6. Piug-in 종속성

플러그인 로더는 각 로딩된 플러그인마다 개별 클래스 로더의 인스턴스를 생성하며 내역서의 Require-Bundle 선언을 사용해 해당 플러그인이 실행 중 참조해야 할 플러그인이 어느 것인지를 지정합니다.

## Piug-in 모델

이클립스는 처음 실행될 때 각 플러그인 디렉토리를 모두 돌아본 다음, 찾아낸 개별 플러그인을 표현하는 내부 모델을 구성합니다. 개별 플러그인 전체를 로딩하지 않으며 플러그인 내역서만 검토합니다.

### 1. Platform

`org.eclipse.core.runtime.Platform` 클래스는 현재 실행 중인 이클립스 환경에 대한 정보를 제공합니다. 이 클래스를 사용해 설치되어 있는 플러그인(번들), 확장, 확장점, 명령행 인자, 작업 관리자 등의 정보를 얻을 수 있습니다.

### 2. Piug-in 과 번들

`Platform.getBundleGroupProviders()` 나 `Platform.getBundle(String)`을 사용해 현재 설치된 플러그 인(번들)에 대한 정보를 얻을 수 있습니다. 플러그인 클래스, 즉 번들 액티베이터에 접근하려면 해당 플러그인을 로드해야 하지만 Bundle 인터페이스에는 별도의 부담 없이 접근할 수 있습니다.

### 3. Piug-in 확장 레지스트리

`Platform.getExtensionRegistry()` 메소드를 사용해서 플러그인 확장 레지스트리(extension registry)에 접근할 수 있습니다. 확장 레지스트리에는 각 플러그인을 표현하는 플러그인 디스크립터가 포함되어 있으며 플러그인을 로딩하지 않고도 다양한 플러그인 정보를 얻을 수 있는 메소드를 제공합니다.

# Piug-in 개발

## Piug-in Project 생성

New -> Plug-in Project 클릭합니다.

<img width="55%" src="/images/rcp/rcp1.png" alt="" title="" >

_Project name_ 입력 후 Next 클릭합니다.

<img width="55%" src="/images/rcp/rcp2.png" alt="" title="" >

1. ID에 패키지명 입력
2. Activator 패키지 명을 1)번에 입력한 패키지명과 같도록 입력
3. No 버튼 클릭 후 Next 클릭

<img width="55%" src="/images/rcp/rcp3.png" alt="" title="" >

“Hello, World Command” 선택 후 Finish 클릭합니다.

<img width="100%" src="/images/rcp/rcp4.png" alt="" title="" >

위와 같이 플러그인 프로젝트가 생성되면 **MANIFEST.MF 클릭 -> Extensions** 탭으로 이동 기본적으로 “Hello, World Command”를 선택하면 commands, handlers, bindings, menus 4개의 트리가 만들어집니다.

Commands는 실제 동작으로부터 독립적이며 선언적이고, `org.eclipse.ui.commands` 확장점을 통하여 정의되어 있습니다. 그리고 단축키(Key Binding)가 정의될 수 있고, 커맨드의 행동은 핸들러를 통하여 정의됩니다.

Handlers는 commands로부터 명령을 받아 호출되고, 호출되자마자 클래스를 실행합니다. 클래스를 정의할 때 `org.eclipse.core.commands.AbstractHandler` 클래스를 상속받습니다.

<img width="75%" src="/images/rcp/rcp5.png" alt="" title="" >

`Execute()` 메소드는 핸들러가 실행되면 호출 되며, HandlerUtil 클래스를 통하여 서비스에 접근할 수 있습니다.

- Bindings는 메뉴에 단축키를 지정할 수 있습니다.
- Menus는 애플리케이션 메인 메뉴, 툴바, 뷰 툴바, 팝업메뉴를 만들 수 있습니다.

<img width="65%" src="/images/rcp/rcp6.png" alt="" title="" >

`org.eclipse.ui.menus` 에서 menuContribution는 사용자 인터페이스에서 메뉴가 표시되는 위치를 정의할 수 있는 locationURI 속성을 가지고 있습니다. locationURI 속성에는 기본적으로 menu:와 toolbar:, popup: 으로 시작하며 그 다음에는 메뉴가 표시될 위치를 지정할 수 있습니다. 예를 들어, 파일 메뉴(ID:fileMenu)의 하의 메뉴에 위치시키려면 아래와 같은 위치식을 이용합니다.
예) menu:fileMenu?after=addition

## Piug-in 배포

플러그인을 만들었으면 jar로 생성해야 합니다.

<img width="80%" src="/images/rcp/rcp7.png" alt="" title="" >

**Export -> Plug-in Development -> Deployable plug-ins and fragments** 선택 후 Next 클릭합니다.

<img width="75%" src="/images/rcp/rcp8.png" alt="" title="" >

배포하는 플러그인 프로젝트를 선택하고, Directory란에 배포하는 폴더를 지정하고, Finish를 클릭합니다.

<img width="80%" src="/images/rcp/rcp9.png" alt="" title="" >

지정한 폴더에 jar로 배포가 되는 것을 확인할 수 있습니다.

# 참고

- [이클립스 커맨드 튜토리얼](http://eclipse.or.kr/wiki/%ED%8A%B9%EC%A7%91%EA%B8%B0%EC%82%AC:Eclipse_%EC%BB%A4%EB%A7%A8%EB%93%9C_%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC)
- [Eclipse RCP 란?](https://narup.tistory.com/77)
