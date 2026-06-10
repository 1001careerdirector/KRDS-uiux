# KRDS 화면설계 Figma 이관 명세서

작성일: 2026.06.10  
기준 산출물: `krds_screen_design_description.html`, `krds_screen_design_deck.pptx`  
기준 자료: KRDS 공식 웹사이트, KRDS-uiux GitHub, Figma `@krds` Community 공개 자료

## 1. 이관 목적

KRDS 화면설계 산출물을 Figma에서 검토, 수정, 핸드오프할 수 있도록 페이지 구조, 프레임 네이밍, 컴포넌트 속성, 디자인 토큰, Description 콜아웃 체계를 정렬한다.

본 문서는 실제 Figma 파일 생성 전 단계의 작업 명세이며, 공개자료 기반 역기획이므로 확정되지 않은 정책은 `추정` 또는 `검토 필요`로 표시한다.

## 2. 권장 파일 구조

| Page | Section / Frame | 목적 | 포함 내용 |
|---|---|---|---|
| `00_Cover` | `Project Overview` | 문서 기본 정보 관리 | 표지, 출처, 버전, 작성자, 주의사항 |
| `01_History` | `Revision History` | 변경 이력 관리 | 버전, 날짜, 변경 유형, 페이지, 내용, 비고 |
| `02_Workflow` | `Role Flow` | 사용자 흐름 정의 | 방문, 탐색, 조회, 적용, 검수 단계 |
| `03_PC` | `PC_Main_List` | PC 메인 화면설계 | 메타 테이블, 와이어프레임, 콜아웃, Description |
| `03_PC` | `PC_Component_Detail` | 컴포넌트 상세 화면설계 | 탐색, 미리보기, 상세 정의, 코드 연결 |
| `04_Mobile` | `Mobile_SMS_Notify` | 모바일 수신 화면설계 | SMS 화면, 상태 메시지, 접근성 기준 |
| `05_Components` | `Component_Matrix` | 공통 컴포넌트 정의 | 상태, 속성, 접근성, 개발 연동 키 |
| `06_Handoff` | `QA_Checklist` | 개발/검수 전달 | 완료 기준, 예외 케이스, 산출물 체크 |

## 3. 프레임 네이밍 규칙

| 유형 | 규칙 | 예시 |
|---|---|---|
| 화면 | `screen/{device}/{page-purpose}` | `screen/pc/main-list` |
| 컴포넌트 | `component/{category}/{name}` | `component/action/button` |
| 상태 | `{component}/{state}` | `button/primary/focus` |
| 패턴 | `pattern/{flow}/{name}` | `pattern/search/filter-panel` |
| 설명 패널 | `description/{screen-id}` | `description/pc-main-list` |
| 콜아웃 | `callout/{screen-id}/{number}` | `callout/pc-main-list/01` |

## 4. 화면별 이관 항목

### 4.1 PC 메인/리스트

| 번호 | 항목 | Figma 요소 | Description 기준 |
|---|---|---|---|
| 1 | 탭형 입력 영역 | `Tabs / Segment Control` | 분류 전환, 선택 상태, 비활성 상태, 키보드 이동 |
| 2 | 검색/필터 영역 | `Search Field`, `Select` | 검색어 입력, 필터 선택, 초기화, focus-visible |
| 3 | 데이터 테이블 | `Data Table` | 정렬, 행 선택, 빈 데이터, 로딩, 페이지네이션 |
| 4 | 배너/이미지 슬롯 | `Media Card`, `Carousel` | 대체텍스트, 이미지 미등록, 업로드 오류 |
| 5 | 하단 액션 | `Button Group` | 저장, 취소, 확인, 비활성, 로딩, 완료 피드백 |

### 4.2 PC 컴포넌트 상세

| 번호 | 항목 | Figma 요소 | Description 기준 |
|---|---|---|---|
| 1 | 컴포넌트 그룹 탐색 | `Side Navigation`, `Tabs` | 카테고리, 검색 조건 유지, 현재 위치 표시 |
| 2 | 상태별 미리보기 | `Variant Preview` | default, hover, pressed, focus, disabled, error |
| 3 | 상세 정의 | `Spec Panel` | 정의, 사용 시점, 금지 사례, 구성 요소, 변형 규칙 |
| 4 | Figma/Code 연결 | `Handoff Table` | property, CSS class, JS behavior, ARIA 연결 |
| 5 | 검수 기준 | `QA Checklist` | 반응형, 접근성, 키보드, 오류 메시지 |

### 4.3 Mobile 알림/수신

| 번호 | 항목 | Figma 요소 | Description 기준 |
|---|---|---|---|
| 1 | 모바일 수신 화면 | `Mobile Frame` | 제목, 본문, 안내문, 실제 수신 채널 표현 |
| 2 | 내용 자동 높이 | `Auto Layout Text Block` | 긴 문구 줄바꿈, 최대 높이, 스크롤 정책 |
| 3 | 상태 메시지 | `Status Message` | 성공, 실패, 예약, 수신 거부 |
| 4 | 접근성 | `A11y Note` | 낭독 순서, 대비, 터치 영역, 확대 대응 |

