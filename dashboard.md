# Dashboard — Hugo + org-mode 블로그 (hugo_clojure)

## 스토리 진행 상태
| Step | 목표 | 상태 |
|---|---|---|
| 1 | Hugo 사이트가 브라우저에 뜬다 | ✅ 완료 |
| 2 | org에서 쓰면 블로그에 뜬다 (ox-hugo) | ✅ 완료 |
| 3 | 디자인/이미지/배포 | ✅ 완료 (push 대기) |

**전체 진행률**: 3/3 (100%) — 배포는 repo push 시 활성화

## 핵심 메트릭
- **글 수**: 1 (`hello-from-org` page bundle) — org 단일화 완료
- **org 원본**: 1 (`content-org/all-posts.org`)
- **사이트**: title=`hello-clojure`, locale `ko-KR`, Ananke `bg-black`
- **baseURL**: `https://sa82trip.github.io/language-clojure/` (로컬: `http://localhost:1313/language-clojure/`)
- **배포 워크플로**: `.github/workflows/hugo.yml` (push to main) — remote 미연결
- **Hugo server**: 미실행 (필요시 `hugo server -D --port 1313`, `/hugo_clojure/` 하위 serve)
- **검증된 파이프라인**: org subtree → ox-hugo(Page Bundles) → Hugo 렌더 ✅

## 테스트 결과 (2026-07-05, Step 3)
| 항목 | 결과 |
|---|---|
| production build | 11 pages, deprecation/error/warning 0 ✅ |
| 홈 (`/language-clojure/`) | HTTP 200, title `hello-clojure` ✅ |
| 글 (`/language-clojure/posts/hello-from-org/`) | HTTP 200, page bundle 렌더 ✅ |
| `<html lang>` | `ko-KR` ✅ |
| 삭제 글 (`/language-clojure/posts/hello/`) | HTTP 404 (단일화 확인) ✅ |

## TODO (배포 이후)
1. GitHub repo 생성 + remote 연결 + push → Pages 자동 배포
2. Settings → Pages = "GitHub Actions" 확인
3. 본격 Clojure 학습 노트 작성
4. (옵션) 이미지 워크플로 실제 이미지로 end-to-end 검증
