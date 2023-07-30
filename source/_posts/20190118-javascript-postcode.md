---
title: '[JavaScript] Daum 우편번호 서비스 사용 방법'
categories:
  - Programming
  - Language
  - JavaScript
tags:
  - JavaScript
  - Address
  - JQuery
  - Daum 우편번호
  - kakao
  - 우편번호 서비스
  - 자바스크립트
date: 2019-01-18 15:52:14
thumbnail: /images/thumbnail/javascript.png
---

웹 프로젝트를 하면서 사용자 등록을 하게 될 때 주소를 입력을 하게 되는데, 우편번호 주소 조회가 되도록 처리해달라는 요청이 있었다. 그래서 우편번호 서비스를 검색해 봤을 때 여러가지가 있었지만 개인적으로 좋아보이는 **Daum 우편번호 서비스**를 사용하게 되었다.

## Daum 우편번호 서비스

- 쉽고 간편하게 우편번호 검색, 도로명 주소 입력 기능을 만들 수 있다.
- Key 를 발급받을 필요가 없다.
- 사용량에 대한 제한이 전혀 없다.
- 기업용이든 상업적 용도이든 상관없이 무조건 무료로 사용 가능하다.
- 도로명 주소, 지번 주소, 영문 주소까지 모두 확인 가능하다.

이 것 말고도 여러 가지 장점이 더 있지만 사용하기 쉽고 무료이며 사용량에 대한 제한이 없고, 특히나 기본 사용법이 정말 쉽게 잘 설명되어 있어서 사용하게 되었다.

[![Daum 우편번호 서비스](/images/javascript/postcode-1.png)](https://postcode.map.daum.net/guide#usage)

### 예제

```js
<script src="//t1.daumcdn.net/mapjsapi/bundle/postcode/prod/postcode.v2.js"></script>
<script>
    new daum.Postcode({
        oncomplete: function(data) {
            // 팝업에서 검색결과 항목을 클릭했을때 실행할 코드를 작성하는 부분입니다.
            // 예제를 참고하여 다양한 활용법을 확인해 보세요.
        }
    }).open();
</script>
```

## 적용

다음은 적용한 코드다.

### HTML

HTML 코드는 다음과 같다. **우편번호**, **도로명 주소**, **상세 주소** 입력 란이 있고 **우편번호 찾기** 버튼이 있다. 버튼을 클릭하게 되면 **execDaumPostcode()** 함수를 호출하게 된다.

```html
<div class="form-group row">
  <label class="col-md-2 offset-md-3 form-label"> 주 소 <span class="text-danger">*</span> </label>
  <div class="col-md-2">
    <input type="text" class="form-control" name="postcode" id="postcode" placeholder="우편번호" readonly />
  </div>
  <div class="col-md-2 postcode-btn">
    <button type="button" class="btn btn-info" onclick="execDaumPostcode()">우편번호 찾기</button>
  </div>
  <div class="offset-md-5 col-md-4 mt-2">
    <input type="text" class="form-control" name="address" id="address" placeholder="도로명 주소" readonly />
  </div>
  <div class="offset-md-5 col-md-4 mt-2">
    <input
      type="text"
      class="form-control"
      id="detailA_address"
      name="detailAddress"
      placeholder="상세 주소"
      required
    />
  </div>
</div>
```

결과 화면이다.

<img width="100%" src="/images/javascript/postcode-2.png" alt="우편번호 찾기 화면" title="" >

### JavaScript

버튼을 클릭하여 `execDaumPostcode()` 함수가 호출되면서 주소 검색 팝업창이 보여지게 한다. 팝업팡에서 주소 검색 결과 항목을 클릭했을 때 우편번호와 도로명주소 입력란에 값을 채워넣게 된다.

```js
<script src="//t1.daumcdn.net/mapjsapi/bundle/postcode/prod/postcode.v2.js"></script>

<script>
/** 우편번호 찾기 */
function execDaumPostcode() {
      new daum.Postcode({
          oncomplete: function(data) {
            // 팝업에서 검색결과 항목을 클릭했을때 실행할 코드를 작성하는 부분입니다.

            // 각 주소의 노출 규칙에 따라 주소를 조합한다.
            // 내려오는 변수가 값이 없는 경우엔 공백('')값을 가지므로, 이를 참고하여 분기 한다.
            let addr = ''; // 주소 변수

            //사용자가 선택한 주소 타입에 따라 해당 주소 값을 가져온다.
            if (data.userSelectedType === 'R') { // 사용자가 도로명 주소를 선택했을 경우
                addr = data.roadAddress;
            } else { // 사용자가 지번 주소를 선택했을 경우(J)
                addr = data.jibunAddress;
            }

            $("#postcode").val(data.zonecode);
            $("#address").val(addr);
            $("#address").focus();
          }
      }).open();
}
</script>
```

Daum 우편번호 서비스를 사용하여 주소를 검색하고 우편번호와 도로명 주소를 받아 입력란에 넣어줬다. Daum 우편번호 서비스 사이트 가시면 예제와 속성, 함수에 대한 부분도 잘 설명 되어 있기 때문에 다양하게 개발할 수 있다.

## 참고

- [Daum 우편번호 서비스](http://postcode.map.daum.net/guide)
- [Daum 우편번호 서비스 사용 가이드 - 우편번호 검색, 적용법 및 사용예제](http://chongmoa.com/javascript/28679)
