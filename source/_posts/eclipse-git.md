---
title: '[Git] 이클립스에서 Git 사용법'
categories:
  - IT
  - Git
tags:
  - Git
  - Eclipse
  - GitHub
  - Repository
  - EGit
date: 2019-01-18 11:17:07
thumbnail:
---

기존에는 사내에서 개발할 때 SVN으로 형상관리를 하였는데, 이번에 개인 공부도 하고 프로젝트로 만들다 보니 GitHub를 사용하게 되었습니다. GitHub는 원격 저장소를 제공하며 여러가지 프로젝트 진행을 원활하게 하는 도구를 함께 제공하는 이점이 있어서 사용하였습니다.

스프링 프레임워크 기반 웹 프로젝트를 이클립스로 개발하고 있어 이클립스와 GitHub를 연동하였습니다. 이제 연동 방법을 설명합니다.

### 1. 원격 저장소 생성

먼저 공식 사이트인 https://github.com/ 에서 회원가입을 합니다. 회원가입 후 로그인을 하고 **_"Start a project"_** 버튼을 클릭합니다. 아래 그림처럼 화면이 나옵니다.

<img width="100%" src="/images/git/git-repository.png" alt="원격 저장소 생성" title="원격 저장소 생성" >

원격 저장소 이름을 입력하고 다른 것은 수정하지 말고 **_"Create repository"_** 버튼을 클릭하면 아래와 같은 원격저장소가 생성됩니다. 빨간 네모 박스의 경로를 복사해둡니다.

<img width="100%" src="/images/git/git-success.png" alt="원격 저장소 생성 완료" title="원격 저장소 생성 완료" >

### 2. EGit 설치

이클립스를 실행하고 **[Help] -> [Eclipse Marketplace]**를 클릭합니다.

<img width="80%" src="/images/git/eclipse-git-1.png" alt="Eclipse Marketplace" title="" >

Marketplace에서 Egit를 검색합니다. 아래 그림 처럼 **EGit - Git Integration for Eclipse** 를 찾아 설치합니다. 설치가 완료되면 이클립스를 다시 실행하게 됩니다.

<img width="50%" src="/images/git/eclipse-git-2.png" alt="EGit 설치" title="" >

재실행 후에 이클립스의 오른쪽 위에 퍼스펙티브 버튼을 클릭하면 창이 보입니다.

<img width="45%" src="/images/git/eclipse-git-3.png" alt="퍼스펙티브 추가" title="" >

Git을 선택하고 **[OK]** 버튼을 눌러 활성화 시킵니다. Git 퍼스펙티브가 추가된 것을 볼 수 있으며 아이콘을 클릭하면 아래 그림처럼 기본화면이 변경됩니다.

<img width="100%" src="/images/git/eclipse-git-4.png" alt="퍼스펙티브 변경" title="" >

### 3. 원격 저장소 연동

Git 퍼스펙티브 화면에서 **[Clone a Git repository]** 를 클릭합니다.

<img width="100%" src="/images/git/eclipse-git-5.png" alt="" title="" >

Clone Git Repository 창이 보이면 **Clone URL** 를 선택하고 **[Next]** 버튼을 클릭하면 아래의 그림처럼 화면이 보입니다.(이클립스 버전마다 조금씩 다른 것 같습니다.)

첫 번째 빨간 박스에서 앞에서 복사해둔 Git 원격 저장소 주소를 **URI** 칸에 복사하면 **Host**, **Repository path** 칸에 자동으로 입력됩니다. 그 밑의 빨간 박스에는 깃허브 아이디와 패스워드를 입력하고 **[Next]** 버튼을 클릭합니다.

<img width="60%" src="/images/git/eclipse-git-6.png" alt="" title="" >

Branch를 선택하는 화면이 보이는데 Branch를 만들지 않았으므로 그냥 **[Next]** 버튼을 클릭합니다.

