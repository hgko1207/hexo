---
title: 'TypeScript 컴파일러(tsc) 및 tsconfig'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - Programming
  - TypeScript
  - Tsconfig
  - TSC
  - TypeScript Tip
date: 2024-03-11 14:26:16
thumbnail: /images/thumbnail/typescript.png
---

![](/images/header/typescript-9.png)

TypeScript 컴파일러(`tsc`)와 구성 파일(`tsconfig.json`)에 대해 살펴봅니다. 컴파일러 옵션과 구성을 이해하는 것은 TypeScript 워크플로를 최적화하는 데 필수적입니다. 다양한 컴파일러 옵션과 `tsconfig.json`의 중요성, 그리고 이러한 도구를 활용하여 TypeScript 개발 프로세스를 간소화하는 방법을 살펴보세요.

## TypeScript 컴파일러(`tsc`)

### 1. `tsc`란 무엇인가요?

`tsc`는 TypeScript 컴파일러입니다. TypeScript 코드(.ts 또는 .tsx 파일)를 가져와서 JavaScript 런타임에서 실행할 수 있는 JavaScript 코드(.js 파일)로 컴파일합니다.

### 2. `tsc` 설치 방법

npm(Node Package Manager)을 사용하여 `tsc`를 전역적으로 설치할 수 있습니다.

```sh
npm install -g typescript
```

### 3. TypeScript 코드 컴파일

`tsc`를 설치한 후 터미널에서 다음 명령을 실행하여 TypeScript 파일을 컴파일할 수 있습니다.

```sh
tsc yourfile.ts
```

### 4. 컴파일러 옵션

`tsc`에는 컴파일 프로세스를 구성할 수 있는 다양한 컴파일러 옵션이 제공됩니다. 예를 들면 다음과 같습니다.

```sh
tsc - target ES5 - outDir ./dist
```

이 명령은 대상 ECMAScript 버전을 ES5로 설정하고 출력 디렉터리를 './dist'로 지정합니다.

## tsconfig.json

### 1. tsconfig.json이란?

`tsconfig.json`은 TypeScript 프로젝트를 위한 구성 파일입니다. 컴파일러 옵션을 지정하고, 파일을 포함/제외하고, TypeScript 프로젝트에 대한 기타 설정을 구성할 수 있습니다.

### 2. `tsconfig.json` 파일 만들기

프로젝트의 루트에서 `tsconfig.json` 파일을 수동으로 만들거나 `tsc --init` 명령을 사용하여 기본 구성 파일을 생성할 수 있습니다.

### 3. `tsconfig.json`의 컴파일러 옵션

`tsconfig.json`에는 다양한 컴파일러 옵션이 포함될 수 있습니다. 몇 가지 일반적인 옵션은 다음과 같습니다:

- `compilerOptions` : 컴파일러 설정을 지정합니다.
- `include` : 컴파일에 포함할 파일 패턴의 배열을 지정합니다.
- `exclude` : 컴파일에서 제외할 파일 패턴의 배열을 지정합니다.
- `extends` : 다른 구성 파일을 확장할 수 있습니다.

### 4. `tsconfig.json` 예제

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "outDir": "./dist"
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```

이 예에서는 대상을 ES5로, 모듈 시스템을 CommonJS로, 출력 디렉터리를 `"./dist"`로 설정하고, `"src"` 디렉터리에 모든 TypeScript 파일을 포함하며, `"node_modules"` 디렉터리는 제외합니다.

`tsconfig.json`을 사용하면 TypeScript 프로젝트 전체에서 일관된 구성을 유지할 수 있으며, `tsc` 명령을 실행할 때마다 옵션을 지정할 필요가 없으므로 컴파일 프로세스가 간소화됩니다.
