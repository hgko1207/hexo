---
title: stack 실전 워크플로우
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
date: 2026-04-06 21:58:22
thumbnail: /images/thumbnail/claude.png
---

> 상황별 최적 명령어 조합 패턴입니다.

---

## 워크플로우 1: 새 기능 개발 (풀 사이클)

가장 완전한 흐름입니다. 아이디어부터 배포, 문서까지 포함합니다.

```
/office-hours                    → 기능이 진짜 필요한지 검증
  ↓
plan.md 작성                     → 구현 계획 문서화
  ↓
/autoplan                        → CEO + Eng + Design 리뷰 자동 실행
  ↓
구현                             → 코딩
  ↓
/simplify                        → 코드 품질 정리
  ↓
/review                          → PR 코드 리뷰
  ↓
/qa                              → QA 테스트 + 버그 수정
  ↓
/ship                            → PR 생성
  ↓
/land-and-deploy                 → 머지 + 배포 + 헬스체크
  ↓
/canary                          → 라이브 모니터링
  ↓
/document-release                → 문서 업데이트
```

---

## 워크플로우 2: 빠른 버그 수정

```
/careful                         → 안전 모드 켜기
  ↓
/investigate [버그 설명]          → 원인 분석
  ↓
수정
  ↓
/review                          → 변경사항 확인
  ↓
/ship → /land-and-deploy         → 배포
```

---

## 워크플로우 3: 새 프로젝트 UI 세팅

```
/design-consultation             → 디자인 시스템 수립 → DESIGN.md 생성
  ↓
CLAUDE.md에 @DESIGN.md 추가
  ↓
UI 개발
  ↓
/design-review                   → 라이브 시각적 감사 + 자동 수정
  ↓
/qa                              → 기능 QA
```

---

## 워크플로우 4: 주간 회고 + 다음 주 계획

```
매주 금요일:
/retro                           → 커밋 히스토리 분석, 팀 기여 회고
  ↓
/office-hours                    → 다음 주 작업 방향 검토
```

---

## 워크플로우 5: 보안 점검

```
/cso                             → 전체 보안 감사
  ↓
발견된 취약점 수정
  ↓
/review                          → 수정사항 검토
  ↓
/ship → /land-and-deploy
```

---

## 워크플로우 6: 성능 최적화

```
/benchmark                       → 현재 성능 기준선 측정
  ↓
성능 개선 작업
  ↓
/benchmark                       → 개선 후 비교
  ↓
/qa                              → 기능 회귀 없는지 확인
  ↓
/ship → /land-and-deploy
  ↓
/canary                          → 프로덕션 성능 모니터링
```

---

## 워크플로우 7: 안전한 리팩토링

```
/freeze src/리팩토링할경로/        → 범위 외 편집 차단
  ↓
/careful                         → 위험 명령어 경고 켜기
  ↓
리팩토링
  ↓
/unfreeze                        → freeze 해제
  ↓
/review                          → 리팩토링 검토
  ↓
/qa                              → 회귀 테스트
```

---

## 워크플로우 8: 독립 코드 검증

```
/review                          → Claude 리뷰
  ↓
/codex review                    → Codex 독립 리뷰
  ↓
(두 리뷰가 다른 점 확인 → 논쟁 포인트 집중)
  ↓
/codex challenge                 → 적대적 테스트
  ↓
수정
  ↓
/ship
```

---

## 상황별 빠른 선택 가이드

| 상황 | 명령어 |
|------|--------|
| 아이디어 검증 | `/office-hours` |
| 플랜 검토 (빠르게) | `/autoplan` |
| 플랜 검토 (깊게) | `/plan-ceo-review` → `/plan-eng-review` → `/plan-design-review` |
| 버그 찾기 | `/investigate` |
| 코드 리뷰 | `/review` |
| 코드 이중 검증 | `/review` + `/codex review` |
| UI 품질 개선 | `/design-review` |
| 새 디자인 시스템 | `/design-consultation` |
| QA (수정 포함) | `/qa` |
| QA (리포트만) | `/qa-only` |
| 성능 확인 | `/benchmark` |
| 배포 (PR 생성) | `/ship` |
| 배포 (풀 배포) | `/ship` → `/land-and-deploy` |
| 배포 후 모니터링 | `/canary` |
| 보안 감사 | `/cso` |
| 위험 작업 전 | `/careful` 또는 `/guard` |
| 주간 회고 | `/retro` |
| 문서 업데이트 | `/document-release` |
| gstack 업데이트 | `/gstack-upgrade` |

---

## 꿀팁 모음

### 1. 플래닝 먼저 / 코딩 나중에

```
/autoplan 또는 /plan-eng-review 없이 바로 코딩하면 나중에 구조 뜯어야 합니다.
5분 투자 → 나중에 몇 시간 절약됩니다.
```

### 2. /setup-deploy는 한 번만

```
프로젝트마다 한 번 실행하면 이후 /ship, /land-and-deploy, /canary가 자동으로 연결됩니다.
새 프로젝트 시작하면 바로 실행하는 습관을 들이세요.
```

### 3. /setup-browser-cookies 인증 설정

```
인증이 필요한 페이지가 있는 앱은 /qa, /design-review 전에 항상 실행합니다.
한 번 설정하면 세션 동안 유지됩니다.
```

### 4. /cso 정기 실행

```
큰 의존성 업데이트 후, 새 외부 API 연동 후, 배포 전 중요한 릴리즈 전에 실행합니다.
보안 문제는 나중에 발견할수록 비용이 커집니다.
```

### 5. /retro로 패턴 발견

```
매주 /retro 실행하면 어떤 버그가 반복되는지, 어디서 시간이 낭비되는지 패턴이 보입니다.
그 패턴을 CLAUDE.md에 기록하면 Claude가 반복 실수를 피할 수 있습니다.
```

### 6. /careful은 프로덕션 작업 기본값

```
프로덕션 DB, 라이브 서버, 공유 인프라 작업 시 항상 먼저 실행합니다.
실수 한 번이 서비스 다운으로 이어질 수 있을 때 사용합니다.
```

---
**출처**: [gstack GitHub](https://github.com/garrytan/gstack) — Garry Tan (Y Combinator CEO)
**태그**: #ClaudeCode #gstack #워크플로우 #실전패턴
