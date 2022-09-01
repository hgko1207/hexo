---
title: Spring AOP
categories:
  - Programming
  - Spring
tags:
  - Spring Framework
  - AOP
date: 2020-03-25 10:04:18
thumbnail: /images/thumbnail/spring.png
---

AOP는 공통관심사항을 분리하여 반복되는 부분을 추출해 핵심 로직에 영향을 미치지 않고 소스의 중복을 줄이는 방법으로 기존 OOP에서 공통관심사항을 여러 모듈에서 적용하며 발생하는 중복된 코드 양산의 한계를 극복하기 위해 나오게 되었습니다.

## Spring AOP의 장점

예를 들어 어떠한 홈페이지에 로그인 처리를 해야할 때 AOP를 사용하지 않는다면 모든 페이지마다 로그인 상태인지 확인하는 소스코드를 넣어야 할테고 혹시나 그 로직이 변경되게 된다면 또 그 모든페이지의 소스를 수정해야하는 일이 생길 것 입니다. 하지만 AOP를 적용한다면 단 하나의 로그인 로직만 바꿔도 모든 소스에 적용시킬수 있는 장점이 있습니다.

## 스프링 AOP 용어

스프링 AOP를 이해하기 위해선 5가지 용어에 대한 이해가 필요합니다.

- Aspect - 여러객체에서 공통으로 적용되는 공통 관심사항(ex:트랜잭션, 로깅, 보안)
- JoinPoint – Aspect가 적용될수있는지점(ex:메소드, 필드)
- Pointcut – 공통 관심사항이 적용될 Joinpoint
- Advice – 어느시점(ex: 메소드수행전/후, 예외발생후등)에 어떤 공통관심기능(Aspect)을 적용할지 정의한것
- Weaving – 어떤 Advice를 어떤 Pointcut(핵심사항)에 적용시킬 것 인지에 대한 설정(Advisor)
