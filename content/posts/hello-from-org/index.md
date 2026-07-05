+++
title = "안녕하세요 클로저 블로그"
author = ["정탐"]
draft = false
+++

이 글은 `org-mode` 에서 `ox-hugo` 로 export한 첫 글입니다.
수동 export(subtree) 파이프라인이 동작하는지 확인하는 테스트 글입니다.


## 소제목 — 리스트와 강조 {#소제목-리스트와-강조}

-   일반 리스트 항목
-   **굵게** 와 _이탤릭_ 도 잘 되는지
-   `코드` 표기도 확인


## 코드 블록 {#코드-블록}

```clojure
(defn hello [name]
  (str "Hello, " name "!"))

(hello "Clojure")
```

다음 글부터는 본격적으로 Clojure 학습 노트를 올릴 예정입니다.
