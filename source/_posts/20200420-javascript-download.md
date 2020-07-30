---
title: '[JavaScript] IE에서 작동하지 않는 BLOB 다운로드'
categories:
  - Web
  - JavaScript
tags:
  - JavaScript
  - BLOB
  - Download
date: 2020-04-20 09:56:01
thumbnail:
---

이미지를 Jcrop 으로 자르고 Canvas 영역을 blob 형식으로 바꿔서 a Tag를 생성하여 다운로드를 시도하였습니다. 크롬에서는 잘 동작하였지만 IE에서는 동작하지 않고 에러를 발생하였습니다.

그래서 아래 코드처럼 변형을 하였더니 둘다 잘 동작하였습니다.

##### 이미지 다운로드

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
