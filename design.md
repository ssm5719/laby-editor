# LABY Editor Design System

LABY 에디터는 **laby-GUI 디자인 시스템**(Laby-4k 설정 프로그램의 `DESIGN.md`)을 그대로 따른다.
같은 LABY 제품군이라 기준을 따로 만들지 않고, laby-GUI에 없는 영상 편집 전용 요소만 **[에디터 확장]**으로 추가한다.

> 이전 버전(Atlassian 기반, 파랑·보라 팔레트)은 커밋 `0068aef`(디자인 교체 직전)에 남아 있다.

## 규칙 (laby-GUI STRICT RULES 준용)

1. **색**: 아래 표의 토큰만 쓴다. 코드에서는 `index.html` `:root`의 CSS 변수로만 참조하고, 새 HEX를 직접 쓰지 않는다.
   새 색이 필요하면 먼저 물어본다.
2. **글자 크기**: 28 / 20 / 18 / 16 / 15 / 12px 여섯 단계만 쓴다 (`--fs-*` 변수).
3. **간격**: 2 / 4 / 6 / 8 / 10 / 12 / 16 / 20 / 24 / 30px만 쓴다.
4. **Radius**: 4 / 6 / 8 / 12 / 16px, pill(9999px)만 쓴다. 세그먼트 활성 아이템의 5px만 laby-GUI 스펙상 예외.
5. **아이콘**: Material Symbols Outlined(weight 300, opsz 20)를 `<span class="ic">이름</span>`으로만 쓴다.
   재생 컨트롤(play_arrow, pause, stop)만 `.ic.fill`. 문자 기호(▶ ✂ ✕ 🔒 등)나 손으로 그린 SVG는 쓰지 않는다.
6. **새 컴포넌트**: 아래 목록에 없는 모양은 만들기 전에 물어보고, 만들었으면 이 문서에 추가한다.

## 색 위계

- **primary(주황)** = 선택 · 포함 · 강조. 에디터에서는 **ON 구간**, 선택된 칩, 현재 재생 중인 줄, 활성 탭 인디케이터.
- 카드(화면 영역) 하나에 **primary 채움 버튼은 하나**. 에디터 전체에서 채움은 "편집 완료 · 업로드"뿐이고,
  "편집안 생성"은 primary outlined.
- **초록(success)** 은 상태 표시 전용(자막 추출 완료, 목표 시간 여유, 완료 아이콘). 버튼·토글에 쓰지 않는다.
- **파랑(secondary)·보라(custom)는 쓰지 않는다.** AI 기능도 별도 색 없이 기본 컴포넌트로 표현한다.
- 주의(목표 시간 초과) = warning 주홍. 되돌릴 수 없는 파괴적 액션 = error 빨강.
- 활성/선택 줄은 회색 배경이 아니라 **좌측 4px primary 인디케이터** + row-highlight 배경.

## 토큰 → CSS 변수

