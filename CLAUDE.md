# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

CareerFoundry의 ["32 UI Elements Designers Need To Know"](https://careerfoundry.com/en/blog/ui-design/ui-element-glossary/) 글로서리에 나오는 32가지 UI 컴포넌트 + 사이트 운영에 필수인 공통 UX 레이어 컴포넌트 6종(경고/확인/토스트/스낵바/바텀시트/알림 배너)을 합쳐 총 38개 컴포넌트를 보여주는 프론트엔드 학습·레퍼런스 사이트다. 좌측 사이드바에서 컴포넌트를 선택하면 우측에 이름·정의/설명과 함께 미리보기 · HTML · CSS · JS 탭이 나타나며, 각 코드 블록은 자체 구현한 문법 하이라이트가 적용되고 원본 소스를 그대로 클립보드에 복사하는 버튼이 붙어 있다.

빌드 도구나 패키지 매니저 없이 **`ui-kit-playground.html` 단일 파일**로 전체가 구성되며, 외부 의존성은 Google Fonts(Noto Sans KR, JetBrains Mono) 링크 2개뿐이다. 브라우저에서 `ui-kit-playground.html`을 직접 열면 그대로 동작한다 — 별도의 설치·빌드·서버 실행 명령이 없다.

`index.html`은 실제 앱이 아니라 `docs/resource/TROUBLE_SHOOTING.md`의 "정본은 하나로 유지 + 루트는 리다이렉트" 패턴을 따르는 얇은 리다이렉트 stub이다(GitHub Pages는 루트 URL에서 `index.html`을 찾으므로). 실제 컴포넌트/로직 수정은 항상 `ui-kit-playground.html`에서 한다 — `index.html`은 `<meta http-equiv="refresh">`로 그리로 넘길 뿐, 유지보수 대상이 아니다.

## 강제 디자인 규칙: `.claude/rules/anti-ai-slop.md`

이 저장소에 새 시각 요소(HTML/CSS/JS/컴포넌트)를 추가하거나 수정할 때는 **반드시** `.claude/rules/anti-ai-slop.md`에 정의된 규칙을 지켜야 한다. 핵심만 요약하면:

- 그라데이션(`linear-gradient`/`radial-gradient`/`conic-gradient`), 컬러가 들어간 `box-shadow`/글로우, `backdrop-filter: blur` 전면 금지.
- hover/load 시 `transform: scale/translate`, fade/stagger, pulse/shimmer/float/glow 키프레임 등 장식용 모션 금지. 단, 컴포넌트 본연의 기능인 모션(예: Loader의 스피너 회전, 스켈레톤 펄스)은 장식이 아니므로 예외.
- 색상은 무채색(흰/회/검) 베이스 + 단일 액센트 색(`--accent: #2563eb`)만 사용, 색은 항상 의미(상태·위계)에만 쓴다.
- 그림자는 없거나 중성 회색 1단계까지만. 구획은 효과 대신 `1px solid` 보더 + 여백으로 나눈다.
- `border-radius`는 0~8px. 이모지 불릿, 배지/pill 남용, 마케팅 상투어 금지.
- 폰트는 기본값(Inter/Roboto/Arial/system-ui)으로 수렴하지 말고 의도적으로 선택 + 이유 한 줄을 남긴다. 이 저장소는 이미 `--sans: "Noto Sans KR"`(한국어 가독성) + `--mono: "JetBrains Mono"`(코드 글자 구분)를 선택한 상태이며, `index.html` 상단 CSS 주석에 그 이유가 적혀 있다.

## `docs/resource/` 참고 자료 — 그대로 베끼지 말 것

`docs/resource/`에는 이 사이트를 만들 때 참고한 원본 HTML 프로토타입들이 들어 있다. 이 폴더는 수정하지 않는다(사이트 본체는 `index.html`뿐). 파일별 성격이 다르므로 주의:

- `component-portfolio.html` (= `ui-elements-demo.html`, 완전히 동일한 파일) — `index.html`의 레이아웃·데이터 구조·핵심 로직(`select()`, `buildSrcdoc()`, 사이드바 카테고리 렌더링)의 실제 출처. anti-slop 규칙을 이미 준수하는 유일한 참고 파일이라 구조를 그대로 가져와 확장했다.
- `ui-component.html`, `ui-components-32-catalog.html`, `alert-ui-showcase.html`, `color-personal-card.html`, `colorpicker.html` — 그라데이션, 컬러 글로우 그림자, hover scale 등 anti-slop 규칙을 위반하는 시각 스타일을 쓴다. 컴포넌트 아이디어·커버리지 체크리스트로만 참고하고, CSS/시각 스타일은 절대 그대로 옮기지 않는다.

## `ui-kit-playground.html` 구조 (실제 앱 — 정본)

전체가 `<style>` 하나 + `<script>` 하나로 이루어진 단일 파일이며, 핵심 구성은 다음과 같다.

**데이터 모델** — 모든 컴포넌트는 `{ n, name, ko, cat, desc, html, css, js }` 형태의 객체다. `n`은 1~38 연속 번호, `cat`은 `layer|input|nav|info|container` 중 하나다.

- `ELEMENTS_LAYER` (33~38번, `cat:"layer"`): Alert, Confirm, Toast, Snackbar, Bottom Sheet, Notification Banner — 공통 UX 레이어 6종. 20번 "Notification"(정적 벨+배지 일러스트, JS 없음)과 35번 "Toast"(실제 동작하는 트리거+자동소멸)는 서로 다른 컴포넌트이니 혼동해 통합하지 않는다.
- `ELEMENTS` (1~32번): CareerFoundry 글로서리의 32개 컴포넌트.
- `DATA = ELEMENTS_LAYER.concat(ELEMENTS)`가 전체 목록이며, `CATS`/`CAT_ORDER`(`["layer","input","nav","info","container"]`)가 사이드바 그룹 순서를 정의한다. 새 컴포넌트를 추가할 때는 이 셋(데이터 배열, `CATS`가 필요하면, `CAT_ORDER`) 중 맞는 곳에 항목을 넣기만 하면 사이드바·탭·미리보기가 자동으로 생성된다.

**핵심 함수:**

- `highlightCode(src, lang)` — 외부 라이브러리 없이 정규식(`HL_RULES.html/css/js`, named capture group)으로 주석/태그·셀렉터/속성/문자열을 구분해 `<span class="tok-*">`로 감싸는 자체 구현 하이라이터. 코드 표시(`<code>` 내부)에만 쓰이고, 색은 anti-slop 규칙에 맞춰 회색(주석)·액센트(태그/키워드)·잉크색(그 외) 2톤만 사용한다.
- `codeBlock(label, source, lang)` — 코드 패널 하나(HTML/CSS/JS)를 만든다. 복사 버튼은 항상 `e.html`/`e.css`/`e.js` **원본 문자열**을 클립보드에 쓰므로, 하이라이트 마크업이 복사본에 섞이지 않는다.
- `buildSrcdoc(e)` — 컴포넌트의 html/css/js를 조합해 `<iframe srcdoc>`용 완전한 HTML 문서를 만든다. 각 컴포넌트의 미리보기는 이렇게 서로 격리된 iframe 안에서 실행된다.
- `select(n)` — 사이드바 클릭 시 호출되며, 상세 헤더(번호/이름/한글명/카테고리 배지)·설명·탭·코드 패널을 렌더링하고 iframe의 `srcdoc`을 프로퍼티로 할당한다(속성 문자열 escape 문제 회피).

## 로컬에서 확인하기

빌드 명령이 없다. `ui-kit-playground.html`을 브라우저로 직접 열면(`file://` 또는 정적 서버 둘 다 가능) 바로 확인할 수 있다. `index.html`을 열어도 즉시 리다이렉트되긴 하지만, 개발 중에는 `ui-kit-playground.html`을 바로 여는 편이 리다이렉트 지연 없이 확인하기 편하다. 코드 문법 오류만 빠르게 확인하려면 인라인 `<script>` 블록을 추출해 `node --check`로 검사할 수 있다.

## 프롬프트 기록 훅

`.claude/settings.json`에 **Stop 훅**이 걸려 있어, 세션 종료 시 `extract-my-prompts.sh`가 이 폴더의 Claude Code 세션에서 사용자가 입력한 프롬프트만 뽑아 [Prompt.md](Prompt.md)에 append한다.
