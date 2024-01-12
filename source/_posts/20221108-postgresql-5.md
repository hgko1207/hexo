---
title: '[PostgreSQL] 사용자 인증'
categories:
  - Programming
  - DB
  - PostgreSQL
tags:
  - PostgreSQL
  - Database
  - DB
  - 사용자 인증
date: 2022-11-08 13:39:56
thumbnail: /images/thumbnail/postgresql.png
---

## 사용자 인증

Postgresql을 처음 설치하게 되면 비밀번호를 묻지 않고 로그인을 할 수 있습니다.
인증과정을 포함하려면 **pg_hba.conf** 에서 설정해야 합니다.

**pg_hba.conf** 파일은 initdb 에서 생성된 클러스터 폴더에 위치합니다.

Authentication Method 필드의 값에 따라서 인증처리가 됩니다.

- trust: 패스워드 없이 접근 가능 (local 이외에는 비추천)
- reject: 거부
- md5: 패스워드를 md5 로 암호화해서 전송
- password: text 로 패스워드를 사용 (스니핑에 바로 보임)

## 사용 예제

TCP/IP로 127.0.0.1에 접근 시 모든 DB, 사용자로의 접근에 패스워드가 필요 없는 예제입니다.

```sh
host  all  all  127.0.0.1/32  trust
```

TCP/IP로 192.168.0.1에 접근 시 hgko 계정으로 모든 DB에 대한 접근이 허용되며, md5로 패스워드를 암호화해야 하는 예제입니다.

```sh
host  all  hgko  192.168.0.1/32  md5
```

TCP/IP로 192.168.0.1에 접근 시 hgko 계정으로 mydb, test DB에 대한 접근이 허용되며, md5로 패스워드를 암호화해야 하는 예제입니다.

```sh
host  mydb,test  hgko  192.168.0.1/32  md5
```

원격 어디서든지 remotegroup의 SYSID로 설정된 계정들로 remotedb의 접근이 허용되며, md5로 패스워드를 암호화해야 하는 예제입니다.

```sh
host  remotedb  +remotegroup  0.0.0.0/0  md5
```

## 모든 호스트로 부터 접속 허용

**postgresql.conf** 파일을 수정합니다.

```sh
listen_addresses = '*'
```

**pg_hba.conf** 파일을 수정합니다.

```sh
# TYPE DATABASE USER CIDR-ADDRESS METHOD
host  all  all  0.0.0.0/0  md5
```

## 참고

- https://www.postgresql.kr/docs/9.5/auth-methods.html
