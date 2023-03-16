---
title: '[PostgreSQL] CentOS 7에서 PostgreSQL 설치 및 시작'
categories:
  - Programming
  - DB
  - PostgreSQL
tags:
  - PostgreSQL
  - CentOS
  - DB
  - Database
date: 2020-09-10 18:22:53
thumbnail: /images/thumbnail/postgresql.png
---

리눅스 환경에서 **PostgreSQL** 설치 및 시작 방법에 대해 알아보겠습니다.

## 운영환경

- CentOS 7.6
- PostgreSQL 11.9

## 인터넷이 되는 환경

```bash
# Install the repository RPM:
$ sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# PostgreSQL을 설치합니다.
$ sudo yum install -y postgresql11-server postgresql11-contrib
```

## 인터넷이 안되는 환경

### 1. RPM 다운로드

외부 환경에서 [PostgreSQL Database Server 11 PGDG](https://yum.postgresql.org/11/redhat/rhel-7-x86_64/repoview/postgresqldbserver11.group.html) 페이지에 접속해서 RPM 파일들을 다운로드 하고 리눅스 환경으로 이동시킨다.

- postgresql11-11.9-1PGDG.rhel7.x86_64.rpm
- postgresql11-contrib-11.9-1PGDG.rhel7.x86_64.rpm
- postgresql11-libs-11.9-1PGDG.rhel7.x86_64.rpm
- postgresql11-server-11.9-1PGDG.rhel7.x86_64.rpm

### 2. 설치

postgresql11-libs -> postgresql11 -> (postgresql11-server, postgresql11-contrib) 순으로 설치합니다.

```shell
sudo rpm -ivh postgresql11-libs-11.5-1PGDG.rhel7.x86_64.rpm
sudo rpm -ivh postgresql11-11.5-1PGDG.rhel7.x86_64.rpm
sudo rpm -ivh postgresql11-server-11.5-1PGDG.rhel7.x86_64.rpm
sudo rpm -ivh postgresql11-contrib-11.5-1PGDG.rhel7.x86_64.rpm
```

## 설치된 패키지 확인

```shell
$ rpm -qa | grep postgresql
```

## 기본 Database 생성

`initdb` 명령어를 통해 기본 데이터베이스를 설치합니다. 기본 데이터베이스는 `postgres` 라는 이름으로 생성됩니다.

```shell
$ sudo /usr/pgsql-11/bin/postgresql-11-setup initdb
```

## 서비스 등록 및 실행

```shell
$ sudo systemctl enable postgresql-11
$ sudo systemctl start postgresql-11
```

## postgresql 접속

```shell
$ sudo -u postgres psql
```

## 데이터베이스 생성

```cmd
postgres=# create database <name> encoding 'utf-8';
```
