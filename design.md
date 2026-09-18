# LABY Editor Design System

## Overview

Atlassian Design System을 기반으로, **LABY 에디터**(영상 구간 편집 도구)의 실제 화면 요구사항에 맞게 보완한 버전입니다.
원본 Atlassian 시스템의 원칙(명료함·일관성·목적 있는 밀도)은 그대로 따르되, 원본에 없는 토큰이 필요한 지점은
**"[확장]"** 표시와 함께 명시적으로 추가했습니다. 임의로 규칙을 어긴 게 아니라, 원본이 다루지 않는 영역(영상
타임라인 편집)에 대해 같은 원칙으로 새 토큰을 정의했다는 뜻입니다.

## Brand Colors

### Core (Atlassian 원본 유지)

| Token | Hex | Usage |
|-------|-----|-------|
| Blue 700 | `#1868DB` | 주요 액션, 링크, 포커스 상태, **ON(Show) 구간 채우기** |
| Blue 800 | `#0055CC` | Hover 상태 |
| Blue 900 | `#09326C` | Active/Pressed 상태 |
| Neutral 0 | `#FFFFFF` | 패널/카드 표면 |
| Neutral 100 | `#F7F8F9` | 페이지 배경 |
| Neutral 200 | `#DCDFE4` | 테두리, 구분선 |
| Neutral 800 | `#172B4D` | 본문 텍스트(주) |
| Neutral 600 | `#44546F` | 본문 텍스트(보조) |

### Neutral 확장 [확장]

Atlassian 원본은 5단계 뉴트럴만 정의합니다. 에디터의 조밀한 UI(패널 안 패널, 흐린 보조 텍스트, 비활성 블록 등)에는
단계가 더 필요해서 같은 색상축 위에 보간했습니다.

| Token | Hex | Usage |
|-------|-----|-------|
| Neutral 75 | `#FAFBFC` | 패널 내부의 보조 표면(예: 상단 툴바, 탭 바 배경) |
| Neutral 150 | `#EDEFF2` | 옅은 구분선(셀 사이 등 경계가 약해야 하는 곳) |
| Neutral 300 | `#C1C7D0` | OFF(Hide) 구간 채우기, 비활성 상태 |
| Neutral 500 | `#6B778C` | 3차 텍스트(타임스탬프, 메타정보) |
| Canvas 1000 | `#0B0C0F` | **영상 스테이지 배경 전용.** 테마와 무관하게 항상 고정되는 검정 — 뉴트럴 스케일이 아니라 "비디오 캔버스"로 별도 관리 |

### Status

| Token | Hex | Usage |
|-------|-----|-------|
| Green 700 | `#22A06B` | 성공(저장 완료) |
| Yellow 600 | `#B38600` | 주의(구간 제외처럼 되돌릴 수 있는 편집 액션) |
| Red 700 | `#CA3521` | 오류, 파괴적 동작의 최종 확인 |
| Teal 600 | `#1D7F8C` | 정보성 안내 |
| Purple 700 | `#6E5DC6` | Discovery — **AI 기능, "AI 추천 구간" 표시 전용** |

### Timeline Amber [확장]

재생 위치 표시와 "지금 드래그로 선택 중인 구간"은 Atlassian 기본 토큰 어디에도 없는, 영상 편집 도구 특유의 상태입니다.
Yellow 600(경고)를 재사용하면 "경고"로 오인되므로, 의도적으로 다른 색상을 새로 정의합니다.

| Token | Hex | Usage |
|-------|-----|-------|
| Timeline Amber 600 | `#B65C1F` | 재생 위치(playhead), 드래그로 선택 중인 구간의 테두리 |
| Timeline Amber 100 | `#FBEEE3` | 위 상태의 옅은 배경 |

### Dark Mode [확장 — 원본 문서에 다크모드 정의 없음]

| Token | Light | Dark |
|-------|-------|------|
| Surface | `#FFFFFF` | `#1E1A25` |
| Page bg | `#F7F8F9` | `#141118` |
| Border | `#DCDFE4` | `#372F42` |
| Text(주) | `#172B4D` | `#EDE8F2` |
| Text(보조) | `#44546F` | `#C2BACF` |
| Blue(ON) | `#1868DB` | `#6699FF` |
| Purple(AI) | `#6E5DC6` | `#CE8ACE` |
| Timeline Amber | `#B65C1F` | `#F0965A` |

## Typography

**본문/UI/제목 전체:** Noto Sans KR (400 / 500 / 700)
**숫자·타임코드·모노스페이스:** IBM Plex Mono (400 / 500)

> Atlassian Sans/Mono 대신 이 두 서체로 대체합니다. 헤딩도 별도 디스플레이 서체를 쓰지 않고 Noto Sans KR 700로
> 통일해서, 서체 자체는 두 개만 유지합니다(로딩 비용·일관성 확보).

### 문서/설명 텍스트 (스펙 페이지 등 정적 콘텐츠용)

Atlassian 스케일을 그대로 따르되, Noto Sans KR에 없는 600 weight는 700으로 대체합니다.

| Role | Size | Line Height | Weight |
|------|------|-------------|--------|
| Display | 35px | 40px | 700 |
| Heading 1 | 29px | 32px | 700 |
| Heading 2 | 24px | 28px | 500 |
| Heading 3 | 20px | 24px | 500 |
| Body | 14px | 20px | 400 |
| Small | 12px | 16px | 400 |

