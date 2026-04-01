---
title: gstack 개발 & 코드 품질 가이드
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
date: 2026-04-01 22:26:23
thumbnail: /images/thumbnail/claude.png
---

# gstack 개발 & 코드 품질 가이드

> `/review`, `/investigate`, `/codex`, `/simplify`, `/careful`, `/freeze`, `/guard`, `/unfreeze`

---

## /review — PR 코드 리뷰

### 무엇을 하는가

현재 브랜치와 base 브랜치의 diff를 분석해서 코드 리뷰를 수행합니다.
일반적인 코드 품질 외에 **구조적 위험**에 집중합니다.

### 검토 항목

| 항목                 | 설명                                       |
| -------------------- | ------------------------------------------ |
| SQL 안전성           | SQL 인젝션, N+1 쿼리, 인덱스 누락          |
| LLM 신뢰 경계        | AI 출력을 직접 실행하거나 신뢰하는 코드    |
| 조건부 사이드 이펙트 | 조건에 따라 의도치 않은 동작이 생기는 코드 |
| 타입 안전성          | TypeScript any, unsafe cast                |
| 인증/인가            | 누락된 권한 체크                           |
| 보안                 | 시크릿 노출, 취약한 의존성                 |

### 사용법

```
/review
```

현재 git diff를 자동으로 읽습니다. PR 번호나 브랜치를 지정할 수도 있습니다:

```
/review feature/auth-refactor
```

### 꿀팁

- `/ship` 전에 반드시 실행합니다 — 배포 전 마지막 안전망입니다
- "SQL 부분만 집중해서 봐줘"처럼 범위 지정이 가능합니다
- 수정까지 원하면 "수정도 해줘" 추가 요청을 합니다

---

## /investigate — 체계적 디버깅

### 무엇을 하는가

**4단계 체계적 디버깅**을 수행합니다.
핵심 원칙: **원인을 파악하기 전에 절대 수정하지 않습니다.**

### 4단계

1. **Investigate** — 현상 파악, 로그/에러 수집, 재현 경로 확인
2. **Analyze** — 코드 추적, 스택 트레이스 분석, 관련 코드 읽기
3. **Hypothesize** — 가능한 원인 가설 나열, 가장 가능성 높은 것 선택
4. **Implement** — 최소한의 수정으로 근본 원인 해결

### 사용법

```
/investigate
```

이후 Claude가 어떤 버그/오류인지 물어봅니다. 또는 바로 설명합니다:

```
/investigate 로그인 후 대시보드 리다이렉트가 안 돼. 에러: undefined is not iterable
```

### 꿀팁

- 에러 메시지, 스택 트레이스, 재현 방법을 같이 제공하면 훨씬 빠릅니다
- "증상만 숨기는 workaround 하지 마"라고 명시하면 근본 원인 수정에 집중합니다
- 복잡한 버그는 `/investigate` → 원인 파악 → 직접 수정 or Claude 수정 선택이 가능합니다

---

## /codex — OpenAI Codex 추가 검토

### 무엇을 하는가

OpenAI Codex CLI를 사용해서 **3가지 모드**로 추가 관점을 제공합니다.
Claude의 결과를 독립적으로 검증하거나, 다른 시각으로 코드를 테스트하는 데 유용합니다.

### 3가지 모드

| 모드            | 설명                                           | 사용 시점       |
| --------------- | ---------------------------------------------- | --------------- |
| **Code Review** | Codex가 독립적으로 diff를 리뷰, pass/fail 판정 | PR 전 이중 검토 |
| **Challenge**   | 적대적 모드 — 내 코드를 부수려 시도            | 견고성 테스트   |
| **Consult**     | Codex에게 질문 (세션 연속성 있음)              | 두 번째 의견    |

### 사용법

```
/codex          # 모드 선택 메뉴
/codex review   # 바로 리뷰 모드
/codex challenge  # 바로 도전 모드
```

### 필요 조건

- OpenAI API 키 필요 (`OPENAI_API_KEY` 환경 변수)
- `codex` CLI 설치: `npm install -g @openai/codex`

### 꿀팁