| CSS 변수 | laby-GUI 토큰 | 라이트 | 다크 |
|---|---|---|---|
| `--page` | bg/base | `#FAFAFA` | `#16130F` |
| `--panel` | bg/surface(카드) | `#FFFFFF` | `#1C1917` |
| `--panel-2` | bg/raised (카드 헤더, thead, 입력 영역) | `#FAFAFA` | `#232020` |
| `--line` | border/default | `#E0E0E0` | `#2E2A26` |
| `--line-2` | modal-divider (행 구분선) | `#F0F0F0` | `#2E2A26` |
| `--line-hi` | border/hi | `#BDBDBD` | `#3D3833` |
| `--ink` | text/primary | `#212121` | `#F5F5F5` |
| `--ink-2` | text/secondary | `#616161` | `#E0E0E0` |
| `--neutral` | neutral/default (outlined 버튼·아이콘 버튼 글자) | `#424242` | `#F5F5F5` |
| `--muted` | text/caption | `#9E9E9E` | `#9E9E9E` |
| `--dis` / `--dis-bg` | text/disabled / bg/surface·disabled-surface | `#BDBDBD` / `#EEEEEE` | `#757575` / `#2E2E2E` |
| `--pri` | primary/default | `#FF9800` | `#FF9800` |
| `--pri-strong` | primary/strong (텍스트·hover) | `#F57C00` | `#FFA726` |
| `--pri-subtle` | primary/subtle (입력 hover) | `#FFA726` | `#FFA726` |
| `--pri-surface` | primary/surface | `#FFF3E0` | `#3D2C14` |
| `--row-hl` | row-highlight-bg | `#FFFBF4` | `#2B2115` |
| `--ok` / `--ok-dot` / `--ok-soft` | success/strong·default / surface | `#52B904` / `#82D323` / `#F2FDE5` | `#9BE83F` / `#9BE83F` / `#1F2E12` |
| `--warn` / `--warn-soft` | warning/default / surface | `#FF5722` / `#FBE9E7` | `#FFA83D` / `#3A2018` |
| `--err` / `--err-soft` | error/default / surface | `#F44336` / `#FEEBEE` | `#FF6B5E` / `#31161A` |
| `--seg-track` / `--seg-on` / `--seg-on-line` | segment-track-bg / active-bg / active-border | `#F5F5F5` / `#FFFFFF` / `#9E9E9E` | `#16130F` / `#302C28` / `#4A443E` |
| `--tip` / `--tip-ink` | neutral/strong (툴팁·토스트) | `#212121` / `#FAFAFA` | `#302C28` / `#F5F5F5` |
| `--stage` | base(dark) — 영상 배경 | `#111111` | `#111111` |

다크 값은 `:root`의 `prefers-color-scheme` 블록과 `[data-theme="dark"]` 블록 **두 곳에 똑같이** 넣는다.

### [에디터 확장] 편집 상태 색

laby-GUI에 없는 영상 편집 상태를 기존 토큰에 매핑한 것이다. 새 HEX는 만들지 않았다.

| CSS 변수 | 의미 | 매핑 | 라이트 | 다크 |
|---|---|---|---|---|
| `--show` / `--show-soft` | ON 구간(결과물에 포함) | primary/default / surface | `#FF9800` / `#FFF3E0` | `#FF9800` / `#3D2C14` |
| `--hide` | OFF 구간 채우기 | state/disabled · border/hi(다크) | `#E0E0E0` | `#3D3833` |
| `--hide-soft` | 시크바 트랙 | inherit/default · bg/base(다크) | `#F5F5F5` | `#16130F` |
| `--intro` | 인트로 삽입 표시(시크바 막대·범례) | channel/scene strong · scene(라이트값) | `#45495D` | `#C9C4BC` |
| `--intro-soft` / `--intro-lbl` | `intro` 뱃지 채움 / 글자 | channel/scene default / label | `#C9C4BC` / `#212121` | `#5A5651` / `#F5F5F5` |
| `--bar` | 재생 위치(헤드·세로선) | text/primary | `#212121` | `#F5F5F5` |

- 재생 위치는 영상 편집기 관례대로 **무채색 세로선**. 주황은 ON 구간 전용이라 겹치지 않게 했다.
- 영상 위 오버레이(태그, 실시간 자막)는 `rgba(33,33,33,.8)`(neutral/strong 80%), 인트로 화면은 `rgba(69,73,93,.92)`(scene strong 92%).

## 타이포그래피

- 한글 **Noto Sans KR** (`--ui`), 영문·숫자·타임코드 **IBM Plex Sans KR** (`--num`, `font-variant-numeric: tabular-nums`).

| 역할 | 크기 / 굵기 / 행간 | 에디터 사용처 |
|---|---|---|
| display | 28 / 700 / 36 | 문서 제목 |
| h1 | 20 / 700 / 36 | 업로드 확인의 최종 길이 숫자 |
| h2 | 18 / 600 / 24 | 문서 섹션 제목, 인트로 화면 제목 |
| h3 · subtitle | 16 / 600·500 / 23 | 모달 제목, 카드 제목, 브랜드 |
| body · body-strong | 15 / 400·600 / 22 | 자막 문장, 탭, 버튼(md), 표 본문, 입력값 |
| caption | 12 / 400 / 20 | 시간·메타 정보, 뱃지, 칩, 안내 문구, 범례, 버튼(sm·xs) |

