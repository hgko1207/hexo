---
title: '[TypeScript] Function Overloads'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - 타입스크립트
  - Function Overloads
  - Overloading
date: 2023-03-16 14:47:52
thumbnail: /images/thumbnail/typescript.png
---

## Function Overloads

동일한 이름에 매개 변수와 매개 변수 타입 또는 리턴 타입이 다른 여러 버전의 함수를 만드는 것을 말합니다. TypeScript 에서는 오버로드 signatures 을 작성하여 **"다양한 방식으로 호출할 수 있는 함수"**를 지정할 수 있습니다.

## 사용 예제

### 매개변수의 데이터 타입이 다른 경우

매개변수의 데이터 타입이 다른 경우 예외 처리를 합니다.

```ts
type Add = {
  (a: number, b: number): number;
  (a: number, b: string): number;
};

const add: Add = (a, b) => {
  if (typeof b === 'string') return a;
  return a + b;
};

add(1, '2');
add(1, 2);
```

### 매개변수의 수가 다른 경우

매개변수의 수가 다른 경우 예외 처리를 합니다.

```ts
type Add = {
  (a: number, b: number): number;
  (a: number, b: number, c: number): number;
};

const add2: Add = (a, b, c?: number) => {
  if (c) return a + b + c;
  return a + b;
};

add(1, 2);
add(1, 2, 3);
```

## 참고

- https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads
