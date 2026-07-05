# hello-clojure

Clojure 학습 노트 블로그. org-mode로 글을 쓰고 ox-hugo + Hugo 파이프라인으로 GitHub Pages에 배포합니다.

🔗 **https://sa82trip.github.io/language-clojure/**

## 기능

- **Hugo** 정적 사이트 생성 (v0.163.3+extended)
- **Ananke** 테마
- **org-mode → ox-hugo**: Emacs org 문서를 Hugo 마크다운으로 export
- **Page Bundles**: 글별 디렉토리 구조 (이미지 등 자산을 글과 함께)
- **GitHub Actions** 자동 배포 — `main` push 시 빌드/배포

## 저장소 구조

```
hugo_clojure/                      작업 공간 루트
├── content-org/all-posts.org      org 원본 (이 repo 외부)
└── hugo_clojure_log/              ← 이 저장소 (Hugo 프로젝트)
    ├── content/posts/<slug>/      export 산물 (배포 대상)
    ├── hugo.toml                  사이트 설정
    └── .github/workflows/hugo.yml 배포 워크플로
```

org 원본(`all-posts.org`)은 작업 루트에 두어 관리하고, 이 저장소에는 export된 마크다운과 Hugo 설정만 추적합니다.

## 글 추가 방법

### 1. org 원본에 subtree 추가

`../content-org/all-posts.org` 에 글 subtree를 추가합니다:

```org
* 글 제목
:PROPERTIES:
:EXPORT_FILE_NAME: index
:EXPORT_HUGO_BUNDLE: my-post
:EXPORT_HUGO_DRAFT: nil
:END:

본문을 여기에 작성...
```

- `EXPORT_HUGO_BUNDLE` = 디렉토리 slug
- `EXPORT_FILE_NAME: index` = bundle 진입점

### 2. export (Emacs 서버 실행 중)

```bash
emacsclient --eval '(progn (find-file "../content-org/all-posts.org") (revert-buffer t t) (org-hugo-export-wim-to-md :all-subtrees))'
```

→ `content/posts/my-post/index.md` 가 생성됩니다.

### 3. 배포

```bash
git add -A
git commit -m "새 글: 글 제목"
git push
```

push하면 GitHub Actions가 자동으로 빌드하여 GitHub Pages에 배포합니다.

## 이미지 추가 (Page Bundle)

글과 같은 bundle의 `images/` 폴더에 이미지를 넣고, org에서 참조합니다:

```
content/posts/my-post/
├── index.md
└── images/
    └── diagram.png
```

```org
[[file:images/diagram.png]]
```

## 사이트 설정 요약

| 항목 | 값 |
|---|---|
| title | hello-clojure |
| 언어 | ko-KR |
| 테마 | Ananke (배경 bg-black) |
| author | 정탐 |
| baseURL | https://sa82trip.github.io/language-clojure/ |