## 컴포넌트

| 컴포넌트 | 스펙 | 클래스 |
|---|---|---|
| Button md | 높이 32, radius 6, 좌우 12, 15px **Regular(400)** — contained도 굵게 하지 않음(600은 lg 40px 전용). contained(primary) = `.btn.pri` 흰 글자, outlined(neutral) = `.btn` 글자 neutral/default, outlined(primary) = `.btn.pri-o` 글자 primary/default | `.btn` |
| Button sm | 높이 28, radius 4, 12px | `.btn.sm` |
| 아이콘 버튼 | 32×32, radius 6, 아이콘 20. `title`·`aria-label` 필수 | `.tb` |
| ON/OFF | Button xs: 높이 22, radius 4, 12px. ON = primary 채움, OFF = neutral outlined, 일부 = primary surface | `.tgl` |
| Badge xs | 높이 22, pill, 12px. 상태는 시맨틱 subtle, 그 외 default | `.badge` |
| 정적 라벨 뱃지 | 높이 22, radius 4, 12px. `ppt` = default outlined, `intro` = scene 채움 | `.bdg` |
| 필터 칩 | 높이 28, pill, 12px. 선택 = primary 채움, 비선택 = default outlined, hover = primary 테두리·surface | `.chip` |
| Tabs | 언더라인. 좌우 16·상하 10, 15px. 활성 600 + 하단 2px primary, 비활성 text/secondary 500 | `.tab` |
| Segmented Toggle | 트랙 `--seg-track` · radius 6 · 안쪽 2. 활성 아이템은 흰 배경 + 보더 + 그림자(primary 채움 없음) | `.seg` |
| Input | md 32 / sm 28, radius 4, 좌우 10. hover primary/subtle, focus primary/strong 테두리 | `.ai-in input`, `.srch input`, `.lenbox input` |
| Card | 보더 1px, radius 8. 제목 영역 raised 배경 · 좌우 20 · 상하 12 · 16px 600 | `.mock`, `.note`, `.tbl` |
| Modal basic | 최대 572px, radius 8. 헤더·푸터 좌우 24 · 상하 16 + 구분선, 본문 24. 취소 = outlined, 확인 = contained, 간격 10 | `.modalcard` |
| Spinner | 지름 20, 테두리 2, 트랙 `--hide` + 회전 구간 primary | `.spin` |
| Toast | 하단 중앙, radius 8, 좌우 16 · 상하 8, 12px, `--tip` 배경 | `.toast` |

### [에디터 확장] 편집 전용 요소

| 요소 | 스펙 |
|---|---|
| 시크바 | 높이 32 트랙(`--hide-soft`, radius 4). ON 블록 = primary(양 끝 1px primary/strong 경계), OFF 블록 = `--hide`, 인트로 = 4px `--intro` 막대 |
| 탐색 구역 | 높이 16, raised 배경. 재생 헤드 = `--bar` 삼각형 + 2px 세로선 |
| 자막 행 | 시간(12px, 44px 폭) + 문장(15px). 편집본 포함 = 좌측 4px primary, 재생 중 = row-highlight + 주황 시간, 제외 = 취소선 + caption 색 |
| 슬라이드 헤더 | sticky, raised 배경, 15px 600 |
| 검색 형광펜 | primary surface 배경 + 하단 2px primary. 현재 결과는 primary 채움 |

## 아이콘 사용 목록

laby-GUI 목록에서 쓰는 것: `play_arrow`·`pause`·`stop`(채움), `content_cut`, `search`, `keyboard_arrow_up`/`keyboard_arrow_down`, `close`, `check_circle`, `cloud_upload`.

**[에디터 확장] 추가 아이콘** (laby-GUI 목록에 없어 에디터에서 새로 쓰는 것):

| 이름 | 사용처 |
|---|---|
| `undo` / `redo` | 실행취소 / 다시실행 버튼 |
| `lock` | 자막이 필요한 칩이 잠겼을 때 |
