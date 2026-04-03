---
title: gstack 디자인 가이드
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
date: 2026-04-03 00:14:06
thumbnail: /images/thumbnail/claude.png
---

> `/design-consultation`, `/design-review`, `/plan-design-review`

---

## /design-consultation — 디자인 시스템 구축

### 무엇을 하는가

제품을 분석하고, 유사 제품을 리서치한 후, **완전한 디자인 시스템을 제안**합니다.
결과물로 `DESIGN.md`를 생성해서 프로젝트의 디자인 소스 오브 트루스로 사용합니다.

### 산출물

- 전체 디자인 시스템 제안
  - 미적 방향 (aesthetic direction)
  - 타이포그래피 시스템
  - 컬러 팔레트
  - 레이아웃 & 스페이싱 규칙
  - 모션 원칙
- 폰트 + 컬러 프리뷰 페이지 (HTML 파일)
- `DESIGN.md` — 디자인 결정사항 문서

### 사용법

```
/design-consultation
```

Claude가 제품의 성격, 타겟 유저, 브랜드 방향을 먼저 물어봅니다.

또는 먼저 설명합니다:

```
/design-consultation 개발자를 위한 SaaS 대시보드야. 신뢰감 있고 깔끔한 느낌.
```

### 꿀팁

- 경쟁 제품이나 레퍼런스 디자인을 함께 언급하면 방향 잡기 쉽습니다
- 생성된 `DESIGN.md`를 `CLAUDE.md`에서 `@DESIGN.md`로 참조하면 이후 UI 작업에 자동 적용됩니다
- `/browse`로 레퍼런스 사이트를 함께 열어두면 더 정확한 결과를 얻을 수 있습니다

---

## /design-review — 라이브 사이트 디자인 감사

### 무엇을 하는가

**실행 중인 웹사이트를 헤드리스 브라우저로 열어서** 시각적 문제를 발견하고 코드를 직접 수정합니다.

발견 → 수정 → 재검증을 반복하며 각 수정을 원자적으로 커밋합니다.

### 발견하는 문제

- 시각적 불일관성 (색상, 폰트, 간격이 제멋대로인 경우)
- 스페이싱 문제 (padding/margin 불균형)
- 계층 구조 문제 (시각적 강조가 잘못된 곳에 있는 경우)
- AI slop 패턴 (AI가 생성한 것처럼 보이는 어색한 UI)
- 느린 인터랙션 (버튼 반응, 전환 애니메이션)

### 사용법

```
/design-review
```

개발 서버가 실행 중이어야 합니다. URL을 자동으로 감지하거나 직접 지정할 수 있습니다:

```
/design-review http://localhost:3000
```

### 사전 준비

1. 개발 서버 실행: `pnpm dev` (또는 `npm run dev`)
2. `/design-review` 실행
3. Claude가 스크린샷 찍고 문제 목록 제시
4. 각 수정 전후 스크린샷으로 비교

### 꿀팁

- 수정 전후 스크린샷이 자동으로 저장됩니다 → diff로 비교 가능합니다
- "이 페이지만 봐줘"처럼 범위 지정이 가능합니다: `/design-review http://localhost:3000/dashboard`
- 인증이 필요한 페이지는 먼저 `/setup-browser-cookies`로 쿠키를 세팅합니다
- `/plan-design-review`(플랜 검토)와 `/design-review`(라이브 감사)는 다른 명령어입니다

---

## /plan-design-review — 플랜 단계 디자인 검토

### 무엇을 하는가

작성된 플랜에서 **디자인 관련 항목을 0~10점으로 채점**하고, 10점이 되려면 뭐가 필요한지 설명한 후 플랜을 업데이트합니다.

### 사용법

```
/plan-design-review
```

plan.md가 있으면 자동으로 읽습니다.

### 차이점 정리

| 명령어                 | 대상             | 출력                 |
| ---------------------- | ---------------- | -------------------- |
| `/plan-design-review`  | 플랜 문서        | 플랜 수정            |
| `/design-review`       | 라이브 사이트    | 코드 수정 + 스크린샷 |
| `/design-consultation` | 없음 (처음 시작) | DESIGN.md 생성       |

---

## 디자인 워크플로우 예시

### 새 프로젝트 디자인 시스템 구축

```
1. /design-consultation    → DESIGN.md 생성
2. CLAUDE.md에 @DESIGN.md 추가
3. 개발
4. /design-review          → 구현된 UI 감사 + 수정
```

### 기존 프로젝트 디자인 개선

```
1. /design-review          → 현재 문제 파악 + 자동 수정
2. /design-consultation    → 더 나은 디자인 시스템 정립
3. DESIGN.md을 기준으로 정비
```

### 새 기능 추가 시

```
1. /plan-design-review     → 플랜 단계에서 UX 방향 확인
2. 구현
3. /design-review          → 구현 결과 시각적 검증
```

---

## DESIGN.md 활용법

`/design-consultation`으로 생성한 `DESIGN.md`를 `CLAUDE.md`에 연결합니다:

```markdown
## 디자인 시스템

@DESIGN.md 참고. 모든 UI 작업은 이 문서의 컬러, 타이포그래피, 스페이싱 규칙을 따를 것.
```

이후 Claude가 UI 코드를 작성할 때 자동으로 디자인 시스템을 참조합니다.
