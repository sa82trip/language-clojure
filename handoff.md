# Hugo + org-mode 블로그 (hugo_clojure) — 밑바닥부터 차근차근

## 현재 상태
**Phase**: ✅ Step 3 완료 — 디자인/이미지(Page Bundles)/배포(GitHub Pages 워크플로) 설정됨. repo push 대기
**다음 작업**: GitHub repo 생성 + push → 자동 배포, 그 다음 본격 Clojure 학습 노트 작성

## 3단계 로드맵
| Step | 목표 ("됐다" 순간) | 상태 |
|---|---|---|
| 1 | Hugo 사이트가 브라우저에 뜬다 | ✅ 완료 |
| 2 | org에서 쓰면 블로그에 뜬다 (ox-hugo) | ✅ 완료 |
| 3 | 디자인/이미지/배포 | ✅ 완료 (push 대기) |

## 핵심 워크플로우
- **원본**: `content-org/all-posts.org` (subtree 방식). 각 subtree에 `:EXPORT_HUGO_BUNDLE: <slug>` + `:EXPORT_FILE_NAME: index`
- **Page Bundles**: export → `content/posts/<slug>/index.md`. 이미지는 같은 bundle의 `images/` 폴더, org 참조 `[[file:images/<name>.jpg]]`
- **수동 export** (Emacs 서버 떠있을 때): `emacsclient --eval '(progn (find-file ".../content-org/all-posts.org") (revert-buffer t t) (org-hugo-export-wim-to-md :all-subtrees))'`
- **baseURL**: `https://sa82trip.github.io/language-clojure/` — 로컬 server도 `/language-clojure/` 하위로 serve (`http://localhost:1313/language-clojure/`)

## 환경
- Hugo v0.163.3+extended / Ananke (git submodule)
- config: `hugo.toml` — title=`hello-clojure`, locale `ko-KR`, Ananke `bg-black`
- 배포: `.github/workflows/hugo.yml` (Hugo 공식 Pages 액션, push to main 트리거). **remote 아직 없음**
- 경로: `/Users/js/Documents/projects/ex_ordinaries/hugo_clojure`
- 서버: `hugo server -D --port 1313` (현재 미실행 — 필요시 재시작, `/hugo_clojure/` 하위로 serve)

## 최근 작업
### 2026-07-05: Step 3 — 디자인/이미지/배포 (완료)
- **결정**: Ananke 유지+튜닝, Page Bundles, GitHub Pages, hello.md 삭제(org 단일화)
- **Config**: `hugo.toml` — baseURL/title/locale/`[languages.ko]`/Ananke params
- **Page Bundles**: org `EXPORT_HUGO_BUNDLE` 추가, flat `hello-from-org.md` → `hello-from-org/index.md`
- **배포**: `.github/workflows/hugo.yml` (Hugo 공식 Pages 워크플로)
- **검증**: clean build(11p, deprecation 0), 홈/글 200 + title·lang 확인, hello 404

## 알려진 이슈
- GitHub remote 없음 → repo 생성 + push 시 자동 배포 시작
- 이미지 참조 워크플로는 구조만 잡고 실제 이미지 미검증 (첫 이미지 글에서 검증 예정)

## TODO
1. ⏳ GitHub repo 생성 + remote 연결 + push → Pages 배포 (Settings → Pages = GitHub Actions)
2. 본격 Clojure 학습 노트 작성 (all-posts.org에 subtree 추가)
3. (옵션) 이미지 워크플로 실제 이미지로 end-to-end 검증
