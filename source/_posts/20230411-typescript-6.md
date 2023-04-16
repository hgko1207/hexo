---
title: '[TypeScript] 설치 및 설정 방법'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - 타입스크립트
  - 설치
  - 설정
date: 2023-04-11 11:10:23
thumbnail: /images/thumbnail/typescript.png
---

NextJS, Create React App(CRA) 를 사용하지 않고 초기 프로젝트에 TypeScript 를 설치하고 설정하는 방법에 대해 알아보겠습니다.

## 프로젝트 시작

프로젝트 디렉터리를 생성합니다.

```bash
$ mkdir typescripttest
$ cd typescripttest
```

아래 명령어를 사용하여 package.json 을 초기화합니다.

```bash
$ npm init -y
```

## TypeScript 설치

명령어를 사용하여 TypeScript를 설치합니다.

```bash
$ npm i -D typescript
```

## tsconfig.json 설정

TypeScript 설정은 tsconfig.json 파일에서 합니다. 디렉터리에 tsconfig.json 파일이 있으면 해당 디렉터리가 TypeScript 프로젝트의 루트임을 나타냅니다. tsconfig.json 파일은 프로젝트를 컴파일하는 데 필요한 루트 파일과 컴파일러 옵션을 지정합니다.

tsconfig.json 파일을 생성합니다. 다음과 같이 기본적인 설정을 작성합니다.

```json
// tsconfig.json
{
  "include": ["src"], // 자바스크립트로 컴파일 하고 싶은 모든 디렉터리
  "compilerOptions": {
    "outDir": "build" // 자바스크립트 파일로 생성될 디렉터리(빌드 디렉터리)
  }
}
```

아래의 명령어로도 기본적인 tsconfig.json 파일 생성이 가능합니다.

```bash
$ npm i -g typescript
$ tsc --init
```

### Target (기본값: ES3)

최신 브라우저는 모든 ES6 기능을 지원하므로 ES6 는 좋은 선택입니다. 코드가 이전 환경에 배포된 경우 더 낮은 target 을 설정하거나 최신 환경에서 코드 실행이 보장되는 경우 더 높은 target 을 설정하도록 선택할 수 있습니다.

```json
// tsconfig.json
{
  "include": ["src"],
  "compilerOptions": {
    "outDir": "build",
    "target": "ES6"
  }
}
```

### Lib(라이브러리)

타입스크립트에게 어떤 API를 사용하고 어떤 환경에서 코드를 실행하는 지를 지정할 수 있습니다. (target 런타임 환경이 무엇인지를 지정합니다.)

프로그램이 브라우저에서 실행되면 lib에 "DOM" 유형 정의를 할 수 있습니다.

- DOM: window, document 등

```json
// ex)
{
  "compilerOptions": {
    "lib": ["ES6", "DOM"]
  }
}
```

### strict

모든 엄격한 타입 검사 옵션을 활성화합니다. `strict` 플래그는 프로그램 정확성을 더 강력하게 보장하는 광범위한 타입 검사 동작을 가능하게 합니다.

tsconfig.json 에서 `"strict": true` 를 통해 strict mode 로 해주면, Declaration Files 가 없는 경우에 대해서도 에러를 띄워줍니다.

```json
{
  "compilerOptions": {
    "strict": true
  }
}
```

## 참고

- https://www.typescriptlang.org/docs/handbook/tsconfig-json.html#handbook-content
- https://www.typescriptlang.org/tsconfig#target
- https://www.typescriptlang.org/tsconfig#lib
- https://www.typescriptlang.org/tsconfig#strict
