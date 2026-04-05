---
title: gstack QA & 배포 가이드
categories:
  - Programming
  - AI
  - CLAUDE
tags:
  - Programming
  - AI
  - claude
  - claude code
  - ai개발도구
  - gstack
  - AI코딩
  - 클로드코드
  - 개발
date: 2026-04-03 21:21:48
thumbnail: /images/thumbnail/claude.png
---

> `/browse`, `/qa`, `/qa-only`, `/benchmark`, `/setup-browser-cookies`
> `/setup-deploy`, `/ship`, `/land-and-deploy`, `/canary`, `/document-release`

---

## Part 1: QA & 브라우저 테스트

### /browse — 헤드리스 브라우저

#### 무엇을 하는가

Playwright 기반의 빠른 헤드리스 브라우저로 사이트를 직접 열어서 테스트합니다.
gstack의 대부분 시각적 명령어(`/qa`, `/design-review`, `/canary`, `/benchmark`)가 내부적으로 이것을 사용합니다.

#### 할 수 있는 것

- 특정 URL 열기 및 스크린샷
- 요소 클릭, 폼 입력, 스크롤
- 페이지 상태 검증 (요소 존재 여부, 텍스트 확인)
- 액션 전후 diff (변경된 것 비교)
- 반응형 레이아웃 테스트 (모바일/태블릿/데스크탑)
- 다이얼로그 처리
- 버그 증거 스크린샷 저장

#### 사용법

```
/browse
```

Claude가 무엇을 할지 물어봅니다. 또는 바로 지시합니다:

```
/browse http://localhost:3000/login 열고 로그인 폼 테스트해줘
```

#### 꿀팁

- 직접 `/browse`를 쓰기보다 `/qa`, `/design-review` 같은 상위 명령어를 주로 사용합니다
- 특정 시나리오만 테스트할 때 `/browse`로 직접 지시하면 유용합니다
- 인증 필요 시 먼저 `/setup-browser-cookies`를 실행합니다

---

### /setup-browser-cookies — 로컬 쿠키 가져오기

#### 무엇을 하는가

로컬 크롬 브라우저의 쿠키를 헤드리스 세션으로 가져옵니다.
로그인이 필요한 페이지를 테스트할 때 필수입니다.

#### 사용법

```
/setup-browser-cookies
```

대화형 UI가 열리며 어떤 도메인의 쿠키를 가져올지 선택합니다.

#### 순서

```
1. 크롬에서 직접 로그인
2. /setup-browser-cookies 실행
3. 도메인 선택 (예: localhost, 또는 실제 도메인)
4. 이후 /browse, /qa, /design-review 실행
```

---

### /qa — QA 테스트 + 자동 수정

#### 무엇을 하는가

웹 앱을 체계적으로 QA 테스트하고 발견된 버그를 **자동으로 수정**합니다.
각 수정을 원자적으로 커밋하고, 수정 후 재검증합니다.

#### 흐름

```
/qa 실행
  → 헤드리스 브라우저로 앱 탐색
  → 버그/문제 발견
  → 소스 코드 수정
  → 커밋 (버그별 별도 커밋)
  → 재검증 (수정됐는지 확인)
  → 다음 버그로
```

#### 사용법

```
/qa                              # 전체 앱 QA
/qa http://localhost:3000/auth   # 특정 페이지만
```

개발 서버가 실행 중이어야 합니다.

#### 꿀팁

- 수정을 원하지 않으면 `/qa-only`를 사용합니다
- 인증 필요 페이지는 `/setup-browser-cookies`를 먼저 실행합니다
- "결제 플로우만 테스트해줘"처럼 범위 지정이 가능합니다
- 발견된 버그가 많으면 우선순위를 물어봐도 됩니다

---

### /qa-only — QA 리포트만 (수정 없음)

#### 무엇을 하는가

`/qa`와 동일하게 테스트하지만 **코드 수정은 절대 하지 않습니다**.
버그 목록, 헬스 스코어, 스크린샷, 재현 방법이 포함된 구조화된 리포트를 생성합니다.

#### 사용법

```
/qa-only                          # 리포트만
/qa-only http://localhost:3000    # 특정 URL
```

#### 언제 쓰는가

- 현재 상태 파악만 필요할 때
- 수동으로 수정하고 싶을 때
- 팀에게 공유할 QA 리포트가 필요할 때
- 중요한 코드라 자동 수정이 불안할 때

---

### /benchmark — 성능 측정

#### 무엇을 하는가

페이지 로드 타임, Core Web Vitals, 리소스 크기를 측정하고 **회귀 감지**를 합니다.
기준선(baseline)을 수립하고, 이후 측정값과 비교해서 성능 저하를 감지합니다.

#### 측정 항목

