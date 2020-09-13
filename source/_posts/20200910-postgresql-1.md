---
title: '[PostgreSQL] CentOS 7에서 PostgreSQL 설치 및 시작'
categories:
  - Programming
  - Database
tags:
  - PostgreSQL
  - CentOS
date: 2020-09-10 18:22:53
thumbnail: /images/thumbnail/postgresql.png
---

최근에 CentOS 7에 PostgreSQL을 설치했다. 설치 과정을 정리해봤다.

## 운영체제

CentOS 7.6

## Version

PostgreSQL 11.9

## 인터넷이 되는 환경

```bash
# Install the repository RPM:
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# PostgreSQL을 설치합니다.
sudo yum install -y postgresql11-server postgresql11-contrib
```

## 인터넷이 안되는 환경

### 1. RPM 다운로드

외부 환경에서 [PostgreSQL Database Server 11 PGDG](https://yum.postgresql.org/11/redhat/rhel-7-x86_64/repoview/postgresqldbserver11.group.html) 페이지에 접속해서 RPM 파일들을 다운로드 하고 리눅스 환경으로 이동시킨다.

- postgresql11-11.9-1PGDG.rhel7.x86_64.rpm
- postgresql11-contrib-11.9-1PGDG.rhel7.x86_64.rpm
- postgresql11-libs-11.9-1PGDG.rhel7.x86_64.rpm
- postgresql11-server-11.9-1PGDG.rhel7.x86_64.rpm

### 2. 설치

postgresql11-libs -> postgresql11 -> (postgresql11-server, postgresql11-contrib) 순으로 설치

```bash
sudo rpm -ivh postgresql11-libs-11.5-1PGDG.rhel7.x86_64.rpm
sudo rpm -ivh postgresql11-11.5-1PGDG.rhel7.x86_64.rpm
sudo rpm -ivh postgresql11-server-11.5-1PGDG.rhel7.x86_64.rpm
sudo rpm -ivh postgresql11-contrib-11.5-1PGDG.rhel7.x86_64.rpm
```

## 설치된 패키지 확인

```bash
rpm -qa | grep postgresql
```

## 기본 Database 생성

`initdb` 명령어를 통해 기본 데이터베이스를 설치합니다. 기본 데이터베이스는 `postgres` 라는 이름으로 생성됩니다.

```bash
sudo /usr/pgsql-11/bin/postgresql-11-setup initdb
```

## 서비스 등록 및 실행

```bash
sudo systemctl enable postgresql-11
sudo systemctl start postgresql-11
```

## postgresql 접속

```bash
sudo -u postgres psql
```

## 데이터베이스 생성

```cmd
postgres=# create database <name> encoding 'utf-8';
```
