# Hexo 블로그

## 테마

- hueman

## Hexo 명령어

### 기본 명령어

```bash
# 새 포스트 생성
hexo new "포스트 제목"

# 새 페이지 생성
hexo new page "페이지 제목"

# 새 드래프트(초안) 생성
hexo new draft "드래프트 제목"

# 드래프트를 포스트로 발행
hexo publish "드래프트 제목"
```

### 서버 실행

```bash
# 로컬 서버 실행 (기본 포트: 4000)
hexo server
hexo s

# 포트 지정
hexo server -p 5000

# 드래프트 포함하여 미리보기
hexo server --draft
```

### 빌드 및 배포

```bash
# 정적 파일 생성
hexo generate
hexo g

# 파일 변경 감지하며 생성
hexo generate --watch
hexo g -w

# 배포
hexo deploy
hexo d

# 생성 + 배포 동시 실행
hexo generate --deploy
hexo g -d

# 캐시 및 생성된 파일 삭제
hexo clean

# clean 후 재생성 및 배포
hexo clean && hexo g -d
```

### npm 스크립트

```bash
npm run build      # hexo generate
npm run clean      # hexo clean
npm run deploy     # hexo deploy
npm run server     # hexo server
```

### 기타 명령어

```bash
# Hexo 버전 확인
hexo version

# 설정 목록 확인
hexo config

# 데이터베이스 목록 확인
hexo list
```

## Install

### Deploy

```bash
npm i hexo-deployer-git --save
```

### 검색엔진 최적화

```bash
npm i hexo-auto-canonical --save
npm i hexo-autonofollow --save
npm i hexo-generator-seo-friendly-sitemap --save
npm i hexo-generator-robotstxt --save
```

### Markdown

```bash
npm un hexo-renderer-marked --save
npm i hexo-renderer-markdown-it-plus --save
```

### Search

```bash
npm i hexo-generator-json-content --save
```