## 5. 컴포넌트 속성 정의

| 컴포넌트 | Figma Properties | 상태 | 개발 키 |
|---|---|---|---|
| Button | `type`, `size`, `state`, `icon`, `width` | default, hover, pressed, focus, disabled, loading | `variant`, `size`, `disabled`, `isLoading` |
| Text Input | `type`, `state`, `required`, `helperText` | default, focus, filled, error, disabled, readonly | `value`, `errorText`, `required`, `readOnly` |
| Select | `state`, `open`, `selected`, `disabled` | default, expanded, selected, error, disabled | `selectedValue`, `isOpen`, `onChange` |
| Tabs | `selected`, `size`, `fill`, `state` | selected, focus, hover, disabled | `activeKey`, `onTabChange` |
| Table | `density`, `sortable`, `selected`, `empty` | default, sorted, selected, loading, empty | `columns`, `rows`, `sortKey`, `page` |
| Modal | `size`, `type`, `open`, `buttonType` | open, confirm, cancel, error, loading | `open`, `onConfirm`, `onClose` |
| Toast / Alert | `type`, `duration`, `action` | info, success, warning, error | `type`, `message`, `duration` |
| Carousel | `itemCount`, `state`, `control` | loaded, empty, error, autoplay, paused | `items`, `activeIndex`, `onNext` |

## 6. 디자인 토큰 매핑

| Token Group | 권장 토큰 | 설명 |
|---|---|---|
| Color | `color.primary`, `color.text`, `color.border`, `color.surface`, `color.feedback.*` | 브랜드, 본문, 라인, 배경, 상태색 |
| Typography | `font.family`, `font.size.*`, `font.weight.*`, `line.height.*` | 한글 가독성과 공공 서비스 문서 톤 유지 |
| Spacing | `space.4`, `space.8`, `space.12`, `space.16`, `space.24`, `space.32` | 컴포넌트 내부 여백과 섹션 간격 |
| Radius | `radius.0`, `radius.2`, `radius.4`, `radius.8` | 공공 서비스 UI 특성상 과도한 라운드 금지 |
| Elevation | `shadow.modal`, `shadow.dropdown`, `shadow.toast` | 레이어 구분, 포커스 유지 |
| Motion | `motion.fast`, `motion.normal`, `motion.reduce` | 드롭다운, 토스트, 모달 등장/해제 |

## 7. 접근성 체크

| 항목 | 기준 |
|---|---|
| 키보드 이동 | Tab 순서가 시각적 순서와 일치해야 한다. |
| 포커스 표시 | `focus-visible` 상태는 모든 인터랙티브 컴포넌트에 제공한다. |
| 명도 대비 | 본문/버튼/상태 메시지는 최소 4.5:1 기준을 검토한다. |
| 레이블 연결 | 입력 필드는 label, description, error message가 연결되어야 한다. |
| 모달 | 열림 시 focus trap, 닫힘 후 원래 트리거로 focus 복귀가 필요하다. |
| 알림 | 토스트/오류/성공 메시지는 screen reader가 인지할 수 있어야 한다. |
| 이미지 | 배너/카드/아이콘은 의미에 따라 alt text 또는 decorative 처리한다. |

## 8. 개발 핸드오프 기준

| 구분 | 전달 항목 |
|---|---|
| 화면 | 화면 ID, 페이지 코드, 상태별 화면, 반응형 기준 |
| 컴포넌트 | props, state, variant, event, accessibility attributes |
| 문구 | 기본 문구, 오류 문구, 빈 데이터 문구, 보조 설명 |
| 데이터 | 필드명, 정렬 키, 필터 키, pagination 정책 |
| 상태 | loading, empty, error, success, disabled, readonly |
| QA | 키보드, 스크린리더, 확대, 모바일, 저속 네트워크 |

## 9. Figma 작업 순서

1. `00_Cover`에 프로젝트 기본 정보와 기준 자료 링크를 등록한다.
2. `01_History`에 변경 이력 표를 만든다.
3. `02_Workflow`에 방문부터 검수까지의 흐름을 배치한다.
4. `03_PC`, `04_Mobile`에 화면 프레임을 만들고 콜아웃 번호를 고정한다.
5. 우측 Description 패널을 컴포넌트화해 화면별로 재사용한다.
6. `05_Components`에서 공통 컴포넌트 variant와 state를 정의한다.
7. `06_Handoff`에서 개발/QA 체크리스트를 정리한다.
8. 실제 KRDS Figma 파일 node ID와 연결 가능한 경우, 각 화면/컴포넌트에 링크를 추가한다.

## 10. 완료 기준

- 화면 프레임과 Description 번호가 1:1로 연결되어 있다.
- PC, Mobile, Component Detail 화면이 각각 독립 검토 가능하다.
- 컴포넌트별 상태와 접근성 요구사항이 누락되지 않았다.
- Figma property와 개발 props/key가 같은 의미 체계로 정리되어 있다.
- PDF/PPT/HTML 산출물과 Figma 구조가 동일한 목차를 공유한다.
