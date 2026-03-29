# Hexo 블로그 개선 플랜

> 프로젝트: d:\01. hgko\Blog\blog
> 테마: Hueman | Hexo 4.2.1 | GitHub Pages 배포
> 포스트: 521개 | URL: https://hgko1207.github.io/
> 작성일: 2026-03-29

---

## 완료된 항목

- [x] 1-1. language: en -> ko 변경 (`_config.yml`)
- [x] 1-2. word_count(읽기 시간) 활성화 (`themes/hueman/_config.yml` counter: true + hexo-wordcount 설치)
- [x] 2-1. google-analytics.ejs를 GA4 gtag.js 방식으로 교체
- [x] 3-1. Open Graph / Twitter Card 메타태그 보강 (twitter_card: summary_large_image 추가)
- [x] 3-2. meta description 자동 생성 추가 (head.ejs)
- [x] 3-3. sitemap에서 tag: true, category: true로 크롤링 범위 확대
- [x] 4-1~4-4. Giscus 댓글 시스템 추가 (giscus.ejs 생성, comment/index.ejs 분기 추가, 테마 설정 추가)
- [x] 5-1. AdSense 사이드바 위젯에 publisher_id/ad_slot 설정
- [x] 5-2. 쿠팡 파트너스 광고 활성화 (article.ejs 주석 해제)
- [x] 6-1. hexo clean && hexo generate 빌드 성공 (2612 파일, 에러 없음)

---

## 다음 작업 (구현 예정)

### 단계 1: 기본 설정 수정 (즉시 적용)

#### 1-1. language: en -> ko 변경
- **파일**: `_config.yml` (10번째 줄)
- **변경**: `language: en` -> `language: ko`
- **목적**: 블로그 UI 텍스트(아카이브, 카테고리, 태그 등)를 한국어로 표시
- **참고**: 테마에 `themes/hueman/languages/ko.yml` 파일이 이미 존재하므로 설정만 변경하면 됨. head.ejs에는 이미 `<html lang="ko">`로 하드코딩되어 있음

#### 1-2. word_count(읽기 시간) 활성화
- **파일**: `themes/hueman/_config.yml` (112번째 줄)
- **변경**: `counter: false` -> `counter: true`
- **목적**: 각 포스트에 글자 수와 예상 읽기 시간 표시
- **참고**: 레이아웃 `themes/hueman/layout/common/post/counter.ejs`에 이미 구현되어 있음. `hexo-wordcount` 플러그인 설치 필요 (`npm install hexo-wordcount --save`)
- **구현 파일**: `themes/hueman/layout/common/post/counter.ejs` (wordcount, min2read 함수 사용)

---

### 단계 2: Google Analytics GA4 전환

