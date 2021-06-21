---
title: '[JavaScript] 우편번호 주소 조회'
categories:
  - Web
  - JavaScript
tags:
  - JavaScript
  - Postcode
  - Address
  - Daum
  - kakao
  - 우편번호 서비스
date: 2019-01-18 15:52:14
thumbnail: /images/thumbnail/javascript.png
---

웹 프로젝트를 하면서 사용자 등록을 하게 될 때 주소를 입력을 하게 되는데, 우편번호 주소 조회가 되도록 처리해달라는 요청이 있었습니다. 그래서 우편번호 서비스를 검색해 봤을 때 여러가지가 있었지만 개인적으로 좋아보이는 **Daum 우편번호 서비스**를 사용하게 되었습니다.

### Daum 우편번호 서비스

- 쉽고 간편하게 우편번호 검색, 도로명 주소 입력 기능을 만들 수 있습니다.
- Key를 발급받을 필요가 없습니다.
- 사용량에 대한 제한이 전혀 없습니다.
- 기업용이든 상업적 용도이든 상관없이 무조건 무료로 사용 가능합니다.
- 도로명 주소, 지번 주소, 영문 주소까지 모두 확인 가능합니다.

이 것 말고도 여러 가지 장점이 더 있지만 사용하기 쉽고 무료이며 사용량에 대한 제한이 없고, 특히나 기본 사용법이 정말 쉽게 잘 설명되어 있어서 사용하게 되었습니다.

<img width="100%" src="/images/javascript/postcode-1.png" alt="Daum 우편번호 서비스" title="" >

아래는 적용한 코드입니다.

## 1) HTML

부끄럽지만 HTML 코드는 아래와 같습니다. **우편번호**, **도로명 주소**, **상세 주소** 입력 란이 있고 **우편번호 찾기** 버튼이 있습니다. 버튼을 클릭하게 되면 **execDaumPostcode()** 함수를 호출하게 됩니다.

```html
<div class="form-group m-form__group row">
  <label class="col-md-2 offset-md-3 col-form-label">
    주&nbsp;&nbsp;소&nbsp;&nbsp;<span class="m--font-orange vertical-middle">*</span>
  </label>
  <div class="col-md-2">
    <input type="text" class="form-control m-input" name="postcode" id="postcode" placeholder="우편번호" readonly />
  </div>
  <div class="col-md-2 postcode-btn">
    <button type="button" class="btn btn-info m-btn--air" onclick="execDaumPostcode()">우편번호 찾기</button>
  </div>
  <div class="col-md-4 offset-md-5">
    <input
      type="text"
      class="form-control m-input m--margin-top-10"
      name="address"
      id="address"
      placeholder="도로명 주소"
      readonly
    />
  </div>
  <div class="col-md-4 offset-md-5">
    <input
      type="text"
      class="form-control m-input m--margin-top-10"
      name="detailAddress"
      placeholder="상세 주소"
      required
    />
  </div>
</div>
```

결과 화면입니다.

<img width="100%" src="/images/javascript/postcode-2.png" alt="우편번호 찾기 화면" title="" >

## 2) JavaScript

버튼을 클릭하여 `execDaumPostcode()` 함수가 호출되면서 주소 검색 팝업창이 보여지게 합니다. 팝업팡에서 주소 검색 결과 항목을 클릭했을 때 우편번호와 도로명주소 입력란에 값을 채워넣게 됩니다.

```JS
<!--autoload=false 파라미터를 이용하여 자동으로 로딩되는 것을 막습니다.-->
<script src="http://dmaps.daum.net/map_js_init/postcode.v2.js?autoload=false"></script>

<script>
/** 우편번호 찾기 */
function execDaumPostcode() {
    daum.postcode.load(function(){
        new daum.Postcode({
            oncomplete: function(data) {
              // 팝업에서 검색결과 항목을 클릭했을때 실행할 코드를 작성하는 부분입니다.
              $("#postcode").val(data.zonecode);
              $("#address").val(data.roadAddress);
            }
        }).open();
    });
}
</script>
```

Daum 우편번호 서비스를 사용하여 주소를 검색하고 우편번호와 도로명 주소를 받아 입력란에 넣어줬습니다. Daum 우편번호 서비스 사이트 가시면 예제와 속성, 함수에 대한 부분도 잘 설명 되어 있기 때문에 다양하게 개발할 수 있습니다.

## 참고

- [Daum 우편번호 서비스](http://postcode.map.daum.net/guide)
- [Daum 우편번호 서비스 사용 가이드 - 우편번호 검색, 적용법 및 사용예제](http://chongmoa.com/javascript/28679)
