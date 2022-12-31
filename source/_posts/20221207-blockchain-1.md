---
title: '[Ethereum] ganache-cli 설치 및 실행'
categories:
  - IT
  - Blockchain
tags:
  - Blockchain
  - Ethereum
  - ganache
  - ganache-cli
date: 2022-12-07 10:20:28
thumbnail: /images/thumbnail/blockchain.png
---

**ganache-cli** 를 설치하고 실행하는 방법에 대해 알아보겠습니다.

## Ganache

"가나슈"라고 읽으면 되고, 가상의 이더리움 네트워크를 생성해서 Smart Contract 를 실행할 수 있도록 해주는 프로그램입니다. 이런 가상 환경을 TestRPC 라고 합니다.

## Ganache CLI

Ganache CLI 는 빠르고 사용자 정의 가능한 블록체인 에뮬레이터인 TestRPC 의 최신 버전입니다. 실제 이더리움 노드를 실행하는 오버헤드 없이 블록체인을 호출할 수 있습니다.

- Transactions are “mined” instantly.
- No transaction cost.
- Accounts can be re-cycled, reset and instantiated with a fixed amount of Ether (no need for faucets or mining).
- Gas price and mining speed can be modified.
- A convenient GUI gives you an overview of your testchain events.

## NPM 설치

Ganache 는 NPM 을 통해 설치할 수 있습니다.