#### 2-1. google-analytics.ejs를 GA4 gtag.js 방식으로 교체
- **파일**: `themes/hueman/layout/plugin/google-analytics.ejs`
- **현재 코드**: UA 방식 (`analytics.js`, `ga('create', ...)`) -- UA 서비스 종료됨
- **변경 내용**: 아래 GA4 gtag.js 코드로 전체 교체
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=<%= theme.plugins.google_analytics %>"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', '<%= theme.plugins.google_analytics %>');
</script>
```
- **목적**: UA 서비스 종료에 따른 GA4 전환으로 방문자 분석 재개

#### 2-2. GA4 측정 ID 설정
- **파일**: `themes/hueman/_config.yml` (98번째 줄, 129번째 줄)
- **변경**: `google_analytics: UA-166318275-1` -> `google_analytics: G-XXXXXXXXXX` (2곳)
  - 98번째 줄: `plugins.google_analytics`
  - 129번째 줄: 루트 레벨 `google_analytics`
- **목적**: GA4 측정 ID 적용
- **사용자 액션**: Google Analytics 콘솔에서 GA4 속성 생성 후 측정 ID(G-로 시작) 발급 필요

---

### 단계 3: SEO 강화

#### 3-1. Open Graph / Twitter Card 메타태그 확인 및 보완
- **파일**: `themes/hueman/layout/common/head.ejs` (35~40번째 줄)
- **현재 상태**: Hexo 내장 `open_graph()` 헬퍼 사용 중 (정상 동작). `fb_app_id`, `fb_admins`, `twitter_id`는 비어 있음
- **변경 내용**:
  - `open_graph()` 호출에 `twitter_card: 'summary_large_image'` 옵션 추가
  - `description: page.description || page.excerpt || config.description` 명시적 전달
  - `themes/hueman/_config.yml`의 `miscellaneous.open_graph` 섹션에 `twitter_id` 값 설정 (트위터 계정이 있는 경우)
- **목적**: SNS 공유 시 미리보기 이미지와 설명이 올바르게 표시되도록 함

#### 3-2. meta description 자동 생성 확인
- **파일**: `themes/hueman/layout/common/head.ejs`
- **현재 상태**: `open_graph()` 헬퍼가 description을 자동 생성함 (포스트 excerpt 또는 앞부분 200자 사용)
- **변경 내용**: 별도 description 메타태그를 명시적으로 추가
```html
<meta name="description" content="<%= strip_tags(page.description || page.excerpt || config.description).substring(0, 160) %>" />
```
- **위치**: head.ejs의 keywords 메타태그 아래에 삽입
- **목적**: 검색 엔진 결과에 포스트 요약이 올바르게 표시

#### 3-3. sitemap 설정 최적화
- **파일**: `_config.yml` (146~149번째 줄)
- **현재 상태**: `hexo-generator-seo-friendly-sitemap` 0.0.25 설치됨, 기본 설정 사용
- **변경 내용**: changefreq, priority 등 세부 설정 추가
```yaml
sitemap:
  path: sitemap.xml
  tag: true
  category: true
```
- **추가 확인**: `robots.txt`에 sitemap URL이 이미 설정되어 있음 (정상)
- **목적**: 카테고리/태그 페이지도 sitemap에 포함하여 크롤링 범위 확대

---

### 단계 4: 댓글 시스템 활성화 (Giscus)

#### 4-1. 댓글 시스템 전환: Disqus -> Giscus
- **현재 상태**: `themes/hueman/_config.yml`에 `disqus: hexo-theme-hueman`으로 설정되어 있으나, 기본 테마 샘플 값이며 실제 동작하지 않음
- **변경 방향**: Disqus 비활성화 후 Giscus(GitHub Discussions 기반) 추가

#### 4-2. Giscus 스크립트 삽입
- **새 파일 생성**: `themes/hueman/layout/comment/giscus.ejs`
```html
<div class="giscus-container">
  <script src="https://giscus.app/client.js"
    data-repo="hgko1207/hgko1207.github.io"
    data-repo-id="[REPO_ID]"
    data-category="Announcements"
    data-category-id="[CATEGORY_ID]"
    data-mapping="pathname"
    data-strict="0"
    data-reactions-enabled="1"
    data-emit-metadata="0"
    data-input-position="bottom"
    data-theme="light"
    data-lang="ko"
    crossorigin="anonymous"
    async>
  </script>
