---
title: '[Android Studio] lombok 사용 방법'
categories:
  - Programming
  - Mobile
  - Android
tags:
  - Android Studio
  - Android
  - lombok
  - Java
  - 안드로이드
date: 2020-04-18 20:14:23
thumbnail: /images/thumbnail/androidstudio.png
---

자바에서 코드를 작성 시 모델을 만들다 보면 constructor와 기본 getter/setter 그리고 상황에 따라서 builder를 만들어 사용해야 합니다.
그런데 이런 일들을 모두 타이핑 하다 보니 보일러플레이트 같은 코드들이 많이도 써야 합니다.
lombok를 사용하면 모델 객체들의 불필요한 보일러플레이트 코드들을 줄일 수 있습니다.
annotation 방법으로 사용하기 때문에 사용 방법도 간단합니다.

#### lombok annotation

1. **@Getter / @Setter**
   기본적으로 멤버 필드들에 대한 getter/setter 메소드들을 만들어 줍니다.
   <br/>
2. **@AllArgsConstructor / @NoArgsConstructor**
   멤버필드들이 모두 파라미터로 지정된 생성자와 빈 생성자를 만들어 줍니다.
   <br/>
3. **@Builder**
   모델을 빌더 패턴으로 만들어 줍니다.
   <br/>
4. **@ToString**
   toString의 override된 메소드를 만들어 줍니다.
   <br/>
5. **@Data**
   @ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor를 합쳐 둔 어노테이션입니다.
   <br/>
6. **@EqualsAndHashCode**
   해당 객체의 equals()와 hashCode() 메소드를 생성합니다.

그 외에도 여러가지가 있습니다.

그럼 AndroidStudio에 적용하는 방법을 알아봅니다.

#### 적용 방법

1. 우선 lombok plugin을 설치해야 합니다.

   `File -> Settings -> Plugins -> Browse repositories lombok`을 검색하여 Lombok Plugin을 설치합니다.

<img width="100%" src="/images/lombok/lombok1.png" alt="" title="" >

2. gradle에 lombok 적용하기
   Gradle Scripts -> build.gradle 파일을 엽니다.
   <br/>
3. dependencies 아래에 추가해줍니다.

```js
compileOnly 'org.projectlombok:lombok:1.18.12'
annotationProcessor 'org.projectlombok:lombok:1.18.12'
```

이와같은 과정 후에 아래와 같은 결과를 볼 수 있습니다.

### 결과

<img width="100%" src="/images/lombok/lombok2.png" alt="" title="" >
