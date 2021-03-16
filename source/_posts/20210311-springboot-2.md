---
title: '[Spring Boot] 환경에 따른 설정'
categories:
  - Programming
  - Spring Framework
tags:
  - Spring Boot
  - Properties
date: 2021-03-11 09:38:25
thumbnail: /images/thumbnail/spring.png
---

Spring Boot 를 사용하여 웹 프로젝트를 할 때에 환경(개발 또는 배포)에 따라 설정 값들을 달리 할 필요가 있습니다.

Spring Boot 에서는 `application.properties` 파일을 `profile` 로 구분하여 사용할 수 있습니다. `profile` 을 작성하지 않을경우 **default** 로 `application.properties` 를 사용합니다.

## application.properties 작성 규칙

`profile` 을 포함한 파일명을 작성합니다.

```properties
# default
application.properties

# 배포 환경(prod)
application-prod.properties

# 개발 환경(dev)
application-dev.properties

# 테스트 환경(test)
application-test.properties

# custom
application-custom.properties
```

## 예제

개발과 배포 할 때의 설정을 나눈 예제입니다.

### 파일 생성

```properties
# 배포용(기본)
application.properties

# 개발용(dev)
application-dev.properties
```

### application.properties 설정

`application-dev.properties` 파일에 `spring.profiles.active=dev` 을 추가합니다.

- **application.properties**

```properties
# Server 설정
server.port=8080

# Database 설정
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://[외부 IP]:3306/test?characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=root!23
```

- **application-dev.properties**

```properties
# Profile 설정 - 이 값을 꼭 넣어야 합니다.
spring.profiles.active=dev

# Server 설정
server.port=8081

# Database 설정
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/test?characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=test!23
```

### Application 실행 설정

#### **STS(Spring Tool Suite)** - Spring Boot Run

아래 이미지와 같이 `Profile` 에 적용하고자 하는 환경 값(예: dev)을 선택하면 `application-dev.properties` 의 설정을 읽어옵니다.

![](/images/springboot/profile_setting.png)

### 실행 테스트

`dev` 환경을 주입 후 실행 테스트를 하였습니다. `dev` 환경일 때 서버 포트를 **8081** 으로 설정을 하였었는데 아래의 실행 로그를 보면 `Tomcat started on port(s): 8081` 처럼 **8081** 포트로 서버가 실행 된 것을 확인할 수 있습니다.

```bash
2021-03-11 13:52:28.738  INFO 13588 --- [  restartedMain] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2021-03-11 13:52:28.772  INFO 13588 --- [  restartedMain] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2021-03-11 13:52:29.903  INFO 13588 --- [  restartedMain] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2021-03-11 13:52:30.836  INFO 13588 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8081 (http) with context path '/admin'
2021-03-11 13:52:30.839  INFO 13588 --- [  restartedMain] c.y.a.a.EAfterschoolAdminApplication     : Started EAfterschoolAdminApplication in 6.985 seconds (JVM running for 7.822)
```
