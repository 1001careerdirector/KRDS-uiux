# KRDS Figma 제작 사양서

작성일: 2026-06-09  
전제: KRDS Figma Community 프로필과 공식 Figma Library v1.0.0을 참조해 작업한다.  
목적: 역기획서를 Figma 파일 안에서 실제 페이지, 프레임, 컴포넌트, 변수, QA 구조로 재현하기 위한 제작 지시서.

## 1. 작업 방식

### 1.1 시작 파일

1. Figma Community에서 KRDS 프로필을 연다: https://www.figma.com/@krds
2. KRDS Figma Library v1.0.0 또는 최신 공개 라이브러리를 복제한다.
3. Pretendard GOV 서체를 설치한다.
4. 복제 파일에서 스타일 가이드, 컴포넌트, 패턴, 아이콘 페이지와 Local Variables를 확인한다.
5. 별도 작업 파일을 만들 경우 KRDS 라이브러리를 publish한 뒤 Assets 패널에서 add to file로 추가한다.

### 1.2 산출 방식

권장 산출물:

- `KRDS Reverse Planning` 파일
- `00 Cover`
- `01 Product Brief`
- `02 IA & User Flows`
- `03 Screen Requirements`
- `04 Component Requirements`
- `05 Figma Library Mapping`
- `06 Design Token Mapping`
- `07 Accessibility QA`
- `08 Open Issues`

KRDS 원본 라이브러리의 컴포넌트는 detach하지 않는다. 화면 요구사항 프레임은 instance 조합으로 구성하고, 필요한 경우만 wrapper frame을 만든다.

## 2. 페이지와 프레임 구조

| Page | Frame | Size | 목적 |
|---|---:|---:|---|
| 00 Cover | `Cover / KRDS Reverse Planning` | 1440x1024 | 문서 표지와 범위 |
| 01 Product Brief | `Project Overview` | 1440x1600 | 목표, 사용자, 범위 |
| 01 Product Brief | `Evidence Board` | 1440x1600 | 공식 사이트/GitHub/Figma 근거 |
| 02 IA & User Flows | `Information Architecture` | 1440x1800 | 1차/2차 메뉴 구조 |
| 02 IA & User Flows | `Designer Journey` | 1440x1200 | 디자이너 온보딩 흐름 |
| 02 IA & User Flows | `Developer Journey` | 1440x1200 | 개발자 온보딩 흐름 |
| 02 IA & User Flows | `Government Journey` | 1440x1200 | 정부 관계자 검수 흐름 |
| 03 Screen Requirements | `Common Shell / Desktop` | 1440x1800 | 공통 헤더/푸터/탐색 구조 |
| 03 Screen Requirements | `Common Shell / Mobile` | 390x1600 | 모바일 공통 구조 |
| 03 Screen Requirements | `Main Page / Desktop` | 1440x2400 | 메인 페이지 요구사항 |
| 03 Screen Requirements | `Search Overlay` | 1440x1200 | 통합검색 상태 |
| 03 Screen Requirements | `Display Settings` | 1440x1200 | 글자·화면 설정 상태 |
| 03 Screen Requirements | `Component List` | 1440x1800 | 검색/필터/목록 |
| 03 Screen Requirements | `Component Detail Template` | 1440x2200 | 상세 문서 템플릿 |
| 03 Screen Requirements | `Pattern Detail Template` | 1440x2200 | 기본/서비스 패턴 템플릿 |
| 04 Component Requirements | `Component Category Matrix` | 1440x2400 | 카테고리별 요구사항 |
| 04 Component Requirements | `State Matrix` | 1440x1600 | 상태/모드/반응형 기준 |
| 04 Component Requirements | `Accessibility Matrix` | 1440x2000 | 컴포넌트별 접근성 |
| 05 Figma Library Mapping | `Library Page Map` | 1440x1400 | KRDS 원본 라이브러리 매핑 |
| 05 Figma Library Mapping | `Property Naming Rules` | 1440x1600 | variant/property 규칙 |
| 06 Design Token Mapping | `Token Flow` | 1440x1400 | Figma JSON to CSS variable 흐름 |
| 06 Design Token Mapping | `Variable Collections` | 1440x1800 | primitive/semantic/mode/responsive |
| 07 Accessibility QA | `KWCAG/WCAG Checklist` | 1440x2400 | 접근성 QA |
| 08 Open Issues | `Public Source Gaps` | 1440x1200 | 공개자료 불일치/추정 항목 |

## 3. 디자인 토큰 설정

### 3.1 Variable collection

KRDS 공식 설명 기준으로 다음 collection을 확인한다.

- `primitive`: color, typo, number
- `semantic`: gap, padding, size-height, radius
- `mode`: color, border-width, shadow
- `responsive`: typo, layout-gap, card-padding

### 3.2 Mode

필수 mode:

- `light`
- `high-contrast`
- `large`
- `small`

작업 원칙:

