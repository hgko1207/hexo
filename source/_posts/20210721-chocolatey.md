---
title: Chocolatey 설치
categories:
  - IT
  - Information
tags:
  - Chocolatey
  - Windows
date: 2021-07-21 19:21:51
thumbnail: /images/thumbnail/information.png
---

윈도우를 사용하면서 개발 환경을 쉽게 꾸릴 수 있는 Chocolatey(윈도우용 패키지 매니저) 설치와 사용 방법에 대해 알아보겠습니다.

# 설치

[공식 Install 홈페이지](https://chocolatey.org/install)를 따라 설치를 진행합니다.
윈도우 7 이상, 윈도우 서버 2003 이상에서 설치가 가능하고 PowerShell 에서 명령어로 설치할 수 있습니다.

## PowerShell 사용

관리자 권한으로 실행해야 합니다. 그렇지 않으면 메세지를 보여줍니다.<br>
아래 설치 명령어를 복사하여 입력하면 설치가 진행됩니다.

```bash
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

설치가 완료되었다면 `choco` 명령어를 입력하였을 때 아래와 같이 버전 정보가 나옵니다.

```bash
C:\Windows\system32> choco
Chocolatey v0.10.15
Please run 'choco -?' or 'choco <command> -?' for help menu.
C:\Windows\system32>
```

# 패키지 설치

[패키지 리스트](https://community.chocolatey.org/packages) 에서 설치 가능한 패키지들을 확인 할 수 있습니다.<br>

구글 크롬을 예제로 설치해보겠습니다. 검색 창에 `google chrome` 을 검색하면 결과가 나오고 오른쪽에 설치 명령어가 보여집니다. 명령어를 복사하고 PowerShell 에 입력하면 설치가 진행됩니다.

```bash
> choco install googlechrome
```

설치가 완료되었으면 아래 명령어를 입력하여 설치된 패키지들을 확인합니다.

```bash
> choco search googlechrome
```

**Ubuntu** 의 `apt-get` 와 **CentOS** `rpm` 명령어처럼 윈도우에서도 설치 명령어를 통해 필요한 프로그램을 쉽게 설치할 수 있습니다.

## 추천 패키지들

- Windows Terminal
- vscode
- python3
- git
- postman
- jdk8
- Adobe Acrobat Reader
- Notepad++
- Node JS
- PowerToys
- WSL(Windows Subsystem for Linux)
