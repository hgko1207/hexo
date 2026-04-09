---
title: Impeccable 설치 가이드 — Claude Code에서 프로급 디자인 스킬 세팅하기
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
  - impeccable
  - AI코딩
  - 클로드코드
  - 개발
  - 디자인
date: 2026-04-08 21:54:52
thumbnail: /images/thumbnail/claude.png
---

> Impeccable은 Claude Code에 **디자인 전문가 수준의 판단력**을 부여하는 스킬 팩입니다. 설치 한 번으로 타이포그래피, 색상, 레이아웃, 모션까지 체계적인 디자인 리뷰가 가능해집니다.

---

## 사전 준비

Impeccable을 설치하기 전에 다음 환경이 갖춰져 있어야 합니다.

| 항목            | 요구 사항                        |
| --------------- | -------------------------------- |
| **Claude Code** | 최신 버전 설치 및 인증 완료      |
| **Node.js**     | v18 이상 (npx 설치 방식 사용 시) |
| **Git**         | GitHub 복사 방식 사용 시 필요    |

Claude Code가 아직 설치되어 있지 않다면, [공식 문서](https://docs.anthropic.com/en/docs/claude-code)를 참고하여 먼저 설치합니다.

---

## 설치 방법

### 방법 1: 웹사이트에서 다운로드 (추천)

가장 간단한 방법입니다. 별도의 CLI 도구 없이 바로 설치할 수 있습니다.

1. [impeccable.style](https://impeccable.style) 웹사이트에 접속합니다.
2. **Download** 버튼을 클릭하여 ZIP 파일을 다운로드합니다.
3. 다운로드한 ZIP 파일을 프로젝트 루트 디렉토리에 압축 해제합니다.
4. `.claude/skills/` 폴더가 프로젝트 루트에 생성되었는지 확인합니다.

```
your-project/
├── .claude/
│   └── skills/
│       ├── frontend-design/
│       ├── audit/
│       ├── critique/
│       └── ...
├── src/
└── package.json
```

### 방법 2: GitHub에서 직접 복사

Git이 설치되어 있다면 리포지토리에서 직접 복사할 수 있습니다.

```bash
# 프로젝트별 설치
git clone https://github.com/pbakaus/impeccable.git /tmp/impeccable
cp -r /tmp/impeccable/dist/claude-code/.claude your-project/

# 전역 설치 (모든 프로젝트에 적용)
cp -r /tmp/impeccable/dist/claude-code/.claude/* ~/.claude/
```

- **프로젝트별 설치**: 해당 프로젝트에서만 Impeccable 스킬이 활성화됩니다. 팀원과 함께 사용하려면 `.claude/` 폴더를 Git에 커밋하면 됩니다.
- **전역 설치**: 모든 프로젝트에서 Impeccable 스킬이 자동으로 적용됩니다. 개인 워크스테이션에서 사용할 때 편리합니다.

### 방법 3: npx로 설치

npx 인스톨러가 제공되는 경우, 한 줄 명령으로 설치할 수 있습니다.

```bash
npx impeccable-install
```

> **참고**: npx 설치 방식은 공식 지원 여부를 [impeccable.style](https://impeccable.style)에서 확인한 후 사용하시기 바랍니다.

---

## 설치 확인

설치가 완료되었다면, Claude Code에서 정상 동작 여부를 확인합니다.

```
> /audit
```

Claude Code 프롬프트에 `/audit`을 입력합니다. Impeccable이 정상적으로 설치되었다면, 현재 프로젝트의 프론트엔드 코드에 대한 디자인 감사(audit) 결과가 출력됩니다.

만약 명령어가 인식되지 않는다면 다음 사항을 점검합니다.

- `.claude/skills/` 디렉토리가 프로젝트 루트(또는 `~/.claude/skills/`)에 존재하는지 확인합니다.
- Claude Code를 재시작한 후 다시 시도합니다.
- 스킬 파일 내부에 `SKILL.md`가 포함되어 있는지 확인합니다.

---

## 초기 세팅: 프로젝트 디자인 컨텍스트 설정

Impeccable은 프로젝트의 디자인 원칙을 학습하여 더 정확한 피드백을 제공합니다. `/teach-impeccable` 명령어로 초기 세팅을 진행합니다.

```
> /teach-impeccable
```

실행하면 Claude Code가 다음과 같은 질문을 순서대로 물어봅니다.

- 프로젝트에서 사용하는 디자인 시스템 (예: Material Design, Tailwind 등)
- 주요 색상 팔레트 및 브랜드 컬러
- 타이포그래피 규칙 (폰트 패밀리, 스케일 등)
- 레이아웃 및 간격 체계
- 기타 디자인 원칙

답변이 완료되면 프로젝트 루트에 **`.impeccable.md`** 파일이 생성됩니다. 이 파일에 프로젝트의 디자인 컨텍스트가 저장되며, 이후 모든 Impeccable 명령어에서 이 컨텍스트를 참조합니다.

```
your-project/
├── .impeccable.md          ← 디자인 컨텍스트 파일 (자동 생성)
├── .claude/
│   └── skills/
└── ...
```

> **팁**: `.impeccable.md` 파일은 Git에 커밋하면 팀 전체가 동일한 디자인 기준을 공유할 수 있습니다.

---

## 설치 구조

Impeccable은 다음과 같은 디렉토리 구조로 설치됩니다. 각 스킬은 독립적인 폴더에 정리되어 있으며, 핵심 디자인 레퍼런스는 `frontend-design/reference/`에 위치합니다.

```
.claude/skills/
├── frontend-design/          # 핵심 디자인 스킬
│   ├── SKILL.md
│   └── reference/
│       ├── typography.md
│       ├── color-and-contrast.md
│       ├── spatial-design.md
│       ├── motion-design.md
│       ├── interaction-design.md
│       ├── responsive-design.md
│       └── ux-writing.md
├── audit/SKILL.md
├── critique/
│   ├── SKILL.md
│   └── reference/
├── normalize/SKILL.md
├── polish/SKILL.md
... (20개 명령어 스킬)
```

주요 스킬 설명은 다음과 같습니다.

| 스킬              | 설명                                                          |
| ----------------- | ------------------------------------------------------------- |
| `frontend-design` | 핵심 디자인 원칙 레퍼런스 (타이포그래피, 색상, 공간, 모션 등) |
| `audit`           | 디자인 품질 전체 감사                                         |
| `critique`        | 특정 컴포넌트에 대한 상세 디자인 비평                         |
| `normalize`       | 일관되지 않은 디자인 토큰 및 스타일 정규화                    |
| `polish`          | 전반적인 디자인 완성도 향상                                   |

---

## 다른 도구에서의 설치

Impeccable은 Claude Code 외에도 여러 AI 코딩 도구에서 사용할 수 있습니다.

| 도구            | 설치 경로                      | 비고                                    |
| --------------- | ------------------------------ | --------------------------------------- |
| **Claude Code** | `.claude/skills/`              | 프로젝트별 또는 전역(`~/.claude/`) 설치 |
| **Cursor**      | `.cursor/rules/`               | Cursor Rules로 설치                     |
| **Gemini CLI**  | `GEMINI.md` 또는 `.gemini/`    | Gemini 설정 방식에 따라 배치            |
| **Codex CLI**   | `AGENTS.md` 또는 프로젝트 설정 | Codex 에이전트 설정에 통합              |
| **Windsurf**    | `.windsurfrules`               | Windsurf 규칙 파일로 설치               |

각 도구별 상세 설치 방법은 [impeccable.style](https://impeccable.style)에서 확인할 수 있습니다. ZIP 다운로드 시 도구별 배포 파일이 함께 포함되어 있습니다.

---

**출처**: [impeccable.style](https://impeccable.style) | [GitHub — pbakaus/impeccable](https://github.com/pbakaus/impeccable)
