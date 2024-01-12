---
title: '메타마스크(MetaMask) 설치 및 사용 방법'
categories:
  - IT
  - Blockchain
tags:
  - Blockchain
  - 블록체인
  - Metamask
  - 메타마스크
date: 2022-12-09 12:59:18
thumbnail: /images/thumbnail/blockchain.png
---

**메타마스크** 설치 및 사용 방법에 대해 알아보겠습니다.

# 메타마스크(MetaMask) 란

> Ethereum 블록체인과 상호 작용하는 데 사용되는 소프트웨어 암호 화폐 지갑입니다. 이를 통해 사용자는 브라우저 확장 프로그램이나 모바일 앱을 통해 이더리움 지갑에 액세스 할 수 있으며, 이를 통해 분산 애플리케이션과 상호 작용할 수 있습니다. [위키백과](https://en.wikipedia.org/wiki/MetaMask)

이더리움 지갑 중 메타마스크는 커뮤니티에서 사용죄는 가장 인기 있는 지갑 중 하나입니다.

# 설치 및 사용 방법

## 설치

[메타마스크 웹사이트](https://metamask.io/)에서 크롬 플러그인으로 설치 할 수 있습니다. 사이트로 접속하여 Download 버튼을 클릭합니다.

![](/images/blockchain/metamask/1.png)

크롬 웹 스토어 창이 열리게 되고 "Chrome에 추가" 버튼을 클릭합니다. 크롬 확장프로그램에 MetaMask가 추가됩니다.

![](/images/blockchain/metamask/2.png)

## Mnemonic 복구

크롬 확장프로그램에서 MetaMask를 선택하고 "시작하기" 버튼을 클릭합니다.

![](/images/blockchain/metamask/3.png)

처음 사용하는 사용자라면 비밀 복구 구문을 사용하여 기존 지갑 가져오기와 새 지갑과 비밀 복구 구문 생성을 선택하는 화면이 보입니다.

지갑 생성을 해서 MetaMask를 사용할 수 있지만 이전 글 [[Ethereum] ganache-cli 설치 및 실행](https://hgko1207.github.io/2022/12/07/blockchain-1/)에서 생성된 Mnemonic을 사용하여 지갑을 가져오도록 하겠습니다.

![](/images/blockchain/metamask/4.png)

"지갑 가져오기"를 클릭하면 비밀 복구 구문으로 계정 가져오기 화면이 보입니다. 생성된 Mnemonic과 비밀번호를 입력하고 "가져오기" 버튼을 클릭합니다.

![](/images/blockchain/metamask/5.png)

![](/images/blockchain/metamask/6.png)

메타마스크 접속 시 화면입니다.

![](/images/blockchain/metamask/7.png)

## 네트워크 추가

ganache로 실행한 네트워크를 연결하기 위해 메타마스크에서 네트워크 추가를 합니다.

메타마스크 화면에서 우측 네트워크를 클릭하고 "네트워크 추가" 버튼을 클릭합니다.

![](/images/blockchain/metamask/8.png)

설정화면에서 "네트워크 수동 추가"를 클릭합니다.

![](/images/blockchain/metamask/9.png)

네트워크 이름, 새 RPC URL(ip 주소와 포트), 체인 ID(url을 입력하면 자동으로 찾아줌), 통화 기호를 입력하고 "저장" 버튼을 클릭합니다.

![](/images/blockchain/metamask/10.png)

추가된 네트워크가 보이며 선택 시 계정 정보가 보입니다.

![](/images/blockchain/metamask/11.png)

# 결론

메타마스크 설치와 사용 방법에 대해 알아보았습니다. 이더리움 지갑에 쉽게 액세스 할 수 있어 블록체인 기반 웹이나 앱개발 시 도움이 많이 됩니다.
