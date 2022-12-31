---
title: '[PostgreSQL] Command 명령어'
categories:
  - Server
  - Database
tags:
  - PostgreSQL
  - 명령어
date: 2020-09-14 10:40:09
thumbnail: /images/thumbnail/postgresql.png
---

## 명령어

PostgreSQL에 접속합니다.

```shell
$ psql -U postgres
```

| 명령어           | 설명                         |
| ---------------- | ---------------------------- |
| \list or \l      | 데이터베이스 목록 조회       |
| \list+ or \l+    | 데이터베이스 목록 상세조회   |
| \c [DB Name]     | 다른 DB에 접속               |
| \d               | 테이블 목록 보기             |
| \dt [Table Name] | 지정된 테이블 컬럼 목록 보기 |
| \dS              | 시스템 테이블 목록 보기      |
| \dv              | 뷰 목록 보기                 |
| \ds              | 시퀀스 목록 보기             |
| \du              | 롤 목록 보기                 |
| \dn              | 스키마 목록 보기             |
| \q               | psql 종료(Ctrl + d)          |

## 백업 및 복원

| 명령어                                                         | 설명                                                           |
| -------------------------------------------------------------- | -------------------------------------------------------------- |
| pg_dump > [백업파일명]                                         | 전체 백업                                                      |
| pg_dump [DB명] > [백업파일명]</br>예) pg_dump mydb > db.sql    | 데이터베이스만 백업                                            |
| psql -U postgres [DB명] > [백업파일명]                         | 데이터베이스만 백업                                            |
| psql -f [백업파일명] [복원할 DB명]</br>예) psql -f db.sql mydb | DB 만 복원</br>단, DB가 없는 경우에는 생성을 먼저 해줘야 한다. |
| psql [복원할 DB명] < [백업파일명]</br>예) psql mydb < db.sql   | DB 만 복원</br>단, DB가 없는 경우에는 생성을 먼저 해줘야 한다. |
