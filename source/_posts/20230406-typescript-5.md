---
title: '[TypeScript] 인터페이스(Interface) 사용 방법'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - 타입스크립트
  - Interface
  - 인터페이스
date: 2023-04-06 23:20:26
thumbnail: /images/thumbnail/typescript.png
---

**TypeScript** 에서 인터페이스(Interface)를 생성하고 사용하는 방법에 대해 알아보겠습니다.

## Interfaces

객체의 모양을 특정해주기 위해 사용합니다. 여기서는 `firstName` 및 `lastName` 필드가 있는 객체를 설명하는 인터페이스를 사용합니다.

```ts
interface Person {
  firstName: string;
  lastName: string;
}
```

다른 인터페이스를 상속 받아 사용할 수 있습니다.

```ts
interface User {
  name: string;
}

interface Player extends User {}

const hgko: Player = {
  name: 'hgko',
};
```

인터페이스 이름이 같도록 3번 각각 만들어도 타입스크립트는 알아서 하나로 합쳐줍니다. Type 과 차이점입니다.

```ts
interface User {
  name: string;
}

interface User {
  nickname: string;
}

interface User {
  age: number;
}

const hgko: User = {
  name: 'hgko',
  nickname: 'ko',
  age: 30,
};
```

## implements

implements 을 사용하여 클래스가 특정 인터페이스를 충족하는지 확인할 수 있습니다.
클래스를 올바르게 구현하지 못하면 오류가 발생합니다.

implements 절은 클래스가 인터페이스 유형으로 처리될 수 있는지 확인하는 것입니다. 클래스의 유형이나 메서드는 전혀 변경하지 않습니다.
또한 클래스는 여러 인터페이스를 구현할 수도 있습니다.

```ts
// ex) 클래스 C 는 A, B 를 구현합니다.
class C implements A, B {}
```

```ts
interface Pingable {
  ping(): void;
}

// Sonar 클래스는 Pingable 인터페이스를 implement 했기 때문에
// Pingable 가 가진 ping 메서드를 구현해줘야 합니다.
class Sonar implements Pingable {
  ping() {
    console.log('ping!');
  }
}
```

여러 개의 인터페이스를 상속받아 사용할 수 있습니다.

```ts
interface User {
  firstName: string;
  lastName: string;
}

interface Human {
  health: number;
}

class Player implements User, Human {
  constructor(
    public firstName: string, 
    public lastName: string, 
    public health: number
  ) {}
}
```

## Type Aliases 과 Interfaces 의 차이점

Type Aliases 과 인터페이스는 매우 유사하며 많은 경우 자유롭게 선택할 수 있습니다. 인터페이스의 거의 모든 기능은 type 에서 사용할 수 있으며, 주요 차이점은 type 을 다시 열어 새 속성을 추가할 수 없는 것입니다. 반면 인터페이스는 항상 확장 가능합니다.

## 참고

- https://www.typescriptlang.org/docs/handbook/typescript-tooling-in-5-minutes.html#interfaces
- https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces