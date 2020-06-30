---
title: JPA Annotation 정리
categories:
  - Programming
  - Spring Framework
tags:
  - Web
  - Spring Framework
  - Jpa
  - Hibernate
  - Annotation
  - Database
date: 2019-01-07 14:15:34
thumbnail:
---

### JPA(Hibernate) Annotation 정리

JPA로 개발하면서 자주 사용하는 어노테이션을 정리하였습니다.

**@Entity**
해당 클래스가 엔티티임을 알리기 위해 사용합니다. 애플리케이션이 실행이 될 때 엔티티 자동검색을 통하여 이 어노테이션이 선언 된 클래스들은 엔티티 빈으로 등록합니다.

**@Table**
데이터의 저장소, 테이블을 의미합니다. name 값은 실제 데이터베이스의 테이블 명을 의미하며, 생략이 가능합니다. 어노테이션을 생략하면 클래스의 이름을 테이블의 이름으로 자동 인식하게 됩니다.

**@Id**
엔티티빈의 기본키를 의미합니다. 이 어노테이션은 하나의 엔티티에는 반드시 하나가 존재해야 합니다. 복수키도 설정할 수 있습니다.

**@GeneratedValue**
데이터베이스에 의해 자동으로 생성된 값이라는 의미입니다. 즉, 프로그램 상에서 조작된 데이터가 아닌, 실제 데이터베이스에 데이터가 영속(저장)될 때 생성되는 값입니다. 몇 가지 생성전략이 존재합니다.

- IDENTITY : 기본 키 생성을 데이터베이스가 함
- SEQUENCE : 데이터베이스 시퀀스를 사용해서 기본 키 할당
- TABLE : 키 생성 테이블 생성

**@Column**
필드와 테이블의 컬럼을 매핑시켜줍니다. 이 어노테이션은 생략이 가능하며, 생략 시 필드의 이름이 테이블의 컬럼으로 자동으로 매핑이 됩니다.

1. name속성(String)
   필드와 매핑 될 컬럼의 이름을 명시합니다.

2. nullable속성(boolean)
   해당 컬럼이 null값을 허용하는가 하지않는가의 여부입니다.

3. length속성(int)
   컬럼의 길이값을 의미합니다.

4. unique속성(boolean)
   컬럼이 유일한 값을 가져야 하는가 아닌가의 여부입니다.

5. insertable속성(boolean)
   엔티티가 영속될 때 insert에 참여할지 말지를 결정합니다. 기본값은 true

6. updatable속성(boolean)
   변경된 필드의 값을 테이블에도 반영할지를 결정합니다. 기본값은 true

name속성을 제외한 나머지 속성은 잘 사용되지 않을 것 이라고 생각됩니다. nullable, length, unique는 DDL과 관련된 속성이고, insertable, updatable은 원래 잘 사용되지 않는 속성이기 때문입니다.

**@Temporal**
java.util.Date와 java.util.Calendar 값을 매핑 할 때 사용합니다.

- TemporalType.Date : 년-월-일 의 date 타입 (2019-01-04)
- TemporalType.Time : 시:분:초 의 time 타입 (12:11:11)
- TemporalType.TIMESTAMP : date + time 의 timestamp(datetime) 타입 (2019-01-04 12:11:11)
- 어노테이션을 사용하지 않을 경우 기본값은 timestamp 입니다. JPA 데이터베이스 방언에 의해, 데이터베이스의 타입에 따른 timestamp 또는 datetime은 자동으로 작성됩니다.

**@ColumnPosition(1)**
컬럼 순서 정합니다.

**@Enumerated**
자바의 enum 타입을 매핑할 때 사용합니다. 속성으로 EnumType.ORDINAL과 EnumType.STRING이 존재하는데 이름 그대로 ORDINAL은 순서를 STRING은 Enum의 이름을 저장합니다.

**@LOB**
데이터베이스 BLOB, CLOB 타입과 매핑됩니다. CLOB(String, char[], java.sql.CLOB)은 문자, BLOB(byte[], java.sql.BLOB)은 나머지가 매핑됩니다.

**@Transient**
저장 조회에 사용되지도 않고 그냥 단순 값을 가지고 있고 싶을 때 사용합니다.

**@Access**
데이터베이스에 엔티티에 값이 저장될 때 필드(AccessType.FIELD)의 값을 직접 접근해서 사용할 것인가 아니면 메서드에 직접(AccessType.PROPERTY) 접근할 것 인가를 설정하는 것 입니다.

**@MappedSuperClass**
어노테이션을 사용하면 부모 엔티티 접근 없이 부모 클래스의 매핑정보를 사용할 수 있습니다.
부모의 내용을 별도로 재정의해서 사용하고 싶은 경우에는 @AttributeOverride를 사용하여 재정의 합니다. 여러 개를 한번에 정의하기 위해서는 @AttributeOverrides를 사용합니다.
