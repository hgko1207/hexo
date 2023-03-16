---
title: '[MySQL] Query'
categories:
  - Programming
  - DB
  - MySQL
tags:
  - MySQL
  - Query
  - Database
  - DB
date: 2020-05-07 11:17:14
thumbnail: /images/thumbnail/mysql.png
---

## SELECT

```sql
SELECT * FROM 테이블명
SELECT * FROM 테이블명 WHERE 조건
SELECT 필드명1, 필드명2, ... FROM 테이블명 WHERE 조건
```

## INSERT

```sql
INSERT INTO 테이블명(필드명1, 필드명2, 필드명3, ...) VALUES (데이터값1, 데이터값2, 데이터값3, ...)
또는
INSERT INTO 테이블명 VALUES (데이터값1, 데이터값2, 데이터값3, ...)
```

## UPDATE

```sql
UPDATE 테이블명 SET 필드명1=데이터값1, 필드명2=데이터값2, ... WHERE 필드명=데이터값
```

## DELETE

```sql
DELETE FROM 테이블명 WHERE 필드명=데이터값
```

## 중복 데이터 조회

중복된 것 모두 조회

```sql
SELECT 필드명, count(*) FROM 테이블명 GROUP BY 필드명
```

중복된 갯수가 n개 이상인 것

```sql
SELECT 필드명, count(*) as 변수명 FROM 테이블명 GROUP BY 필드명 HAVING 변수명 > n;
또는
SELECT 필드명, count(*) FROM 테이블명 GROUP BY 필드명 HAVING count(*) > n;

SELECT 필드명, count(*) as 변수명 FROM 테이블명 WHERE 조건 GROUP BY 필드명 HAVING 변수명 > n;
```

중복 데이터 추출(WHERE 절의 IN 사용)

```sql
SELECT * FROM 테이블명 WHERE column1 IN (
  SELECT column1 FROM 테이블명 WHERE 조건 GROUP BY column1 HAVING count(*) > 1
)
```

## AUTO_INCREMENT 초기화

```sql
ALTER TABLE 테이블명 AUTO_INCREMENT = 시작할 값;
```

## 날짜

```sql
SELECT * FROM 테이블명 WHERE 필드명 >= 시작날짜
SELECT * FROM 테이블명 WHERE 필드명 BETWEEN 시작날짜 and 종료날짜
```
