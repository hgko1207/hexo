---
title: '[TypeScript] Classes'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - Classes
  - 클래스
date: 2023-03-29 14:20:34
thumbnail: /images/thumbnail/typescript.png
---

TypeScript 에서 클래스를 생성하고 사용하는 방법에 대해 알아보겠습니다.

## 클래스(Class)

가장 기본적인 클래스입니다.

```ts
class Player {}
```

필드를 선언해서 사용 가능합니다.

```ts
class Player {
  firstname: string;
  lastname: string;
}

const hgko = new Player();
hgko.firstname = 'ko';
hgko.lastname = 'hg';
```

생성자에 매개변수를 추가해서 선언할 수 있습니다.

```ts
class Player {
  constructor(
    private firstname: string,
    private lastname: string,
    public nickname: string
  ) {}
}

const hgko = new Player("ko", "hg", "고수");

// [오류]
// firstname는 private 이기 때문에 접근 불가
// javascript 에서는 아무 문제없이 작동함
🚫 hgko.firstname;
```

- public: 모든 클래스에서 접근 가능
- private: 해당 클래스 내에서만 접근 가능 (자식 클래스에서도 접근 불가)
- protected: 해당 클래스와 자식 클래스에서 접근 가능

## 추상 클래스(Abstract Class)

TypeScript 와 객체지향 프로그램이 가지고 있는 엄청 훌륭한 것은 추상 클래스(Abstract Class)라고 생각됩니다.

추상클래스는 다른 클래스가 상속받을 수 있는 클래스입니다. 하지만 이 클래스는 직접 새로운 인스턴스를 만들 수는 없습니다.

```ts
abstract class User {
  constructor(
    private firstname: string,
    private lastname: string,
    public nickname: string
  ) {
    abstract getNickname(): void
  }
}

// [오류]
// TypeScript 가 추상 클래스의 인스턴스를 만들 수 없다고 경고함
🚫 const hgko = new User("ko", "hg", "고수");
```

```ts
class Player extends User {
  // 추상 메서드는 추상 클래스를 상속받는 클래스들이 반드시 구현(implement)해야하는 메서드입니다.
  getNickname() {
    console.log(this.nickname);
  }
}

const hgko = new Player('ko', 'hg', '고수');
hgko.getNickname();
```

추상 클래스를 사용하기 위해서는 상속을 받아 사용합니다.

## 참고

- https://www.typescriptlang.org/docs/handbook/2/classes.html
