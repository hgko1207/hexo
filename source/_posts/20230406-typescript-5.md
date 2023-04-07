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

객체의 모양을 특정해주기 위해 사용합니다. 여기서는 firstName 및 lastName 필드가 있는 객체를 설명하는 인터페이스를 사용합니다.

```ts
interface Person {
  firstName: string;
  lastName: string;
}
```

## 참고

- https://www.typescriptlang.org/docs/handbook/typescript-tooling-in-5-minutes.html#interfaces
