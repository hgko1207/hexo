---
title: '[Spring Boot] Maven 빌드 방법'
categories:
  - Programming
  - Backend
  - Spring
tags:
  - Spring Boot
  - Maven
  - 스프링부트
date: 2021-03-09 13:52:07
thumbnail: /images/thumbnail/spring.png
---

## STS(Spring Tool Suite)에서 빌드 방법

1. 메뉴 -> Run -> Run Configurations -> Maven Build(우클릭) -> New Configuration 클릭
2. **[Name]** 입력 란에 작성
3. **[Base directory]** 에서 **Workspace** 버튼 클릭
4. 빌드하려는 프로젝트 선택
5. **[Goals]** 입력 란에 `clean install` 작성
6. 저장 후 빌드 실행

아래 이미지는 설정 한 내용입니다.

![](/images/springboot/maven_build.png)

## Maven 빌드 중에 데이터베이스 연결을 제외하는 방법

- Maven Build -> **[Goals]** 입력 란에 `clean install -DskipTests` 작성합니다.

- 또는 pom.xml에 아래 코드를 추가합니다.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <configuration>
        <skipTests>true</skipTests>
    </configuration>
</plugin>
```
