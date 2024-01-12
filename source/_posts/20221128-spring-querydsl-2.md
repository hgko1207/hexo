---
title: '[Spring] QuerydslRepositorySupport 사용'
categories:
  - Programming
  - Backend
  - Spring
tags:
  - Spring
  - Querydsl
  - QuerydslRepositorySupport
date: 2022-11-28 11:45:08
thumbnail: /images/thumbnail/spring.png
---

`QueryDslPredicateExecutor`를 이용하는 findAll, findOne 등은 where, Sort, Limit 등의 조건만 넣을 수 있습니다. 하지만 Join이나 Group by 등의 기능을 사용하려면 인터페이스 선언만으로는 기능을 구현하기 힘듭니다.

이를 해결하기 위해서 **Spring Data JPA**에서 제공하는 `QuerydslRepositorySupport` 추상 클래스가 있습니다. `QuerydslRepositorySupport`는 개발자에게 querydsl 객체를 직접 제공합니다.

예를 들어 권한별 사용자 수에 대한 데이터가 필요하다면, 다음과 같이 할 수 있습니다.

사용자 클래스와 DTO 클래스를 생성합니다.

```java
@Data
@Entity
@Table
public class User {

  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private long id;

  @Column(nullable = false, length = 50)
  private String username;

  @Column(nullable = false, length = 50)
  private String password;

  private int role;
}
```

```java
@Data
public class UserRoleCountDTO {

  private int role;

  private long count;

  public UserRoleCountDTO(int role, long count) {
    this.role = role;
    this.count = count;
  }
}
```

권한별 사용자 수를 얻어오는 인터페이스를 생성하고 메소드를 선언합니다.

```java
public interface UserRepositoryCustom {
  List<UserRoleCountDTO> getUserRoleCount();
}
```

`UserRepository`에 상속 시킵니다.

```java
public interface UserRepository extends JpaRepository<User, Long>, UserRepositoryCustom {
}
```

`QuerydslRepositorySupport`를 이용해서 `UserRepositoryCustom`를 구현하는 클래스를 작성합니다.
`UserRepository` 이름 뒤에 Impl이라는 Postfix 가 붙으면 자동으로 Spring Data JPA의 AOP 주입 대상이 됩니다.

```java
public class UserRepositoryImpl extends QuerydslRepositorySupport implements UserRepositoryCustom {

  public UserRepositoryImpl() {
    super(User.class);
  }

  @Override
  public List<UserRoleCountDTO> getUserRoleCount() {
    QUser user = QUser.user;
    return from(user).groupBy(user.role)
                  .list(Projections.constructor(UserRoleCountDTO.class, user.role, user.role.sum));
  }
}
```

위의 예제를 통해 JpaRepository의 기능과 추가로 구현한 UserRepositoryCustom의 추가 기능까지 사용할 수 있습니다.

```java
@Service
@RequiredArgsConstructor
public class UserService {

  private final UserRepository userRepository;

  public void testQuery() {
    List<UserRoleCountDTO> userRoleCountDTOs = userRepository.getUserRoleCount();
    System.out.println("result =>" + userRoleCountDTOs);
  }
}
```
