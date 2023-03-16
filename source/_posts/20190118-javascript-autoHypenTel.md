---
title: '[JavaScript] 전화번호 하이픈(-) 자동입력'
categories:
  - Programming
  - Language
  - JavaScript
tags:
  - JavaScript
  - Hypen
  - input
  - HTML
  - 자바스크립트
  - 전화번호
date: 2019-01-18 15:22:36
thumbnail: /images/thumbnail/javascript.png
---

사용자 등록 시 전화번호를 입력하게 되는데 아래 그림처럼 세 개의 입력을 받아 합치는 형식으로 많이 되어 있습니다.

<img width="65%" src="/images/javascript/hypen-1.png" alt="연락처 입력" title="" >

이렇게 개발해도 괜찮지만 좀 더 쉽게 하기 위해서 전화번호 입력 시 자동으로 하이픈(-)이 입력되도록 하는 형식으로 바꾸면 좋겠다 싶어 반영해봤습니다.
개발 된 화면은 다음과 같습니다.

<img width="75%" src="/images/javascript/hypen-2.png" alt="" title="" >

## 1) HTML

먼저 HTML 소스 코드입니다. **input** 태그를 사용하고 **pattern**과 **maxlength**, **required**, **placeholder**를 사용하였습니다. 속성에 대한 설명은 참고 사이트를 보시면 됩니다.

```html
<input
  type="tel"
  class="form-control m-input"
  name="tel"
  id="telInput"
  required
  pattern="[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}"
  maxlength="13"
  placeholder="예) 010-1234-5678"
/>
```

## 2) JavaScript

먼저 전화번호 크기에 따라 나눴습니다. 서울 전화번호는 02로 두자리로 시작하고 핸드폰은 010, 011.. 이고 다른 지역 전화번호는 031, 041, 051 등 세자리로 시작하여 {2}-{3 or 4}-{4} 또는 {3}-{3 or 4}-{4} 형태가 되도록 문자열을 잘라내는 방식으로 하였습니다.

```js
function autoHypenTel(str) {
  str = str.replace(/[^0-9]/g, '');
  var tmp = '';

  if (str.substring(0, 2) == 02) {
    // 서울 전화번호일 경우 10자리까지만 나타나고 그 이상의 자리수는 자동삭제
    if (str.length < 3) {
      return str;
    } else if (str.length < 6) {
      tmp += str.substr(0, 2);
      tmp += '-';
      tmp += str.substr(2);
      return tmp;
    } else if (str.length < 10) {
      tmp += str.substr(0, 2);
      tmp += '-';
      tmp += str.substr(2, 3);
      tmp += '-';
      tmp += str.substr(5);
      return tmp;
    } else {
      tmp += str.substr(0, 2);
      tmp += '-';
      tmp += str.substr(2, 4);
      tmp += '-';
      tmp += str.substr(6, 4);
      return tmp;
    }
  } else {
    // 핸드폰 및 다른 지역 전화번호 일 경우
    if (str.length < 4) {
      return str;
    } else if (str.length < 7) {
      tmp += str.substr(0, 3);
      tmp += '-';
      tmp += str.substr(3);
      return tmp;
    } else if (str.length < 11) {
      tmp += str.substr(0, 3);
      tmp += '-';
      tmp += str.substr(3, 3);
      tmp += '-';
      tmp += str.substr(6);
      return tmp;
    } else {
      tmp += str.substr(0, 3);
      tmp += '-';
      tmp += str.substr(3, 4);
      tmp += '-';
      tmp += str.substr(7);
      return tmp;
    }
  }

  return str;
}
```

호출 부분 코드입니다. 키가 입력될 때마다 검사를 진행합니다.

```js
$('#telInput').keyup(function (event) {
  event = event || window.event;
  var _val = this.value.trim();
  this.value = autoHypenTel(_val);
});
```

전화번호 시작이 1588, 1668 등과 같은 번호 일 경우에 대해서는 작성하지 않았습니다. 보다시피 완벽하게 최적화가 되지 않았기 때문에 추후에 수정이 될 것 같습니다.

## 참고

- [HTML Input 속성들(Attributes)](http://jun.hansung.ac.kr/CWP/htmls/HTML%20Input%20Attributes.html)
- [핸드폰 번호 하이픈(-) 자동입력](https://mulder21c.github.io/2014/11/03/automatically-enter-cell-phone-number-hyphen/)
- [전화번호 입력시 하이픈(-) 자동 입력](http://www.blueb.co.kr/?c=1/9&cat=Form+Check&uid=2077)