</div>
```

#### 4-3. comment/index.ejs에 Giscus 분기 추가
- **파일**: `themes/hueman/layout/comment/index.ejs`
- **변경**: gitalk 분기 아래에 giscus 조건 추가
```ejs
<% } else if (theme.comment.giscus && theme.comment.giscus.on) { %>
    <%- partial('comment/giscus') %>
```

#### 4-4. 테마 설정에 Giscus 옵션 추가
- **파일**: `themes/hueman/_config.yml` (comment 섹션)
- **변경**:
  - `disqus:` 값 제거 (주석 처리)
  - giscus 설정 블록 추가:
```yaml
    giscus:
        on: true
        repo: hgko1207/hgko1207.github.io
        repo_id: # https://giscus.app 에서 발급
        category: Announcements
        category_id: # https://giscus.app 에서 발급
```
- **사용자 액션**: https://giscus.app 에서 repo 연결 후 repo_id, category_id 값 확인 필요. GitHub 리포지토리에서 Discussions 기능 활성화 필요

---

### 단계 5: 수익화 개선

#### 5-1. AdSense 광고 배치 최적화
- **현재 상태**:
  - `head.ejs`: AdSense 스크립트 로드 (ca-pub-7581566810202853)
  - `ads/google_ad.ejs`: 본문 내 자동 삽입 광고 (슬롯 5075244775) -- article.ejs에서 호출
  - `widget/google_adsense.ejs`: 사이드바 위젯 -- 위젯 목록에 포함되어 있으나 `publisher_id`가 비어 있어 기본 링크 표시됨
- **변경 내용**:
  - `themes/hueman/_config.yml`의 `google_adsense` 설정에 실제 값 입력:
    ```yaml
    google_adsense:
      publisher_id: pub-7581566810202853
      ad_slot: [사이드바용 광고 슬롯 ID]
    ```
  - 또는 `widget/google_adsense.ejs`를 직접 수정하여 하드코딩된 AdSense 코드 삽입
- **목적**: 사이드바 광고 슬롯 활성화로 수익 증대

#### 5-2. 쿠팡 파트너스 배너 영역 활성화
- **현재 상태**: `ads/coupang_ad.ejs` 파일 존재 (trackingCode: AF1935979), 하지만 `article.ejs`에서 주석 처리됨 (`<!-- <%- partial('ads/coupang_ad') %> -->`)
- **변경 내용**:
  - `themes/hueman/layout/common/article.ejs` 24번째 줄의 주석 해제:
    - `<!-- <%- partial('ads/coupang_ad') %> -->` -> `<%- partial('ads/coupang_ad') %>`
  - 또는 별도 위젯으로 사이드바에 배치: `themes/hueman/layout/widget/` 디렉토리에 `coupang.ejs` 위젯 생성 후 `_config.yml` widgets 목록에 추가
- **목적**: 쿠팡 파트너스 제휴 수익 활성화
- **주의**: 광고가 과도하면 UX 저하 및 AdSense 정책 위반 가능. 본문 내 또는 사이드바 중 하나만 선택 권장

---

### 단계 6: 배포 및 확인

#### 6-1. 빌드 확인
- **명령어**: `hexo clean && hexo generate`
- **확인 사항**:
  - 빌드 에러 없는지 확인
  - `hexo-wordcount` 플러그인 설치 확인 (단계 1-2)
  - GA4 스크립트가 생성된 HTML에 포함되는지 확인
  - 로컬 서버로 미리보기: `hexo server`

#### 6-2. 변경사항 커밋 및 배포
- **명령어**:
```bash
git add -A
git commit -m "블로그 개선: GA4 전환, 한국어 설정, SEO 강화, Giscus 댓글, 광고 최적화"
hexo deploy
```
- **배포 후 확인**:
  - https://hgko1207.github.io/ 접속하여 변경사항 반영 확인
  - Google Analytics 실시간 보고서에서 데이터 수집 확인
  - 댓글 시스템 동작 확인
  - Google Search Console에서 sitemap 재제출

---

## 참고: 주요 파일 경로 요약

| 구분 | 파일 경로 |
|------|----------|
| 메인 설정 | `_config.yml` |
| 테마 설정 | `themes/hueman/_config.yml` |
| GA 스크립트 | `themes/hueman/layout/plugin/google-analytics.ejs` |
| HTML head | `themes/hueman/layout/common/head.ejs` |
| 글 본문 레이아웃 | `themes/hueman/layout/common/article.ejs` |
| 댓글 분기 | `themes/hueman/layout/comment/index.ejs` |
| 워드카운트 | `themes/hueman/layout/common/post/counter.ejs` |
| 본문 광고 | `themes/hueman/layout/ads/google_ad.ejs` |
| 사이드바 광고 | `themes/hueman/layout/widget/google_adsense.ejs` |
| 쿠팡 광고 | `themes/hueman/layout/ads/coupang_ad.ejs` |
| 한국어 언어 | `themes/hueman/languages/ko.yml` |
| 패키지 설정 | `package.json` |