<img width="60%" src="/images/git/eclipse-git-7.png" alt="" title="" >

원격 저장소와 연결할 로컬 저장소를 설정한 뒤 **[Finish]** 버튼을 클릭합니다.

<img width="60%" src="/images/git/eclipse-git-8.png" alt="" title="" >

### 4. 프로젝트 연동

개발하고 있는 프로젝트와 연동하기 위해 작업을 합니다. 프로젝트를 마우스 우클릭 후 그림 처럼 **[Team] -> [Share Project]** 를 클릭합니다.

<img width="70%" src="/images/git/eclipse-git-9.png" alt="" title="" >

**Git** 을 선택하고 **[Next]** 버튼을 클릭합니다. 그런 다음 Repository 란에서 앞에서 생성한 저장소를 설정해주고 **[Finish]** 버튼을 클릭합니다.

<img width="100%" src="/images/git/eclipse-git-10.png" alt="" title="" >

### 4. 첫 번째 커밋

원격 저장소에 첫 번째로 커밋을 합니다. 프로젝트를 마우스 우클릭 후 **[Team] -> [Commit]** 을 클릭합니다.

<img width="70%" src="/images/git/eclipse-git-11.png" alt="" title="" >

아래와 같은 화면이 뜨면 **_Commit Message_** 항목에 메시지를 작성 한 후 프로젝트 파일 전체를 **_Staged Changes_**로 옮깁니다. 그런 후에 마지막으로 **[Commit and Push]** 버튼을 클릭합니다.

<img width="100%" src="/images/git/eclipse-git-12.png" alt="" title="" >

Branch에 push 하기 과정인데 이 부분은 패스하겠습니다. **[Next]** 버튼을 클릭합니다.

<img width="65%" src="/images/git/eclipse-git-13.png" alt="" title="" >

그럼 로그인 창이 뜰텐데, GitHub의 아이디와 비밀번호를 입력하시고 **[OK]** 버튼을 클릭합니다. Push 확인 화면이 보여지는데 확인하고 **[Finish]** 버튼을 클릭합니다.

<img width="65%" src="/images/git/eclipse-git-14.png" alt="" title="" >

다시 로그인 창이 뜹니다. 처음에만 2번 로그인하고 그 다음에는 한번만 로그인 하면 됩니다. 아이디 비밀번호를 입력하고 **[OK]** 버튼을 클릭합니다. 완료가 되면 아래 그림 처럼 Push 결과 화면이 보여집니다.

<img width="65%" src="/images/git/eclipse-git-15.png" alt="" title="" >

## 5. GitHub에서 프로젝트 확인

[GitHub](https://github.com/) 홈페이지를 가서 Push된 프로젝트를 확인 할 수 있습니다. 그림 처럼 프로젝트가 올라가있고 수정된 이력도 보여집니다. 이클립스에서 소스 코드를 수정하고 위에서 본 **Commit** 과정과 같이 하면 프로젝트를 관리할 수 있습니다.

<img width="100%" src="/images/git/eclipse-git-16.png" alt="" title="" >

<br>

이클립스와 GitHub의 원격 저장소와 연동하여 설정을 하였습니다. 아직은 깃을 많이 사용해보지 못하였고 조금씩 알아가며 사용하고 있고 Branch에 대해서도 알아가고 있습니다. 늦은 감이 있긴 한데 이제라도 얼른 써서 익숙해지려고 노력해야겠습니다.

## 참고

- [[Git] 이클립스에서 Git 사용하기](http://eanastudy.tistory.com/66)
- [[Git] 이클릭스에서의 Git 사용법(egit) 1](http://gasaesososo.tistory.com/9?category=726951)
- [[Git] 이클립스와 깃(GitHub) 연동하여 원격 저장소의 프로젝트 내려받기](https://coding-factory.tistory.com/247)
- [[git] 이클립스(eclipse) 연동하여 처음 사용하기](http://lee-mandu.tistory.com/317)