- Challenge 모드: "내 코드가 얼마나 견고한가?" 확인에 특히 유용합니다
- Claude + Codex 두 개가 동의하면 상당히 안전한 코드입니다
- 의견이 다를 때가 제일 흥미롭고 배울 점이 많습니다

---

## /simplify — 코드 단순화

### 무엇을 하는가

최근 변경된 코드를 검토하여 **재사용성, 품질, 효율성** 문제를 발견하고 수정합니다.

### 검토 항목

- 중복 코드 (DRY 원칙)
- 불필요한 복잡도
- 더 나은 추상화 기회
- 성능 개선 여지
- 명명 개선

### 사용법

```
/simplify              # 최근 변경 파일 자동 검토
/simplify src/auth/    # 특정 경로 지정
```

### 꿀팁

- 기능 구현 완료 후 배포 전에 한 번 실행하면 좋습니다
- 너무 큰 리팩토링은 원하지 않으면 "사소한 것만" 명시합니다
- `/review` (구조적 문제) + `/simplify` (코드 품질) 조합이 이상적입니다

---

## /careful — 위험 명령어 경고

### 무엇을 하는가

Claude가 위험한 명령어를 실행하기 전에 **경고를 표시**하고 사용자 확인을 요청합니다.

### 차단하는 명령어

```
rm -rf          # 대량 삭제
DROP TABLE      # DB 테이블 삭제
git push --force  # 강제 푸시
git reset --hard  # 로컬 변경 전체 롤백
kubectl delete  # 쿠버네티스 리소스 삭제
```

### 사용법

```
/careful
```

이후 세션 전체에 적용됩니다. 각 위험 명령어마다 확인을 요청합니다.

### 꿀팁

- 프로덕션 디버깅 시 항상 먼저 실행합니다
- 각 경고에서 재정의가 가능합니다 → 알고 하는 것과 실수로 하는 것을 구분합니다
- `/guard` = `/careful` + `/freeze` 조합 (더 강력합니다)

---

## /freeze — 편집 범위 제한

### 무엇을 하는가

세션 동안 **지정한 디렉터리 외 파일 편집을 차단**합니다.
Edit, Write 도구가 해당 경로 밖 파일에 접근하면 차단됩니다.

### 사용법

```
/freeze src/auth/       # auth 폴더만 편집 허용
/freeze src/components/ # components 폴더만 편집 허용
```

### 사용 시점

- 버그 디버깅 시 관계없는 코드를 "수정"하는 것 방지
- 특정 모듈만 리팩토링할 때 범위 이탈 방지
- 새 팀원이 코드를 탐색할 때 안전망

### 꿀팁

```
/unfreeze    # freeze 해제
```

- `/freeze`와 `/careful`을 조합하려면 `/guard`를 사용합니다

---

## /guard — 최강 안전 모드

### 무엇을 하는가

`/careful` (위험 명령어 경고) + `/freeze` (디렉터리 편집 제한)를 **동시에 활성화**합니다.

### 사용법

```
/guard src/api/    # src/api/ 외 편집 차단 + 위험 명령어 경고
```

### 사용 시점

- 프로덕션 서버에서 작업할 때
- 공유 인프라 디버깅 시
- 실수 한 번이 크리티컬할 때

---

## 개발 워크플로우 예시

### 일반 개발 사이클

```
구현 완료
  → /simplify    (코드 품질 정리)
  → /review      (구조적 문제 확인)
  → /ship        (PR 생성)
```

### 버그 수정

```
버그 발견
  → /careful                      (안전 모드 켜기)
  → /freeze src/관련모듈/          (범위 제한)
  → /investigate 버그 설명          (체계적 분석)
  → 수정
  → /review                        (변경사항 검토)
  → /ship
```

### 복잡한 코드 신뢰성 검증

```
구현 완료
  → /review          (Claude 리뷰)
  → /codex challenge  (Codex가 부수려 시도)
  → 발견된 문제 수정
  → /ship
```

---

**출처**: [gstack GitHub](https://github.com/garrytan/gstack) — Garry Tan (Y Combinator CEO)
