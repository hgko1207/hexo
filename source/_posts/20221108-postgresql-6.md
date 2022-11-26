---
title: '[PostgreSQL] 사용자, 그룹 관리'
categories:
  - Server
  - Database
tags:
  - PostgreSQL
  - Database
  - DB
  - 사용자 관리
  - 그룹 관리
date: 2022-11-08 14:03:30
thumbnail: /images/thumbnail/postgresql.png
---

## 실행 파일을 통합 방법

### 사용자 생성

```bash
$ createuser hgko --createdb --no-superuser --no-createrole
```

### 사용자 삭제

```bash
$ dropuser hgko
```

## DB 접속을 통한 방법

### GROUP 생성, 수정, 삭제

- **SYSID**: 내부의 GROUP ID 구분용 숫자 코드이며, 설정하지 않으면 자동으로 100부터 1씩 증가합니다. (1~99는 핵심적인 그룹을 위함) 자동으로 설정되게 하면됩니다.

#### GROUP 생성

```sql
CREATE GROUP [그룹명];
CREATE GROUP [그룹명] WITH USER user1, user2, user3;
CREATE GROUP [그룹명] WITH SYSID 100 USER user1;
CREATE GROUP [그룹명] WITH SYSID 100;
```

#### GROUP 수정

```sql
ALTER GROUP [그룹명] ADD USER user4, user5;
ALTER GROUP [그룹명] DROP USER user3;
ALTER GROUP [그룹명] RENAME TO [새로운 그룹명];
```

#### GROUP 삭제

```sql
DROP GROUP [그룹명];
```

- GROUP 조회

```sql
-- 1)
postgres=# \dg
postgres=# \du

-- 2)
select * from pg_group;
```

### 사용자 생성, 수정, 삭제

#### 사용자 생성

```sql
CREATE USER test_user CREATEDB CREATEUSER IN GROUP test_group UNENCRYPTED PASSWORD '1234';
```

사용자 생성에 사용되는 옵션들입니다.

- [ SUPERUSER | NOSUPERUSER ]
- [ CREATEDB | NOCREATEDB ]
- [ CREATEROLE | NOCREATEROLE ]
- [ CREATEUSER | NOCREATEUSER ]
- [ LOGIN | NOLOGIN ]
- [ ENCRYPTED | UNENCRYPTED ] PASSOWRD 'password'
- VALID UNTIL 'timestamp'
- IN ROLE role_name [, ...]
- IN GROUP group_name [, ...]
- ROLE role_name [, ...]
- ADMIN role_name [, ...]
- USER role_name [, ...]
- SYSID uid

#### 사용자 수정

```sql
ALTER USER [사용자명] RENAME TO [새로운 사용자명];
```

#### 사용자 삭제

```sql
DROP USER [사용자명]
```
