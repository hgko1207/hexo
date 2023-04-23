---
title: '[TypeScript] 클래스(Class) 사용 방법'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - 타입스크립트
  - Class
  - 클래스
date: 2023-03-29 14:20:34
thumbnail: /images/thumbnail/typescript.png
---

**TypeScript** 에서 클래스(Class)를 생성하고 사용하는 방법에 대해 알아보겠습니다.

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

const eden = new Player();
eden.firstname = 'ko';
eden.lastname = 'eden';
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

const eden = new Player("ko", "eden", "고수");

// [오류]
// firstname는 private 이기 때문에 접근 불가
// javascript 에서는 아무 문제없이 작동함
🚫 eden.firstname;
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

    getFullName() {
      return `${this.firstname} ${this.lastname}`;
    }
  }
}

// [오류]
// TypeScript 가 추상 클래스의 인스턴스를 만들 수 없다고 경고함
🚫 const eden = new User("ko", "eden", "고수");
```

```ts
class Player extends User {
  // 추상 메서드는 추상 클래스를 상속받는 클래스들이 반드시 구현(implement)해야하는 메서드입니다.
  getNickname() {
    console.log(this.nickname);
  }
}

const eden = new Player('ko', 'eden', '고수');
eden.getNickname();
eden.getFullName();
```

추상 클래스를 사용하기 위해서는 상속을 받아 사용합니다.

## Static Members

클래스에는 static 멤버가 있을 수 있습니다. 이 멤버는 클래스의 특정 인스턴스와 연결되지 않습니다. 클래스 생성자 객체 자체를 통해 액세스할 수 있습니다. static 멤버는 동일한 public, protected 및 private 과 함께 사용할 수도 있습니다.

```ts
class MyClass {
  static x = 0;

  static printX() {
    console.log(MyClass.x);
  }
}

console.log(MyClass.x);
MyClass.printX();
```

## 참고

- https://www.typescriptlang.org/docs/handbook/2/classes.html
- https://www.typescriptlang.org/docs/handbook/2/classes.html#static-members
