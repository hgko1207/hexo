---
title: '[PostgreSQL] 외부 접속 허용'
categories:
  - Programming
  - Database
tags:
  - PostgreSQL
  - CentOS
date: 2020-09-11 10:20:47
thumbnail: /images/thumbnail/postgresql.png
---

## 외부 접속 허용 설정

### 1. 사용자 비밀번호 설정

외부에서 접속 하기 위해선 우선 `postgres` 비밀번호를 설정해야 합니다.

```bash
// postgres 계정으로 접속
su - postgres psql

// 비밀번호 설정
\password postgres

# 종료
\q
```

### 2. 방화벽 개방

방화벽에서 5432 포트를 개방합니다.

```bash
firewall-cmd --permanent --zone=public --add-port=5432/tcp
firewall-cmd --reload
```

### 3. 설정 파일 변경

postgresql 접속 후 Data 디렉토리 확인을 할 수 있습니다.

```bash
show data_directory;
-> /var/lib/pgsql/11/data
```

```bash
# postgresql.conf 설정 파일을 엽니다.
vi /var/lib/pgsql/11/data/postgresql.conf

# 설정 파일에서 아래와 같이 변경
# listen_addresses = 'localhost' -> 주석으로 되어있음
listen_addresses = '*'
```

### 3. 보안 설정 변경

외부 접속을 위해 보안 설정을 변경합니다.

```bash
# root 계정으로 복귀합니다.
su - root

# 설정 파일을 엽니다.
vi /var/lib/pgsql/11/data/pg_hba.conf

# 설정 정보를 아래와 같이 변경합니다.
local all all peer => local all all md5
host all all 127.0.0.1/32 ident => host all all 0.0.0.0/0 md5
host all all ::1/128 ident => host all all ::1/128 md5
```

- `md5` : 패스워드를 md5로 암호화해서 전송

### 4. 서비스 재시작

```bash
sudo systemctl restart postgresql-11
```

## 참고

아래 링크에서는 pg_hba.conf를 수정하지 않고 접근제어를 할 수 있도록 하는 방법이 설명되어 있는데 테스트 해보진 않았습니다.

- [CentOS 7 에서 방화벽에 PostgreSQL 리스너 포트 등록하기](https://rastalion.me/centos-7-%EC%97%90%EC%84%9C-%EB%B0%A9%ED%99%94%EB%B2%BD%EC%97%90-postgresql-%EB%A6%AC%EC%8A%A4%EB%84%88-%ED%8F%AC%ED%8A%B8-%EB%93%B1%EB%A1%9D%ED%95%98%EA%B8%B0/)
