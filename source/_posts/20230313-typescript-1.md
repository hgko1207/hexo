---
title: '[TypeScript] Types'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - Types
date: 2023-03-13 13:56:29
thumbnail: /images/thumbnail/typescript.png
---

## 타입스크립트란?

TypeScript 는 JavaScript 에 추가적인 구문을 추가하여 editor 와의 단단한 통합을 지원합니다. editor 에서 초기에 오류를 잡을 수 있습니다.

TypeScript 코드는 JavaScript 가 실행되는 모든 곳(브라우저, Node.js 또는 Deno 및 앱 등)에서 JavaScript 로 변환될 수 있습니다.

TypeScript 는 JavaScript 를 이해하고 타입 추론(type inference)을 사용하여 추가 코드 없이도 훌륭한 도구를 제공합니다.

## Types(기본)

- ✅ 배열: 자료형[]
- ✅ 숫자: number
- ✅ 문자열: string
- ✅ 논리: boolean

```ts
type Player = {
  name: string;
  age: number;
  weapons: string[];
  attack: bool;
};
```

## optional 사용

?를 :앞에 붙이면 optional 사용 가능합니다.

```ts
const player: {
  name: string;
  age?: number;
} = {
  name: 'hgko',
};
```

위와 같이 `player.age` 를 optional 로 설정할 경우 Typescript 는 `player.age` 가 undefined 일수도 있다고 오류를 알려줍니다.

```ts
// ❌ player.age 가 undefined 일 가능성 알림
if (player.age < 10) {
}
```

`player.age` 가 존재하는지 확인을 거쳐야 오류 알림이 사라집니다.

```ts
// ⭕ player.age 가 undefined 일 가능성 체크
if (player.age && player.age < 10) {
}
```

## Alias(별칭) 타입

```ts
type Player = {
  name: string;
  age?: number;
};

const player: Player = {
  name: 'hgko',
};
```

## readonly 사용

변수 또는 별칭 앞에 `readonly` 를 붙이면 readonly 사용 가능합니다.

```ts
type Player = {
  readonly name: string;
  age?: number;
};
```

`readonly` 가 있으면 최초 선언 후 수정 불가합니다. 불변성(immutability)이 부여됩니다. 하지만 javascript 에서는 그냥 배열로 인식하여 수정이 됩니다.

```ts
const playerMaker = (name: string): Player => ({ name });

const player = playerMaker('hgko');
// [오류]
🚫 player.name = "khk"

const numbers: readonly number[] = [1, 2, 3, 4];
// [오류]
🚫 numbers.push(5)
```

## Tuple 타입

정해진 개수와 순서에 따라 배열 선언이 가능합니다.

```ts
const player: [string, number, boolean] = ['hgko', 1, true];
// [오류]
🚫 player[0] = 1 // 바꿀 수 없습니다. string으로 지정됨
```

readonly 도 사용 가능 합니다.

```ts
const player: readonly [string, number, boolean] = ['hgko', 1, true];
```

## any / undefined / null 타입

- ✅ any: 어떠한 타입도 허용

```ts
const a: any[] = [1, 2, 3, 4];
const b: any = true;
```

- ✅ undefined: undefined 값만 가질 수 있음
- ✅ null: null 값만 가질 수 있음

```ts
let nullable: null = null;
let undefinedable: undefined = undefined;

// [오류]
// 'undefined' 형식은 'null' 형식에 할당할 수 없습니다.
🚫 nullable = undefined;
```

## void 타입

**void** 는 값을 반환하지 않는 함수의 반환 값을 나타냅니다. 함수에 return 문이 없거나 해당 return 문에서 명시적 값을 반환하지 않을 때 항상 유추되는 타입입니다.

```ts
// The inferred return type is void
function noop() {
  return;
}
```

```ts
function test() {
    console.log('x')
}

const a = test()
// [오류]
🚫 a.toUpperCase()
```

## unknown 타입

**unknown** 타입은 모든 값을 나타냅니다. 이것은 any 타입과 비슷하지만 any 보다 unknown 이 더 안전합니다. 이유는 unknown 값으로 작업을 수행하는 것은 합법적이지 않기 때문입니다.

```ts
function test(a: any) {
  a.b(); // OK
}

function test2(a: unknown) {
  🚫 a.b(); // 에러: Object is of type 'unknown'.
}
```

## never 타입

**never** 타입은 모든 타입에 할당 가능한 하위 타입이나, never 타입에는 본인 외에 다른 타입이 할당될 수는 없습니다. never 타입은 절대 발생할 수 없는 타입을 나타냅니다.

가장 흔한 예제로는 에러를 발생시킬 때 사용됩니다.

```ts
function fail(msg: string): never {
  throw new Error(msg);
}
```

사용법에 대해 좀 더 찾아봐야겠지만 그 외에도 특정 타입 값을 할당받지 않도록 하거나, 매개변수의 제한을 건다거나 뭐 그런 곳들에 사용된다는데, 사실 많이 사용하는 타입은 아니라고 봐도 무방합니다.

## 참고

- [타입스크립트 코드 테스트](https://www.typescriptlang.org/play)
- [타입스크립트 핸드북](https://typescript-kr.github.io/pages/basic-types.html)
