# Changelog

## [Step 3: 디자인/이미지(Page Bundles)/배포(GitHub Pages)] - 2026-07-05

**Project**: hugo_clojure | **Phase**: Step 3 완료 (push 대기)

### 결정 사항
- 디자인: **Ananke 유지 + 최소 튜닝** (배경색 등)
- 이미지: **Page Bundles** (글별 bundle, images/ 폴더)
- 배포: **GitHub Pages** (Hugo 공식 액션, baseURL `https://sa82trip.github.io/hugo_clojure/`)
- 글 단일화: hello.md 삭제, org 원본 → export 단일 파이프라인

### Added
- **Config** (`/`)
  - `hugo.toml` - baseURL/title=hello-clojure, `[languages.ko]` locale ko-KR, Ananke params(bg-black)
- **Deploy** (`.github/workflows/`)
  - `hugo.yml` - Hugo 공식 GitHub Pages 워크플로 (push to main, build+deploy job)
- **Content 구조** - Page Bundles 전환
  - `content/posts/hello-from-org/index.md` - bundle 진입점 (flat → bundle)

### Changed
- `content-org/all-posts.org` - subtree에 `:EXPORT_HUGO_BUNDLE: hello-from-org` + `:EXPORT_FILE_NAME: index` 추가. 이미지 워크플로 주석
- `hugo.toml` - languageCode(deprecated) → `[languages.ko].locale` 로 마이그레이션

### Removed
- `content/posts/hello.md` - Step 1 수동 파일 (org 단일화)
- `content/posts/hello-from-org.md` - flat 산물 (page bundle로 대체)

### Technical Notes
- Page Bundle export: ox-hugo가 `EXPORT_HUGO_BUNDLE` 보고 `content/posts/<slug>/index.md` 생성
- baseURL path 영향: 로컬 server도 `http://localhost:1313/hugo_clojure/` 하위로 serve
- export: `emacsclient --eval '(progn (find-file "...") (revert-buffer t t) (org-hugo-export-wim-to-md :all-subtrees))'`
- 검증: clean build (11 pages, deprecation/error/warning 0), 홈·글 HTTP 200, title=`hello-clojure`, lang=`ko-KR`, 삭제 글 404
- Total: 2 files added (hugo.yml, bundle index.md), 2 removed, 2 changed

---

## [Step 2: ox-hugo 파이프라인] - 2026-07-05

**Project**: hugo_clojure | **Phase**: Step 2 완료

### 결정 사항
- export: **수동** (이전 auto-export 버그·복잡도 회피. 검증 후 Step 3에서 자동화 재검토)
- org 구조: **subtree 방식** (content-org/all-posts.org — ox-hugo 공식 권장)

### Added
- **Content** (`content-org/`)
  - `all-posts.org` - org 원본. `#+hugo_base_dir: ../` + 첫 글 subtree(`hello-from-org`)
- **Content(산물)** (`content/posts/`)
  - `hello-from-org.md` - ox-hugo export 결과 (front matter TOML, 리스트, 강조, 코드 블록)

### Changed
- 없음 — config.el 미변경. `(org +hugo)` 플래그 + `#+hugo_base_dir` 속성만으로 동작

### Technical Notes
- export 명령: `emacsclient --eval '(progn (find-file ".../all-posts.org") (org-hugo-export-wim-to-md :all-subtrees))'`
- 환경: Doom Emacs `(org +hugo)`, org 9.8, ox-hugo 자동 로드됨
- 검증: localhost:1313/posts/hello-from-org/ HTTP 200, 제목·소제목·코드 블록 렌더 확인
- Total: 2 files added (org 원본 + export 산물)

---

## [Step 1: Hugo 사이트 구축] - 2026-07-05

### Added
- Hugo 새 사이트 + Ananke 테마(git submodule) + `hugo.toml`(theme)
- `content/posts/hello.md` (첫 글, draft=false)

### Changed
- Hugo 0.155.3 → 0.163.3 업그레이드 (Ananke `site.Locale` 호환)

### Technical Notes
- 검증: localhost:1313/ + /posts/hello/ HTTP 200, "안녕하세요" 렌더 → 사용자 브라우저 확인
