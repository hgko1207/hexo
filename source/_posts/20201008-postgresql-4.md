---
title: '[PostgreSQL] TimescaleDB 설치'
categories:
  - Programming
  - DB
  - PostgreSQL
tags:
  - PostgreSQL
  - DB
  - TimescaleDB
  - 설치
date: 2020-10-08 13:12:58
thumbnail: /images/thumbnail/postgresql.png
---

## TimescaleDB 란

**TimescaleDB**는 빠른 수집, 복잡한 쿼리를 편리하게 사용하기 위해 설계된 오픈 소스 시계열 데이터베이스 입니다.

PostgreSQL을 기반으로 하며 자동 파티셔닝과 SQL 지원을 제공합니다. PostgreSQL 보다 10 ~ 100배 빠른 쿼리를 수행하고 시계열에 대해 최적화가 되어 있습니다.

5 ~ 10분 단위로 수집되는 많은 양의 데이터를 데이터베이스에 추가하고 시계열로 관리하며 빠르게 조회하기 위해 TimescaleDB를 사용하였습니다.

## 운영환경

- CentOS 7.6
- PostgreSQL 11

## 설치

PostgreSQL이 설치 되어있어야 합니다. 미설치 시 [[PostgreSQL] CentOS 7에서 PostgreSQL 설치 및 시작](https://hgko1207.github.io/2020/09/10/postgresql-1/)을 참고해서 설치합니다.

### 1. PostgreSQL 설치 확인

```shell
$ rpm -qa | grep postgresql
```

### 2. 계정 확인

```shell
$ cat /etc/passwd | grep postgres
```

postgres 계정이 없으면 생성합니다.

```shell
$ sudo useradd postgres
$ sudo passwd postgres
```

### 3. 설정 변경

```bash
$ vi /var/lib/pgsql/11/data/postgresql.conf

#listen_addresses = 'localhost'  ->  listen_addresses = '*'
#password_encryption = md5  ->  password_encryption = md5
```

### 4. TimescaleDB 다운로드

다음 명령어를 복사해서 붙여넣습니다.

```bash
$ sudo cat > /etc/yum.repos.d/timescale_timescaledb.repo <<EOL
[timescale_timescaledb]
name=timescale_timescaledb
baseurl=https://packagecloud.io/timescale/timescaledb/el/7/\$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packagecloud.io/timescale/timescaledb/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
EOL
```

```shell
$ sudo yum update -y
$ yum install -y timescaledb-postgresql-11
```

### 5. 데이터베이스 설정

계속 y를 눌러줍니다.

```shell
$ sudo timescaledb-tune --pg-config=/usr/pgsql-11/bin/pg_config
```

### 6. PostgreSQL 재시작

```shell
$ systemctl restart postgresql-11
```

### 7. 접속

```shell
$ sudo su
$ su - postgres
$ psql
```