- Primitive는 원시값이므로 직접 UI 프레임에 연결하지 않는다.
- 화면 프레임은 semantic/mode/responsive 변수를 우선 사용한다.
- 컴포넌트 token은 개발 코드에서 정의하므로 Figma 화면에는 component token을 새로 만들지 않는다.
- 기관 확장을 가정한 컬러 변경은 primitive color만 변경한 뒤 semantic 참조가 유지되는지 확인한다.

### 3.3 토큰 매핑 표기

각 주요 화면 프레임 오른쪽에 `Token Notes` 섹션을 둔다.

예시:

| UI 대상 | Figma variable | CSS variable 예시 | 비고 |
|---|---|---|---|
| 페이지 배경 | mode/color/background/basic | `--krds-color-background-basic` | light/high-contrast 전환 |
| 본문 텍스트 | mode/color/text/basic | `--krds-color-text-basic` | 대비 검수 |
| 주요 CTA | mode/color/action/primary | `--krds-color-action-primary` | semantic 기준 |
| 카드 간격 | responsive/layout-gap/medium | `--krds-layout-gap-medium` | large/small 전환 |
| 컴포넌트 높이 | semantic/size-height/medium | `--krds-size-height-medium` | 버튼/입력 공통 |

## 4. 오토레이아웃과 반응형

### 4.1 기본 프레임

Desktop:

- Frame width: 1440
- Content max width: 1280
- Outer margin: 80
- Section gap: token 기반
- Header: full width
- Side navigation: 240-280 권장
- Main content: flexible

Mobile:

- Frame width: 390 또는 375
- Outer margin: 20
- Header: compact
- GNB: drawer 또는 full menu
- Side navigation: accordion 또는 in-page navigation
- Bottom interaction: mobile component 사용 가능

### 4.2 Auto Layout 규칙

- 같은 역할의 컴포넌트는 같은 padding, gap, alignment를 사용한다.
- 텍스트가 길어지는 문서형 UI는 fixed height를 피한다.
- 버튼/입력/태그/배지는 hug contents 또는 min width를 사용한다.
- 카드형 목록은 grid frame 안에서 동일한 row height를 강제하지 말고, 텍스트 overflow 검수 후 필요한 경우 description line clamp를 정의한다.
- 모바일에서는 2열 이상의 복잡한 정보표현을 단일열 또는 horizontal scroll table로 전환한다.

## 5. 컴포넌트 Property 규칙

### 5.1 공통 property

| Property | 값 | 설명 |
|---|---|---|
| Type | primary, secondary, tertiary, danger, text | 역할과 중요도 |
| Size | xsmall, small, medium, large, xlarge | 크기 |
| State | enabled, hover, pressed, focus, disabled, error, success | 상호작용 상태 |
| Icon | none, leading, trailing, only | 아이콘 위치 |
| Mode | light, high-contrast | 표시 모드 |
| Responsive | large, small | 반응형 |
| Platform | web, mobile | 플랫폼 |

### 5.2 입력 property

| Property | 값 | 설명 |
|---|---|---|
| Required | true, false | 필수 입력 |
| Value | empty, filled | 입력값 존재 |
| Help text | true, false | 도움말 노출 |
| Error | true, false | 오류 상태 |
| Readonly | true, false | 읽기 전용 |
| Disabled | true, false | 비활성 |

### 5.3 탐색 property

| Property | 값 | 설명 |
|---|---|---|
| Selected | true, false | 현재 선택 |
| Current | true, false | 현재 위치 |
| Expanded | true, false | 펼침 |
| Depth | 1, 2, 3 | 메뉴 계층 |
| Orientation | horizontal, vertical | 방향 |

## 6. 화면별 Figma 프레임 사양

### 6.1 Common Shell / Desktop

포함 instance:

- Masthead
- Skip link
- Header
- Main menu
- Search trigger
- Full menu trigger
- Language switcher
- Resize/Display setting
- Breadcrumb
- Side navigation
- In-page navigation
- Footer

Annotation:

- Header는 모든 페이지에 일관 배치
- 검색/전체메뉴/글자·화면 설정은 overlay state frame 별도 작성
- 현재 메뉴는 selected/current 상태로 표기
- 본문 영역은 h1, intro, section, content module 구조 유지

### 6.2 Main Page / Desktop

포함 섹션:

- Hero: `모두를 위한 디지털 서비스 경험`
- Role start: Designer / Developer / Government
- Key composition: Principles / Inclusion / Style / Components / Basic Pattern / Service Pattern
- Case studies
- FAQ
- Feedback CTA

Annotation:

- 첫 화면에서 목적, 대상, 시작 액션이 모두 보여야 한다.
- 역할 카드에는 튜토리얼, 리소스, 토큰/코드 등의 하위 액션을 둔다.
- 적용 사례는 작은 카드보다 증거성 있는 목록/요약 형태가 더 적합하다.

### 6.3 Search Overlay

상태 프레임:

- default
- typing
- results
- no results
- keyboard focus

필수 annotation:

- focus entry: input
- close: button, Esc, outside click
- result item: title, type, path, snippet
- no result: 철자 확인, 단어 분리, 일반 단어 안내

