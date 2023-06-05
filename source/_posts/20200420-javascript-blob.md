---
title: '[JavaScript] IE에서 작동하지 않는 BLOB 다운로드'
categories:
  - Programming
  - Language
  - JavaScript
tags:
  - JavaScript
  - Download
  - 자바스크립트
date: 2020-04-20 09:56:01
thumbnail: /images/thumbnail/javascript.png
---

이미지를 Jcrop 라이브러리를 사용하여 자르고 **Canvas** 영역을 blob 형식으로 바꿔서 `a` Tag 를 생성하여 다운로드를 시도하였습니다. 크롬에서는 잘 동작하였지만 IE 에서는 동작하지 않고 에러를 발생하였습니다.

아래 코드처럼 작성하였더니 둘 다 동작하였습니다.

## 소스 코드

```js
function downloadURI(blob, name) {
  if (window.navigator && window.navigator.msSaveOrOpenBlob) {
    // IE에서 동작
    window.navigator.msSaveBlob(blob, name);
  } else {
    // 크롬에서 동작
    var link = document.createElement('a');
    link.download = name;
    link.href = URL.createObjectURL(blob);
    link.click();
    delete link;
  }
}
```