| 지표             | 설명                                        |
| ---------------- | ------------------------------------------- |
| LCP              | Largest Contentful Paint (주요 콘텐츠 로드) |
| FCP              | First Contentful Paint (첫 콘텐츠 표시)     |
| CLS              | Cumulative Layout Shift (레이아웃 이동)     |
| TTI              | Time to Interactive (인터랙티브 가능 시점)  |
| 번들 크기        | JS/CSS 파일 크기                            |
| 네트워크 요청 수 | 불필요한 요청 감지                          |

#### 사용법

```
/benchmark                        # 현재 상태 기준선 측정
/benchmark http://localhost:3000  # 특정 URL
```

---

## Part 2: 배포 워크플로우

### 배포 전 한 번만: /setup-deploy 설정

```
/setup-deploy
```

배포 플랫폼(Vercel, Netlify, Fly.io, Render, Heroku, GitHub Actions 등)을 자동 감지하고:

- 프로덕션 URL
- 헬스체크 엔드포인트
- 배포 상태 확인 명령어

를 CLAUDE.md에 저장합니다. `/land-and-deploy`와 `/canary`가 이 정보를 사용합니다.

---

### /ship — PR 생성 (배포 전 단계)

#### 무엇을 하는가

PR을 만들기 위한 전체 준비를 자동화합니다.

#### 실행 순서

```
1. base 브랜치 감지 및 최신화
2. 테스트 실행
3. diff 리뷰
4. VERSION 업데이트 (있으면)
5. CHANGELOG 업데이트
6. 커밋 & 푸시
7. PR 생성
```

#### 사용법

```
/ship
```

#### 꿀팁

- "테스트 건너뛰어도 돼"처럼 특정 단계 생략 요청이 가능합니다
- CHANGELOG가 없는 프로젝트는 자동으로 생성됩니다
- `/review` 후 `/ship`이 이상적인 순서입니다

---

### /land-and-deploy — PR 머지 + 배포 + 검증

#### 무엇을 하는가

`/ship`으로 만든 PR을 머지하고, CI/CD 완료를 기다리고, 프로덕션 헬스체크까지 합니다.

#### 실행 순서

```
1. PR 머지
2. CI/CD 파이프라인 대기
3. 배포 완료 대기
4. 프로덕션 헬스체크
5. /canary로 라이브 모니터링
```

#### 사용법

```
/land-and-deploy
```

`/setup-deploy`로 배포 설정이 되어 있어야 합니다.

#### 꿀팁

- 단독으로도 쓸 수 있지만 `/ship` → `/land-and-deploy` 순서가 표준입니다
- CI가 느리면 기다리는 동안 다른 작업이 가능합니다 (백그라운드 대기)

---

### /canary — 배포 후 모니터링

#### 무엇을 하는가

배포 후 **라이브 앱을 지속적으로 모니터링**합니다.

- 콘솔 에러 감지
- 성능 회귀 감지
- 페이지 실패 감지
- 주기적 스크린샷 + 배포 전 기준선과 비교

#### 사용법

```
/canary                           # 모니터링 시작
/canary http://my-app.vercel.app  # 특정 URL
```

---

### /document-release — 배포 후 문서 업데이트

#### 무엇을 하는가

배포 후 프로젝트 문서를 실제 출시된 내용과 동기화합니다.

#### 업데이트 대상

- README — 새 기능, 변경된 설정
- ARCHITECTURE.md — 아키텍처 변경사항
- CONTRIBUTING.md — 프로세스 변경
- CLAUDE.md — 새로운 작업 방식
- CHANGELOG — 배포 항목 문체 다듬기
- TODO 정리 — 완료된 항목 제거
- VERSION 업데이트 (선택)

#### 사용법

```
/document-release
```

최근 diff를 읽고 모든 관련 문서를 자동으로 업데이트합니다.

---

## 전체 배포 워크플로우

### 표준 흐름

```
개발 완료
  → /review                  (코드 리뷰)
  → /qa                      (QA 테스트 + 수정)
  → /ship                    (PR 생성)
  → /land-and-deploy         (머지 + 배포 + 검증)
  → /canary                  (라이브 모니터링)
  → /document-release        (문서 업데이트)
```

### 빠른 배포 (작은 수정)

```
수정 완료
  → /ship
  → /land-and-deploy
```

### 신중한 배포 (중요 기능)

```
개발 완료
  → /benchmark               (성능 기준선 측정)
  → /qa                      (QA)
  → /review                  (코드 리뷰)
  → /codex review             (추가 검토)
  → /ship
  → /land-and-deploy
  → /canary                  (모니터링)
  → /benchmark               (배포 후 성능 비교)
  → /document-release
```

---

**출처**: [gstack GitHub](https://github.com/garrytan/gstack) — Garry Tan (Y Combinator CEO)