### 6.4 Display Settings

상태 프레임:

- default selected
- font size changed
- high-contrast selected
- system setting selected

필수 annotation:

- 5단계 글자 크기
- 기본/선명/시스템 설정
- 초기화
- 닫기
- local storage 또는 session persistence 권장

### 6.5 Component List

구성:

- Page title
- 설명
- Search input
- Type filter chips 또는 segmented controls
- Count
- Component list
- No result state

Annotation:

- 한글명, 영문명, 설명, 유형을 한 행에서 스캔 가능하게 한다.
- 카드는 과하면 정보 밀도가 낮아질 수 있으므로 문서형 목록을 우선한다.
- 필터 선택 상태는 텍스트와 시각 단서 모두로 표시한다.

### 6.6 Component Detail Template

구성:

- Title: `Button (버튼)`
- Summary
- When to use
- When not to use
- Anatomy
- Variants
- Sizes
- States
- Interaction
- Accessibility
- Content guidelines
- Responsive
- Figma properties
- Code
- Related patterns

Annotation:

- 상태표는 Figma property와 code class를 함께 보여준다.
- 접근성 영역은 label, role, state, keyboard, focus를 분리한다.
- 예시는 light/high-contrast와 desktop/mobile을 최소 1개씩 포함한다.

## 7. 컴포넌트 카테고리 매핑

| Category | Components | Figma 작업 기준 |
|---|---|---|
| Identity | Masthead, Identifier, Header, Footer | 공공성, 운영 주체, 브랜드 신뢰 |
| Navigation | Skip link, Main menu, Breadcrumb, Side navigation, In-page navigation, Pagination, Link, Back button, Tab bars | 현재 위치와 이동 경로 |
| Layout & Display | Structured list, Critical alerts, Calendar, Disclosure, Modal, Badge, Accordion, Image, Carousel, Tab, Table, Text list, Favicon | 정보 구조화와 집중 |
| Action | Button, FAB | 실행과 상태 변경 |
| Selection | Radio button, Checkbox, Select, Tag, Toggle switch, Range slider, Quantity toggle | 선택과 값 조정 |
| Feedback | Step indicator, Spinner, Toast, Snackbar | 진행/결과 피드백 |
| Help | Help panel, Tutorial panel, Contextual help, Coach mark, Tooltip, TTS | 보조 설명과 안내 |
| Input | Date input, Textarea, Text input, File upload | 데이터 입력 |
| Settings | Language switcher, Resize | 사용자 표시 환경 설정 |
| Content | Accessible multimedia, Visually hidden | 접근 가능한 콘텐츠 |
| Mobile | Bottom sheet, Splash screen | 모바일 전용 과업 |

## 8. 접근성 QA 프레임

### 8.1 공통 체크리스트

- Focus order가 시각 순서와 일치한다.
- 모든 interactive element에 접근 가능한 이름이 있다.
- 현재 위치, 선택, 펼침 상태가 보조기술에 전달된다.
- 오류 메시지가 필드와 연결된다.
- 색상만으로 상태를 전달하지 않는다.
- 자동 재생 또는 시간 제한에는 조절 수단이 있다.
- high-contrast mode에서 주요 텍스트와 UI 경계가 충분히 구분된다.
- large font mode에서 텍스트가 겹치거나 잘리지 않는다.

### 8.2 컴포넌트별 QA annotation

각 컴포넌트 프레임 오른쪽에 다음 블록을 둔다.

```text
Accessibility QA
- Role:
- Name:
- State:
- Keyboard:
- Focus:
- Screen reader note:
- High-contrast check:
- Responsive check:
```

## 9. 오픈 이슈

| 이슈 | 내용 | 처리 |
|---|---|---|
| 컴포넌트 수 차이 | 웹 컴포넌트 목록은 37건, 디자이너 가이드는 Figma 43종 표기 | Figma 원본 라이브러리에서 실제 asset count 확인 필요 |
| Figma 직접 생성 불가 | 현재 작업 환경에서 Figma 파일 업로드/생성 커넥터 없음 | 본 사양서로 수동 재현 또는 Figma MCP/Plugin 환경에서 자동화 |
| 내부 KPI 부재 | 공개 자료만으로 실제 목표 수치 확인 불가 | 제안 KPI로 분리 |
| 기관별 확장 범위 | 실제 기관 브랜딩 정책은 별도 확인 필요 | 표준형/확장형 토큰 정책으로 관리 |

## 10. 최종 검수 기준

- KRDS 원본 라이브러리 instance를 유지한다.
- 화면 프레임은 Desktop과 Mobile을 최소 한 벌씩 포함한다.
- 모든 주요 화면은 light/high-contrast 모드 검수 annotation을 가진다.
- 모든 입력/선택/탐색 컴포넌트는 focus 상태를 가진다.
- 디자인 토큰 흐름이 Figma variable에서 CSS variable까지 이어진다.
- component property명이 문서/개발 상태명과 대응된다.
- 공개자료 기반 추정 항목은 `Open Issues`에 남긴다.
