# Claude Code 프롬프트 모음

- 프로젝트: `D:\classClaude\classProject\class-ui-component2`
- 범위: cwd 전체 합본 (증분)
- 추출 시각: 2026-07-30 05:24:30
- 세션 수: 1 / 프롬프트 수: 8

---

### 1. 2026-07-29

https://careerfoundry.com/en/blog/ui-design/ui-element-glossary/ 를 기반으로 32가지 UI 컴포넌트와 컴포넌트의 미리보기, HTML, CSS, Javascript(있을경우) 코드 영역에 해당 코드들이 로드되어야 하고, 코드 하일라이트 기본적인 기능들이 적용되어야 해. 각 소스마다 복사하기 버튼을 통해 해당 요소를 복사해서 내 사이트에 붙여넣기 하는 컴포넌트 페이지를 만드는거야.

촤측에는 UI 요소 리스트와 UX에 필요한 기본적인 공통 모달(경고, 확인, 알림, 토스트, 스낵바, 바텀 시트 등 사이트에 꼭 필요한 알림등 레이어 처리 관련 컴포넌트)들을 포함해서 해당 리스트를 누르면 우측 메인 컨텐츠 영역에 클릭한 컴포넌트 명 - 정의와 설명이 나오고 하단에는 미리보기 html, css, js 탭들이 나와서 각각의 기능을 수항하면 돼

참고해야 할 리소스는 @docs/resource/component-portfolio.html 구조를 비롯해서 @docs/resource/ui-component.html @docs/resource/ui-components-32-catalog.html 이고 @docs/resource/label-chip-system.html @docs/resource/alert-ui-showcase.html 이고 @docs/resource/ 에 참고할 자료들들을 업로드 해놨어.

이를 바탕으로 /init 을 실행해서 기본적인 CLAUDE.md를 비롯한 초기화 작업 진행하고 CLAUDE.md는 한글로 작성해

### 2. 2026-07-29

[Request interrupted by user for tool use]

### 3. 2026-07-29

https://careerfoundry.com/en/blog/ui-design/ui-element-glossary/ 를 기반으로 32가지 UI 컴포넌트와 컴포넌트의 미리보기, HTML, CSS, Javascript(있을경우) 코드 영역에 해당 코드들이 로드되어야 하고, 코드 하일라이트 기본적인 기능들이 적용되어야 해. 각 소스마다 복사하기 버튼을 통해 해당 요소를 복사해서 내 사이트에 붙여넣기 하는 컴포넌트 페이지를 만드는거야.

촤측에는 UI 요소 리스트와 UX에 필요한 기본적인 공통 모달(경고, 확인, 알림, 토스트, 스낵바, 바텀 시트 등 사이트에 꼭 필요한 알림등 레이어 처리 관련 컴포넌트)들을 포함해서 해당 리스트를 누르면 우측 메인 컨텐츠 영역에 클릭한 컴포넌트 명 - 정의와 설명이 나오고 하단에는 미리보기 html, css, js 탭들이 나와서 각각의 기능을 수항하면 돼

참고해야 할 리소스는 @docs/resource/component-portfolio.html 구조를 비롯해서 @docs/resource/ui-component.html @docs/resource/ui-components-32-catalog.html 이고 @docs/resource/label-chip-system.html @docs/resource/alert-ui-showcase.html 이고 @docs/resource/ 에 참고할 자료들들을 업로드 해놨어.

이를 바탕으로 /init 을 실행해서 기본적인 CLAUDE.md를 비롯한 초기화 작업 진행하고 CLAUDE.md는 한글로 작성해

### 4. 2026-07-29

handoff 스킬을 만들거야. 

# handoff — 세션 인계

세션을 넘길 때 아래를 한 파일(`.handoff.md` 또는 STATE)에 적는다.

- ✅ **무엇이 됐나** (검증된 증거와 함께)
- ❌ **무엇을 시도했고 실패했나** (반복 방지)
- ⏳ **다음 할 일 + 아직 안 한 것**

체크리스트 형태로 만들어줘

### 5. 2026-07-29

핸드오프 스킬 검증해봐

### 6. 2026-07-29

분석한 결과를 바탕으로 @CLAUDE.md 를 다시 참조해서 ui-kit-playground.html 파일을 프로젝트 루트에 생성해줘

### 7. 2026-07-29

extract-my-prompts.sh의 두 줄을 python3 → python으로 바꿨는데 여전히 프롬프트 기록 Stop hook이 실행되지 않아.

### 8. 2026-07-29

extract-my-prompts.sh의 두 줄을 python3 → python으로 바꿨는데 여전히 프롬프트 기록 Stop hook이 실행되지 않아

### 9. 2026-07-29

ui-kit-playground.html 결과를 확인해보니 한가지 수정이 필요해.
아코디언 메뉴 화면의 경우 너비가 클릭 전, 클릭 후 사이즈가 다른데 사이즈가 일정하도록 보정을 해야 하고 아코디언 바와 같은 동작이 없이 클릭 후 펼침, 접힘 기능만 되고 있으니 아코디언 바 처럼 수정해야함

