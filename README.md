# ⚡ Smart Device Manager (스마트 가전 기기 관리 서비스)

스마트 가전 기기의 정보, 구매 내역, 무상 보증기간 및 작동 상태를 효율적으로 관리하기 위한 CRUD Frontend Service입니다.

---

## 1. Service Topic
* **서비스 주제:** 스마트 가전 기기 관리 서비스 (Smart Device Manager)
* **목적:** 가전 기기 및 IT 디바이스의 구매일, 가격, 무상 보증기간, 기기 상태 등을 한눈에 확인하고 통합 관리할 수 있는 웹 서비스

---

## 2. Data Fields
본 서비스는 총 **7개의 데이터 Field**로 구성되어 있습니다.

1. **ID (기기 식별 번호):** 레코드를 식별하기 위한 고유한 숫자값
2. **기기명 (Device Name):** 제품의 명칭 (예: LG 오브제 스탠드 청소기)
3. **카테고리 (Category):** 가전 분류 (주방가전 / 생활가전 / IT·음향 / 계절가전)
4. **구매 가격 (Price):** 제품 구매 시 결제 금액 (원 단위)
5. **구매일자 (Purchase Date):** 제품을 구매한 날짜 (YYYY-MM-DD)
6. **무상 보증기간 (Warranty):** 제공되는 A/S 무상 보증 기간 (1년 / 2년 / 3년 / 5년)
7. **상태 (Status):** 현재 기기의 작동/관리 상태 (정상 작동 / 수리 필요 / 폐기·교체)

---

## 3. List Page (`index.html`)
메인 목록 페이지에서는 전체 7개 필드 중 아래 **5개 Field**를 테이블 형태로 한눈에 확인할 수 있도록 구성하였습니다.

* **표시 Field:** `ID` / `기기명` / `카테고리` / `구매가격` / `상태`
* **주요 기능:**
  * 상단 `+ 기기 등록 (Add)` 버튼 클릭 시 `add.html`로 이동
  * 테이블 내 `상세보기` 버튼 클릭 시 해당 레코드의 `view.html`로 이동

---

## 4. Validation
`add.html` (추가) 및 `edit.html` (수정) 폼에 적용된 JavaScript 유효성 검사 규칙 4가지입니다.

1. **필수값 입력 및 문자열 길이 검증 (`기기명`):**
   * 기기명이 빈값이거나 **2자 미만**으로 입력되었을 경우 경고창을 띄우고 제출을 방지합니다.
2. **Select 선택 여부 검증 (`카테고리`, `보증기간`):**
   * 카테고리와 무상 보증기간의 드롭다운(Select) 옵션이 선택되지 않고 기본값으로 남아 있을 경우 알림을 표시합니다.
3. **숫자 범위 검증:**
   * 가격 필드가 비어있거나 **10,000원 미만**의 값이 입력되었을 때 올바른 금액을 입력하도록 유도합니다.
4. **날짜 입력 여부 검증:**
   * Date Input 필드에 구매일자가 정확히 선택/입력되었는지 확인합니다.

---

## 5. RWD (Responsive Web Design / 반응형 웹)
`my.css`를 통해 디바이스 스크린 크기에 따라 레이아웃이 유연하게 반응하도록 설정했습니다.

* **Desktop 환경:**
  * `.container`의 `max-width: 900px`와 중앙 정렬을 지정하여 시각적인 가독성을 확보했습니다.
  * 테이블(`table`) 형태 데이터 뷰 및 버튼 그룹을 가로로 배열하였습니다.
* **Mobile 환경:**
  * `meta name="viewport" content="width=device-width, initial-scale=1.0"` 설정 및 `%` 기반 가변 레이아웃을 사용했습니다.
  * `.table-container` 영역에 `overflow-x: auto` 속성을 부여하여 스크린이 좁아지더라도 데이터 표가 깨지지 않고 좌우 스크롤로 모든 항목을 조회할 수 있도록 구현했습니다.
  * Input 폼 및 버튼 요소가 모바일 터치 영역에 최적화되도록 전체 너비(`width: 100%`)와 충분한 패딩(`padding: 10px 12px`)을 적용했습니다.

---

## 6. Bootstrap
*본 프로젝트는 프레임워크 없이 pure CSS(`my.css`)를 사용하여 Bootstrap 스타일 디자인 시스템을 직관적으로 재현하였습니다.*

* **Layout & Container:** Bootstrap의 `.container`, `.card` 구조를 차용하여 유연한 반응형 카드를 배치
* **Form & Input:** `.form-group`, `input[type="..."]`, `select`에 Focus 시 outline 스타일링 적용
* **Button System:** `.btn`, `.btn-primary`, `.btn-danger`, `.btn-secondary` 등 역할에 따른 컬러 시스템 적용
* **Table System:** `.table-container` 및 Hover 효과(`tr:hover`)가 포함된 스트라이프 형태 테이블 스타일링

---

## 7. Problem & Solution
* **문제점:** 모바일 해상도로 접속 시 테이블 내 필드가 많아 오른쪽 내용이 잘리거나 레이아웃이 깨지는 현상이 발생함.
* **해결 방법:** 테이블을 감싸는 div 태그에 `.table-container` 클래스를 지정하고 CSS에 `overflow-x: auto;`를 적용하여 수평 스크롤을 활성화함으로써 모바일 가독성을 확보함.

---

## 8. Reflection
* **새롭게 알게 된 점:** 
  * HTML5 기본 Form 입력 요소들과 JavaScript의 DOM 조작, Event 처리를 연결하여 프론트엔드 차원의 유효성 검사를 구현하는 메커니즘을 명확히 이해하게 되었습니다.
  * 공통 CSS 스타일시트를 별도로 분리하여 관리함으로써 여러 페이지간 디자인 일관성을 지키고 코드 재사용성을 높이는 라이브러리 방식 작성 기법을 익혔습니다.
* **궁금한 점:**
  * 현재는 폼 데이터가 페이지 전환 시 실제 데이터베이스(DB)나 LocalStorage에 저장되지 않고 정적 레코드로 표시되는데, 차후 JavaScript의 `localStorage` API나 `JSON Server`를 연동하여 실제 데이터를 생성이나 수정 혹은 삭제하는 동적 상태 관리법을 더 다뤄보고 싶습니다.