### 컴포넌트/조작 UI 텍스트 [확장 — 고밀도 도구용]

편집기 자체(자막 리스트, Edit List, 시크바 라벨 등)는 문서보다 훨씬 조밀합니다. "Small(12px)" 아래로 토큰이
없다는 게 원본의 공백이라, 두 단계를 추가합니다.

| Role | Size | Line Height | Weight | Font |
|------|------|-------------|--------|------|
| UI Body | 13px | 1.6 | 400 | Noto Sans KR |
| UI Meta | 11.5px | 1.4 | 400 | IBM Plex Mono |
| UI Micro | 10px | 1.4 | 700, letter-spacing .15em, uppercase | Noto Sans KR |

## Spacing

8px 그리드 원칙 유지. 고밀도 편집 UI를 위해 절반 단위(4px, 12px)를 [확장]으로 추가합니다.

| Token | Value | 비고 |
|-------|-------|------|
| space.050 | 4px | [확장] 아이콘-텍스트 간격 등 미세 조정 |
| space.100 | 8px | 기본 단위 |
| space.150 | 12px | [확장] 버튼 내부 패딩 등 |
| space.200 | 16px | |
| space.300 | 24px | |
| space.400 | 32px | |

## 색상만으로 의미를 전달하지 않기 (원본 규칙 보완)

원본 규칙 "색으로만 의미를 전달하지 마라"에 맞춰, 지금까지 색으로만 구분되던 상태들을 아래처럼 보강합니다.

| 상태 | 색상 | 추가 구분 요소 |
|---|---|---|
| ON(Show) 구간 | Blue 700 채우기 | 블록 좌측에 체크 아이콘 |
| OFF(Hide) 구간 | Neutral 300 | 블록에 "숨김" 텍스트 라벨(hover 시 노출) |
| AI가 고른 구간 (자막 리스트) | Purple 700 좌측 테두리(실선) | 자막 앞에 보라색 점(●) 아이콘 추가 |
| 수동 선택 중인 구간 | Timeline Amber 좌측 테두리(**점선**) | AI 추천과 테두리 스타일(실선/점선)로도 구분 |
| 리사이즈 핸들 | — | 항상 좌우 끝에 물리적 손잡이(막대 아이콘)로 표시, 색에 의존하지 않음 |

## 버튼 컴포넌트 (표준화 — 커스텀 버튼 금지 규칙 보완)

원본 규칙 "커스텀 버튼 스타일 만들지 마라"에 따라, 지금까지 화면마다 즉흥적으로 만들던 버튼들을 4종으로
표준화해서 이 시스템의 공식 컴포넌트로 편입합니다. 새 버튼이 필요하면 아래 4종 중에서 고르고, 새로 만들지 않습니다.

| Variant | 배경 | 텍스트 | 테두리 | 용도 |
|---|---|---|---|---|
| Primary | Blue 700 | White | 없음 | 저장, 이 구간 추가처럼 확정 액션 |
| Secondary | Neutral 0 | Neutral 800 | Neutral 200 | 취소, 보조 액션 |
| Caution | Neutral 0 | Yellow 600 | Yellow 600 | 이 구간 제외처럼 되돌릴 수 있는 편집 |
| Ghost-Icon | 투명 | Neutral 500 | 없음 | 모달 닫기(✕) 등 최소 강조 액션 |

- 모든 버튼은 `border-radius: 6px`, 세로 패딩 `space.100`(8px), 가로 패딩 `space.150`(12px) 고정.
- 아이콘 단독 버튼 금지 — Ghost-Icon도 `title` 툴팁 필수.

## Do's and Don'ts

### Do's
- 주요 액션(저장, 추가 확정)에는 Blue 700만 사용 — Primary 버튼을 두 개 이상 나란히 두지 않기
- 텍스트 대비 4.5:1 유지
- 8px 그리드(및 확장된 4px 절반 단위) 안에서만 여백 사용
- 상태(ON/OFF/AI추천/수동선택)는 색 + 아이콘/패턴을 함께 표시
- AI 관련 표시는 항상 Purple 700으로 통일 — 다른 보라색 임의 사용 금지

### Don'ts
- 색으로만 의미를 전달하지 않기
- Noto Sans KR / IBM Plex Mono 외 서체 사용 금지
- 버튼 4종(Primary/Secondary/Caution/Ghost-Icon) 외 새 버튼 스타일 임의 생성 금지
- Timeline Amber를 경고(Yellow) 대용으로 쓰지 않기 — 반드시 재생위치·수동선택 용도로만
- Canvas 1000(영상 배경)을 일반 다크 서페이스 색으로 재사용하지 않기

## 이 문서에서 원본 대비 추가된 토큰 요약

투명성을 위해, 원본 Atlassian 스펙에 없던 것 중 이 문서에서 새로 정의한 항목만 모았습니다.

- **색상**: Neutral 75 / 150 / 300 / 500, Canvas 1000, Timeline Amber 600·100, Dark Mode 전체
- **타이포**: UI Body / UI Meta / UI Micro 세 단계
- **여백**: space.050(4px), space.150(12px)
- **컴포넌트**: 버튼 4종 표준(Primary/Secondary/Caution/Ghost-Icon)

## Resources

- [Atlassian Design System](https://atlassian.design/) (원본)
- 이 문서는 위 원본을 laby-editor 프로젝트용으로 각색한 내부 버전입니다.
