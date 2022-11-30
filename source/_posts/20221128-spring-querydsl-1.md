---
title: '[Spring] JPA with Querydsl'
categories:
  - Programming
  - Spring
tags:
  - Spring
  - Spring Data JPA
  - Querydsl
date: 2022-11-28 10:57:14
thumbnail: /images/thumbnail/spring.png
---

# Query DSL

- JPA, JDO, SQL 같은 백엔드를 위해 type-safe SQL을 만드는 프레임워크
- Domain Specific Language
- 특정한 도메인에 초점을 맞춘 제한적인 표현력을 가진 컴퓨터 프로그래밍 언어

## 특징

- type-safe
- 조회에 특화된 프로그래밍 언어
- 단순, 간결
- 다양한 저장소 조회 기능 통합 (데이터 조회 기능 추상화)

## 동작 방식

- Member java or Member table 의 메타 데이터를 참조하여 코드 생성기를 통해 QMember.java 를 생성합니다.
- APT: Annotation Processing Tool
- Table Meta: Querydsl-maven-plugin

## 기능

- Query: from, where, join
- Path: QMember, Qmember.name
- Expression: name.eq, name.qt

## 세부기능

- from
- innerJoin, join, leftJoin, fetchJoin, fullJoin, on
- where (and, or, allOf, anyOf)
- groupBy
- having
- order By (desc, asc)
- limit, offset, restrict(limit + offset) (Paging)
- list
- listResults (list + Paging Info(totalCount))
- iterate
- count
- singleResult, uniqueResult

## 사용 방법

Spring Boot 프로젝트의 pom.xml 에 dependency 와 plugin 을 추가합니다.

```xml
<!-- properties 에 추가 -->
<querydsl.version>4.4.0</querydsl.version>

<!-- dependencies 에 추가 -->
<dependency>
  <groupId>com.querydsl</groupId>
  <artifactId>querydsl-apt</artifactId>
  <version>${querydsl.version}</version>
  <scope>provided</scope>
</dependency>

<dependency>
  <groupId>com.querydsl</groupId>
  <artifactId>querydsl-jdo</artifactId>
  <version>${querydsl.version}</version>
</dependency>

<!-- build - plugins 에 추가 -->
<plugin>
  <groupId>com.mysema.maven</groupId>
  <artifactId>apt-maven-plugin</artifactId>
  <version>1.1.3</version>
  <executions>
    <execution>
      <goals>
        <goal>process</goal>
      </goals>
      <configuration>
        <outputDirectory>target/generated-sources/java</outputDirectory>
        <processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
        <sourceEncoding>UTF-8</sourceEncoding>
      </configuration>
    </execution>
  </executions>
</plugin>
```

테이블 도메인 클래스를 생성합니다.

```java
@Entity
@Table(name = "tb_team")
public class Team {
  @Id
  private int id;

  @Column(name = "name", nullable = false)
  private String name;

  private int rating;
}
```

Repository 인터페이스를 작성합니다.

```java
public interface TeamRepository extends JpaRepository<Team, Integer> {
}
```

### Querydsl 사용 예

Repository 인터페이스에 `QuerydslPredicateExecutor` 를 확장합니다.

```java
public interface TeamRepository extends JpaRepository<Team, Integer>, QuerydslPredicateExecutor<Team> {
}
```

```java
@Service
@RequiredArgsConstructor
public class TeamService {

  private final TeamRepository teamRepository;

  public void testQuerydsel {
    teamRepository.findAll(QTeam.team.name.eq("test"1));
    teamRepository.findOne(QTeam.team.rating.loe(100));
  }
}
```

### JPAQuery 사용 예

```java
@Service
public class TeamService {

  @PersistenceContext
  private EntiryManager em;

  public void testQuerydsl() {
    JPAQuery query = new JPAQuery(em);
    QTeam team = QTeam.team;

    List<Team> teams = query.from(team)
                            .where(team.name.eq("test1").or(team.name.like("hgko%")))
                            .list(team);
    System.out.println("querydsl =>" + teams);
  }
}
```
