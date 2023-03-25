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

- **poly:** many, serveral, much, multi 등과 같은 뜻
- **morphos:** form, structure 등과 같은 뜻
- **polymorphos = poly + morphos:** 여러 다른 구조

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

## Generics

제네릭은 C# 이나 Java 와 같은 언어에서 재사용 가능한 컴포넌트를 만들기 위해 사용하는 기법입니다. 단일 타입이 아닌 다양한 타입에서 작동할 수 있는 컴포넌트를 생성할 수 있습니다.
(구체적인 타입을 지정하지 않고 다양한 인수와 리턴 값에 대한 타입을 처리할 수 있습니다.)
타입스크립트에서 제네릭을 통해 인터페이스, 함수 등의 재사용성을 높일 수 있습니다.

```ts
function identity<Type>(arg: Type): Type {
  return arg;
}

// 제네릭 화살표 함수 (tsx기준)
const identity = <Type extends {}>(arg: Type): Type => {
  return arg;
};

let output = identity<string>('myString'); // 첫 번째 방법
let output = identity('myString'); // 두 번째 방법
```

위에서 두 번째 방법은 type argument inference(타입 인수 유추)를 사용합니다. 즉, 컴파일러가 전달하는 인수 유형에 따라 자동으로 Type 값을 설정하기를 원합니다.

## 참고

- https://www.typescriptlang.org/docs/handbook/2/generics.html#handbook-content
- https://www.typescriptlang.org/docs/handbook/2/generics.html#hello-world-of-generics
