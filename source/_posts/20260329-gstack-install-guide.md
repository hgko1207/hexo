---
title: gstack 설치 가이드 (Windows) — Claude Code를 가상 엔지니어링 팀으로 만들기
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
date: 2026-03-29 00:38:16
thumbnail: /images/thumbnail/Claude.png
---

> Garry Tan (Y Combinator CEO)이 공개한 오픈소스 Claude Code 스킬 모음입니다.
> 60일 만에 60만 줄 프로덕션 코드를 혼자 작성한 그의 워크플로우를 그대로 쓸 수 있습니다.

---

## gstack이 뭔가요?

[gstack](https://github.com/garrytan/gstack)은 Claude Code를 **가상 엔지니어링 팀**으로 만들어주는 슬래시 커맨드 모음입니다.

| 역할          | 커맨드                                  |
| ------------- | --------------------------------------- |
| 기획/전략     | `/office-hours`, `/plan-ceo-review`     |
| 아키텍처 설계 | `/plan-eng-review`                      |
| 디자인 리뷰   | `/plan-design-review`, `/design-review` |
| 코드 리뷰     | `/review`                               |
| QA 테스트     | `/qa`, `/qa-only`                       |
| 배포          | `/ship`, `/land-and-deploy`             |
| 보안 감사     | `/cso`                                  |
| 디버깅        | `/investigate`                          |
| 성능 측정     | `/benchmark`                            |
| 회고          | `/retro`                                |

총 28개 스킬이 포함되어 있으며, 헤드리스 브라우저(`/browse`)로 실제 UI를 열어서 QA까지 자동으로 수행합니다.

---

## 설치 전 필요한 것

| 도구                                      | 설명                             | 확인 명령          |
| ----------------------------------------- | -------------------------------- | ------------------ |
| [Claude Code](https://claude.ai/download) | Anthropic 공식 CLI               | `claude --version` |
| [Git](https://git-scm.com/)               | 소스 클론                        | `git --version`    |
| [Node.js](https://nodejs.org/)            | Windows 필수 (Playwright 실행용) | `node --version`   |
| [Bun](https://bun.sh/)                    | 빌드 도구 (아래 설치법 참고)     | `bun --version`    |

---

## 1단계 — Bun 설치 (Windows)

Bun은 gstack 빌드에 필수입니다. PowerShell을 열고 아래 명령을 실행하세요.

```powershell
powershell -c "irm bun.sh/install.ps1 | iex"
```

설치 완료 후 **터미널을 재시작**해야 PATH가 적용됩니다.

설치 확인:

```bash
bun --version
# 1.3.11
```

---

## 2단계 — gstack 전역 설치

Claude Code 터미널(또는 Git Bash)에서 실행합니다.

```bash
git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup
```

설치가 완료되면 아래처럼 출력됩니다:

```
gstack ready (claude).
  browse: /c/Users/{username}/.claude/skills/gstack/browse/dist/browse.exe
```

---

## 트러블슈팅 — Windows에서 setup 실패하는 경우

### 증상

```
gstack setup failed: browse binary missing at .../browse/dist/browse
```

### 원인

bun이 Windows에서 바이너리를 컴파일할 때 `browse.exe`로 생성하는데,
setup 스크립트가 확장자 없는 `browse`만 체크해서 실패합니다.
실제 파일은 정상적으로 빌드되어 있지만 인식을 못하는 것입니다.

### 해결 방법

`~/.claude/skills/gstack/setup` 파일을 열고 아래 코드를 추가합니다.

**수정 전 (line 18~21 부근):**

```bash
IS_WINDOWS=0
case "$(uname -s)" in
  MINGW*|MSYS*|CYGWIN*|Windows_NT) IS_WINDOWS=1 ;;
esac
```

**수정 후:**

```bash
IS_WINDOWS=0
case "$(uname -s)" in
  MINGW*|MSYS*|CYGWIN*|Windows_NT) IS_WINDOWS=1 ;;
esac

if [ "$IS_WINDOWS" -eq 1 ] && [ -f "${BROWSE_BIN}.exe" ]; then
  BROWSE_BIN="${BROWSE_BIN}.exe"
fi
```

수정 후 다시 실행합니다:

```bash
cd ~/.claude/skills/gstack && ./setup
```

> **참고:** 이 문제는 gstack의 Windows 지원 버그입니다. 추후 업스트림에서 수정될 수 있습니다.

---

## 3단계 — 프로젝트에 추가 (팀원 공유용)

전역 설치만 하면 본인 PC에서만 동작합니다.
팀원들과 함께 쓰려면 프로젝트 레포에도 추가해야 합니다.

```bash
mkdir -p .claude/skills
cp -Rf ~/.claude/skills/gstack .claude/skills/gstack
rm -rf .claude/skills/gstack/.git
cd .claude/skills/gstack && ./setup
```

그런 다음 프로젝트 루트에 `CLAUDE.md`를 만들거나 기존 파일에 아래 내용을 추가합니다:

```markdown
## gstack

Use the `/browse` skill from gstack for all web browsing. Never use `mcp__claude-in-chrome__*` tools.

If gstack skills aren't working, run `cd .claude/skills/gstack && ./setup` to build the binary and register skills.

### Available skills

/office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation,
/review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /qa, /qa-only, /design-review,
/setup-browser-cookies, /setup-deploy, /retro, /investigate, /document-release, /codex, /cso,
/autoplan, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade
```

팀원은 `git clone` 이후 아래 한 줄만 실행하면 됩니다:

```bash
cd .claude/skills/gstack && ./setup
```

---

## 설치 완료 후 사용법

Claude Code에서 바로 슬래시 커맨드를 입력하면 됩니다.

```
/office-hours       → 프로젝트 기획 브레인스토밍
/plan-ceo-review    → 기능 아이디어 전략 검토
/plan-eng-review    → 아키텍처 설계 리뷰
/review             → 현재 브랜치 코드 리뷰
/qa                 → 웹앱 QA 자동화 (버그 발견 + 수정)
/ship               → PR 생성 및 배포 워크플로우
/retro              → 주간 커밋 회고
/investigate        → 버그 원인 분석
/cso                → 보안 감사
```

---

## 정리

| 단계 | 내용                                    |
| ---- | --------------------------------------- |
| 1    | PowerShell에서 Bun 설치                 |
| 2    | `git clone` + `./setup` 으로 전역 설치  |
| 3    | Windows 버그 패치 (`.exe` 인식 문제)    |
| 4    | 프로젝트 레포에 복사 + `CLAUDE.md` 등록 |

전체 과정을 마치면 Claude Code 어디서든 28개의 gstack 슬래시 커맨드를 바로 쓸 수 있습니다.

---

_설치 환경: Windows 11, Node.js v24, Bun 1.3.11, Claude Code_
