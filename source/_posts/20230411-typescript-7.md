---
title: '[TypeScript] JSDoc Reference 사용 방법'
categories:
  - Programming
  - Language
  - TypeScript
tags:
  - TypeScript
  - JavaScript
  - 타입스크립트
  - 자바스크립트
  - JSDoc
date: 2023-04-11 14:53:58
thumbnail: /images/thumbnail/typescript.png
---

JavaScript 파일에서 TypeScript처럼 코드를 보호받을 수 있도록 하는 방법에 대해 알아보겠습니다.

## @ts-check

JavaScript 파일에서 오류를 활성화하려면 `// @ts-check`를 .js 파일의 첫 번째 줄에 추가하여 TypeScript가 오류를 발생시키도록 합니다. TypeScript는 여러 오류를 제공할 수 있습니다.

아래 코드는 TypeScript와 같이 함수 파라미터에 정의가 되어 있지 않아 오류가 발생합니다.

```js
// @ts-check

// [오류]
export function init(🚫 config) {
  return true;
}

// [오류]
export function exit(🚫 code) {
  return code + 1;
}
```

이러한 오류를 무시하고 싶다면 `// @ts-ignore` 또는 `// @ts-expect-error`를 추가하여 특정 줄의 오류를 무시할 수 있습니다.

## JSDoc Reference

JSDoc 주석을 사용하여 JavaScript 파일에 type 정보를 제공할 수 있습니다. (자바스크립트 파일에서 타입 정보를 제공할 수 있습니다.)

```js
// @ts-check

/**
 * Initializes the project
 * @param {object} config
 * @param {boolean} config.debug
 * @param {string} config.url
 * @returns {boolean}
 */
export function init(config) {
  return true;
}

/**
 * Exits the program
 * @param {number} code
 * @returns {number}
 */
export function exit(code) {
  return code + 1;
}
```

JSDoc 주석을 통해 타입을 정의하고 TypeScript 파일에서 다음과 같이 함수를 사용할 수 있습니다.

```js
init({
  debug: false,
  url: 'true',
});

exit(1);
```

## 주의 사항

- `@ts-check`를 사용하면 JavaScript 파일 내에서 타입 검사를 허용합니다.
- `@ts-check`를 사용하지 않고 JSDoc 만 사용하면 TypeScript 파일에서는 JavaScript의 타입을 검사 하지만, JavaScript 내에서는 단순 주석이나 타입을 명시하는 정도로만 사용할 수 있는 것 같습니다

## 참고

- https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html#ts-check
- https://www.typescriptlang.org/docs/handbook/jsdoc-supported-types.html