먼저 NPM 이 설치되어 있어야 합니다. 이전 글 [Node.js 및 NPM 설치](https://hgko1207.github.io/2022/12/07/linux-24/) 을 참고해서 설치를 합니다.

## Ganache 설치

```shell
$ npm install -g ganache-cli
```

## 실행

```shell
$ ganache-cli <options>
```

`ganache-cli` 명령어를 통해 실행합니다. 옵션 없이 실행 시 아래와 같은 결과를 볼 수 있습니다.

```shell
$ ganache-cli
Ganache CLI v6.12.2 (ganache-core: 2.13.2)

Available Accounts
==================
(0) 0x3F82D42b4b946aA53fF069cF931d940872C3f675 (100 ETH)
(1) 0x0912b4EdD5279FEE8362257adD75715424C51a39 (100 ETH)
(2) 0x668fF7BD1fe9ffe6758B9d1f71fcdA22c56f68ce (100 ETH)
(3) 0xD74Dd2D769763B78009a67b6b87c7810a7eb7E6d (100 ETH)
(4) 0x6Ec7b0A1f88f482711f4C8b378c8B4c6dCB863EB (100 ETH)
(5) 0xa7eed29620A49ca13F780b740d597Cc79092E2D9 (100 ETH)
(6) 0xfE7f9A8E6c147A07bd1b0601431dc74468456174 (100 ETH)
(7) 0x0b3a29F6174631a97fe9B9289c66456ddD27D069 (100 ETH)
(8) 0x89b626bAF633fAb58986499195b4F98d15D09252 (100 ETH)
(9) 0xA42521a288fD576f59E1F7A7461Dfe88A52cAF99 (100 ETH)

Private Keys
==================
(0) 0xe7c964a0050a9c8c79008eab74502ea7c105a425b5e6b8ffe57d72eef4165c20
(1) 0x098196b42d262985b0f0b43edc4a51919d8dd9925e0feee485859c5987b4af9c
(2) 0x23738d8fc442fd26c7a802423868bbfc0c0d930f15baef50531483a1e9f7cecd
(3) 0xa67eaa626df00109e219b5f94d33535d536b19d362fbf0eff08e7143383fd95e
(4) 0xede8027c26a03ec63d6b9c404216fe6328936cc6584f93b3389901bfe34efef0
(5) 0x30541fc3cac5dbe9e96a482dcd4100930270f9759d1e15494bbf26932fd6e873
(6) 0xa8ed660d43f2c775efff16732088e34ab23775fa56375f491c8bec3123bde75c
(7) 0x5cf88b19ce7be57320c2a89bf03a9ea5a512a5dc07f9e14f4a752fb1a021deac
(8) 0x557ae7917ca63f17fbb947933c3ad13cc699f42293aafbebe24729f91708eabe
(9) 0xbe44643a2507aa8fc13893f4052edd154e6753d74bec3f8a8ec6a88fda645c19

HD Wallet
==================
Mnemonic:      convince have junior clean bomb fluid gossip surprise build twenty urban sword
Base HD Path:  m/44'/60'/0'/0/{account_index}

Gas Price
==================
20000000000

Gas Limit
==================
6721975

Call Gas Limit
==================
9007199254740991

Listening on 127.0.0.1:8545
```

기존 Mnemonic 을 가지고 있다면 -m 옵션을 추가하여 설정할 수 있습니다.

```shell
$ ganache-cli -d -m "taxi"
Ganache CLI v6.12.2 (ganache-core: 2.13.2)

Available Accounts
==================
(0) 0x90F8bf6A479f320ead074411a4B0e7944Ea8c9C1 (100 ETH)
(1) 0xFFcf8FDEE72ac11b5c542428B35EEF5769C409f0 (100 ETH)
(2) 0x22d491Bde2303f2f43325b2108D26f1eAbA1e32b (100 ETH)
(3) 0xE11BA2b4D45Eaed5996Cd0823791E0C93114882d (100 ETH)
(4) 0xd03ea8624C8C5987235048901fB614fDcA89b117 (100 ETH)
(5) 0x95cED938F7991cd0dFcb48F0a06a40FA1aF46EBC (100 ETH)
(6) 0x3E5e9111Ae8eB78Fe1CC3bb8915d5D461F3Ef9A9 (100 ETH)
(7) 0x28a8746e75304c0780E011BEd21C72cD78cd535E (100 ETH)
(8) 0xACa94ef8bD5ffEE41947b4585a84BdA5a3d3DA6E (100 ETH)
(9) 0x1dF62f291b2E969fB0849d99D9Ce41e2F137006e (100 ETH)

Private Keys
==================
(0) 0x4f3edf983ac636a65a842ce7c78d9aa706d3b113bce9c46f30d7d21715b23b1d
(1) 0x6cbed15c793ce57650b9877cf6fa156fbef513c4e6134f022a85b1ffdd59b2a1
(2) 0x6370fd033278c143179d81c5526140625662b8daa446c22ee2d73db3707e620c
(3) 0x646f1ce2fdad0e6deeeb5c7e8e5543bdde65e86029e2fd9fc169899c440a7913
(4) 0xadd53f9a7e588d003326d1cbf9e4a43c061aadd9bc938c843a79e7b4fd2ad743
(5) 0x395df67f0c2d2d9fe1ad08d1bc8b6627011959b79c53d7dd6a3536a33ab8a4fd
(6) 0xe485d098507f54e7733a205420dfddbe58db035fa577fc294ebd14db90767a52
(7) 0xa453611d9419d0e56f499079478fd72c37b251a94bfde4d19872c44cf65386e3
(8) 0x829e924fdf021ba3dbbc4225edfece9aca04b929d6e75613329ca6f1d31c0bb4
(9) 0xb0057716d5917badaf911b193b12b910811c1497b5bada8d7711f758981c3773

HD Wallet
==================
Mnemonic:      taxi
Base HD Path:  m/44'/60'/0'/0/{account_index}

...
```

## 실행 옵션

옵션들을 확인하여 환경에 맞게 실행합니다.

- `-a` or `--accounts`: 시작 시 생성할 계정 수를 지정합니다.
- `-b` or `--blocktime`: 자동 마이닝을 위한 블록 타임을 초 단위로 지정합니다. 기본값은 0이며 자동 마이닝이 없습니다.
- `-d` or `--deterministic`: 미리 정의된 니모닉을 기반으로 결정적 주소를 생성합니다.
- `-n` or `--secure`: 기본적으로 사용 가능한 계정 잠금(제3자 트랜잭션 서명에 적합)
- `-m` or `--mnemonic`: 특정 HD 지갑 니모닉을 사용하여 초기 주소를 생성합니다.
- `-p` or `--port`: 포트 번호 설정. 기본값은 8545 입니다.
- `-h` or `--hostname`: 호스트 이름. 기본값은 노드의 server.listen() 입니다.
- `-s` or `--seed`: 임의의 데이터를 사용하여 사용할 HD 지갑 니모닉을 생성합니다.
- `-g` or `--gasPrice`: 사용자 지정 가스 가격 설정(기본값은 20000000000)
- `-l` or `--gasLimit`: 사용자 지정 가스 한도 설정(기본값은 90000)
- `-f` or `--fork`: 주어진 블록에서 현재 실행 중인 다른 이더리움 클라이언트에서 분기합니다. 입력은 다른 클라이언트의 HTTP 주소 및 포트여야 합니다.(예: http://localhost:8545)
- `-i` or `--networkId`: ganache-cli가 자신을 식별하는 데 사용할 네트워크 ID를 지정합니다.
- `--db`: 체인 데이터베이스를 저장할 디렉토리 경로를 지정합니다. 데이터베이스가 이미 존재하는 경우 ganache-cli는 새 체인을 생성하는 대신 해당 체인을 초기화합니다.
- `--debug`: Output VM opcodes for debugging
- `--mem`: ganache-cli 메모리 사용량 통계를 출력합니다.
- `--e`: 사용자 계정별 가스를 설정합니다.(기본값은 100)

## 참고

- https://www.npmjs.com/package/ganache-cli
- https://docs.nethereum.com/en/latest/ethereum-and-clients/ganache-cli/
