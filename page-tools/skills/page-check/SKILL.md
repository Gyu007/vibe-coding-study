---
name: page-check
description: 이 저장소(vibe-coding-study)의 정적 HTML 페이지(index.html, about.html, contact.html)를 CLAUDE.md 구조 규칙과 접근성/일관성 기준으로 점검하고, 🔴🟡🟢 등급으로 보고한다. 수정은 하지 않는다.
---

# page-check

정적 HTML 페이지의 품질을 점검하는 절차. **이 스킬은 코드를 수정하지 않는다. 점검과 보고만 수행한다.**

## 점검 대상

인자로 특정 파일이 주어지면 그 파일만, 없으면 `index.html`, `about.html`, `contact.html`, `css/style.css`, `README.md`를 모두 대상으로 한다.

## 점검 절차

1. 대상 HTML 파일을 모두 읽는다.
2. 아래 체크리스트를 각 파일에 적용한다.
3. 항목별로 🔴(심각)/🟡(개선 권장)/🟢(정상) 중 하나를 매긴다.
4. 파일별로 그룹핑해서 보고서를 작성한다. 코드는 고치지 않는다.

## 체크리스트

### 기본 메타 정보 (파일별)
- `<title>` 태그 존재 여부 — 없으면 🔴
- `<meta charset="UTF-8">` 존재 여부 — 없으면 🔴
- `<meta name="viewport" ...>` 존재 여부 — 없으면 🟡 (모바일 레이아웃 깨짐 가능)
- `<html lang="ko">` 여부 — 없거나 다르면 🟡

### 접근성
- 모든 `<img>`에 `alt` 속성이 있는지 — 없으면 🔴
- `<form>` 내 `<label for="...">`와 `<input id="...">`가 정확히 매칭되는지 — 불일치 시 🟡
- 버튼/링크 텍스트가 스크린리더로 의미 파악 가능한지 (예: "여기 클릭" 같은 모호한 텍스트) — 있으면 🟡

### 사이트 일관성 (여러 파일 비교)
- `css/style.css`를 `<link rel="stylesheet">`로 연결하는지, 아니면 인라인 `<style>`을 쓰는지 — 페이지마다 방식이 다르면 🟡, 다른 페이지들과 완전히 이질적인 구조(헤더/네비/푸터 없음 등)면 🔴
- `header`/`nav`/`footer` 마크업이 세 페이지에서 동일한 패턴을 따르는지 — 어긋나면 🟡
- nav 링크가 `index.html` ↔ `about.html` ↔ `contact.html` 상호 연결되는지 — 한쪽에서만 연결되고 반대 방향 링크가 없으면 🔴 (탐색 단절)
- 활성 페이지에 `class="active"` 같은 현재 위치 표시가 있는지 — 없으면 🟢(선택 사항, 감점 없음)

### 리소스/폼
- `<img src="...">` 경로가 실제 존재하는 파일이거나 유효한 data URI인지 — 깨진 경로면 🔴
- `contact.html`의 `<form>`에 `action`/`onsubmit` 등 실제 제출 로직이 있는지 — CLAUDE.md에 따르면 정적 목업이므로 없는 것이 **정상(🟢)**, 있다면 오히려 CLAUDE.md와 불일치하니 🟡로 보고

### 저장소 차원 이슈
- `README.md`에 Git 병합 충돌 마커(`<<<<<<<`, `=======`, `>>>>>>>`)가 남아있는지 — 있으면 🔴 (CLAUDE.md에 known issue로 명시된 항목)

## 보고 형식

파일별 섹션으로 나누고, 각 항목을 등급 이모지와 함께 한 줄로 요약한다. 예:

```
## index.html
- 🔴 <title> 태그 없음
- 🟡 viewport 메타 태그 없음
- 🔴 다른 페이지로 가는 nav 링크 없음 (about.html/contact.html은 index.html로 링크하지만 역방향 없음)

## about.html
- 🟢 title/viewport/alt 모두 정상
```

마지막에 🔴 개수, 🟡 개수를 합산한 요약 줄을 추가한다. **수정 제안은 텍스트로만 언급하고 실제로 파일을 고치지 않는다.**
