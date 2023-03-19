---
title: '[TypeScript] 다형성(Polymorphism)'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - Polymorphism
  - 다형성
date: 2023-03-16 14:59:01
thumbnail: /images/thumbnail/typescript.png
---

## 다형성(Polymorphism)

다형성이란, 여러 타입을 받아들임으로써 여러 형태를 가지는 것을 의미합니다.

poly 란?

- many, serveral, much, multi 등과 같은 뜻

morphos 란?

- form, structure 등과 같은 뜻

polymorphos = poly + morphos = 여러 다른 구조

## 예시

```ts
type SuperPrint = {
  (arr: T[]): T;
};

const superPrint: SuperPrint = (arr) => {
  return arr[0];
};

const a = superPrint([1, 2, 3]);
const b = superPrint([true, false, true]);
const c = superPrint(['a', 'b']);
const d = superPrint([1, 2, 'a', 'b', true]);
```

## any, generics 차이점

**any** 를 사용하는 것은 어떤 타입이든 받을 수 있다는 점에서 **generics** 과 같지만 함수를 반환하는데 있어 **any** 는 받았던 인수들의 타입을 활용하지 못합니다.

즉, **generics** 은 어떤 타입이든 받을 수 있다는 점에서 **any** 와 같지만 해당 정보를 잃지 않고 타입에 대한 정보를 다른 쪽으로 전달할 수 있다는 점이 다릅니다.

## 참고

- https://www.typescriptlang.org/docs/handbook/2/generics.html#handbook-content
- https://www.typescriptlang.org/docs/handbook/2/generics.html#hello-world-of-generics
