# 김비서 대시보드 프로젝트

> Claude Code 워크숍 실습 결과물 (2026-05-06)  
> GitHub: https://github.com/hellovr-dev/secretary-test  
> GitHub Pages: https://hellovr-dev.github.io/secretary-test/dashboard.html

---

## 📁 프로젝트 구조

```
워크숍-실습/
├── dashboard.html          # 메인 대시보드
├── chart.html              # 매출 현황 차트
├── diagram.html            # 업무 프로세스 다이어그램 (HTML 래퍼)
├── diagram.svg             # 업무 프로세스 다이어그램 (SVG 원본)
├── report.html             # 사이트 분석 보고서
├── 김비서-데이터/
│   ├── 매출데이터.csv
│   ├── 업무목록.csv
│   ├── 주간일정.txt
│   ├── 프로젝트현황.csv
│   └── 회의록.txt
└── 정리해줘/
    ├── 보고서/             # 보고서_초안, 수정, 최종 등
    ├── 메모/               # 기획_메모, 아이디어_메모 등
    ├── 업무/               # 할일, 피드백, 영수증_정리 등
    └── 기타/               # temp.csv, 링크모음 등
```

---

## 🗂️ 오늘 작업 내역

### 1. 데이터 읽기 & 대시보드 생성 (`dashboard.html`)
- `김비서-데이터/` 폴더의 5개 파일 전체 분석
- **4개 섹션** 구성:
  - ✅ **할 일 목록** — 체크박스, 우선순위 배지(높음/보통/낮음/완료)
  - 📅 **이번 주 일정** — 월~금 일정표, 클로드 워크숍 강조
  - 📊 **프로젝트 진행률** — 프로그레스 바 6개, 예산 집행 현황
  - 💰 **매출 요약** — 누적 총매출, 월별, 카테고리별, 제품별 비중 차트

### 2. 프리미엄 디자인 업그레이드 (`dashboard.html`)
- **글래스모피즘**: `backdrop-filter: blur(24px)` + 반투명 테두리
- **그라디언트 배경**: 3레이어 방사형 그라디언트 + 12초 애니메이션
- **배경 오브(orb)**: 블러 처리된 컬러 장식 오브 3개
- **다크/라이트 모드 토글**: 우측 상단 슬라이드 스위치
  - `localStorage`에 테마 저장 (재방문 시 유지)
  - 다크: 배경 `#0f0f23`, 카드 `rgba(255,255,255,0.06)`, 텍스트 `#e0e0e0`
  - 라이트: 배경 `#667eea~#764ba2` 그라디언트, 카드 `rgba(255,255,255,0.72)`

### 3. 파일 자동 분류 (`정리해줘/`)
- 15개 파일을 용도별 4개 폴더로 자동 분류 (PowerShell)
- 보고서 4개 / 메모 4개 / 업무 4개 / 기타 3개

### 4. 매출 차트 (`chart.html`)
- **외부 라이브러리 없이** 순수 Canvas API로 구현
- **월별 매출 추이**: 선 그래프 (1월 4,649만 → 2월 2,450만)
- **제품별 매출 비교**: 전자기기(파란)/생활용품(초록) 묶음 막대 그래프
- **통계 카드**: 누적 총매출 · 월 평균 · 최고 판매 제품
- HiDPI 지원, 창 크기 변경 시 자동 재렌더링

### 5. 업무 프로세스 다이어그램 (`diagram.svg` / `diagram.html`)
- SVG로 5단계 가로 플로우 다이어그램
- 단계: **기획 → 제작 → 검토 → 배포 → 분석**
- 파스텔 5색 (블루/그린/퍼플/오렌지/핑크), 둥근 사각형, 화살표
- `diagram.html`: 네비게이션 포함 SVG 래퍼 페이지

### 6. 사이트 분석 보고서 (`report.html`)
- 대상: https://www.subtrac.kr (구독 관리 SaaS)
- 항목별 카드 레이아웃: 사이트 개요 / 구조 / 디자인 / 기능 / 잘한점 / 개선점 / 종합평가

### 7. 공통 네비게이션 메뉴
- 모든 HTML 파일에 동일한 네비게이션 추가
- `position: sticky; top: 0` — 스크롤해도 항상 상단 고정
- 현재 페이지 자동 강조 (`location.pathname` 기반)
- 메뉴 항목: 📊 대시보드 / 📈 매출 현황 / 🔄 업무 프로세스 / 📋 사이트 분석

### 8. GitHub 연동
- `git init` → remote 추가 → 커밋 → 푸시
- Classic PAT 사용 (Fine-grained token은 조직 레포 접근 제한)
- `.env` 파일로 토큰 로컬 관리 (`.gitignore`로 푸시 제외)

---

## 🎨 디자인 시스템

### 색상
| 용도 | 라이트 | 다크 |
|------|--------|------|
| 배경 | `#667eea → #764ba2` | `#0f0f23` |
| 카드 | `rgba(255,255,255,0.72)` | `rgba(255,255,255,0.06)` |
| 텍스트 | `#1a1a2e` | `#e0e0e0` |
| 강조 | `#4f6ef7` | `#7c9fff` |

### 카드 스타일 (글래스모피즘)
```css
background: var(--glass-bg);
border: 1px solid var(--glass-border);
border-radius: 20px;
backdrop-filter: blur(24px) saturate(160%);
box-shadow: 0 8px 40px rgba(0,0,0,0.55);
```

### 공통 네비게이션 CSS (비대시보드 페이지용)
```css
.site-nav { position: sticky; top: 0; z-index: 999;
  background: rgba(15,15,35,0.88);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,255,255,0.1); }
.site-nav ul { display: flex; list-style: none; max-width: 1320px; margin: 0 auto; padding: 0 32px; }
.site-nav li { flex: 1; }
.site-nav a { display: block; padding: 14px 20px; text-align: center;
  color: rgba(255,255,255,0.6); text-decoration: none;
  font-size: 0.88rem; font-weight: 600;
  border-bottom: 3px solid transparent; }
.site-nav a.active { color: #7c9fff; border-bottom-color: #7c9fff; }
```

### 네비게이션 활성화 JS (공통)
```js
(function() {
  var page = location.pathname.split('/').pop() || 'dashboard.html';
  document.querySelectorAll('.site-nav a').forEach(function(a) {
    if (a.getAttribute('href') === page) a.classList.add('active');
  });
})();
```

---

## ⚙️ 기술 스택

| 항목 | 내용 |
|------|------|
| 언어 | 순수 HTML + CSS + JavaScript (외부 라이브러리 없음) |
| 차트 | Canvas API (chart.html) |
| 다이어그램 | SVG |
| 테마 | CSS 변수(`--var`) + `data-theme` 속성 |
| 저장 | `localStorage` (테마 설정) |
| 배포 | GitHub Pages |

---

## 🔧 새 작업 요청 시 참고사항

### 새 HTML 페이지 추가할 때
1. 위 공통 네비게이션 CSS + HTML + JS 스니펫 삽입
2. `<body>` 직후 `<nav class="site-nav">` 추가
3. `body { padding: 0 20px; }` (padding-top 제거)
4. 메인 컨테이너에 `padding-top: 36px` 추가
5. **모든 기존 파일**의 nav에도 새 메뉴 항목 추가

### 네비게이션 메뉴 항목 (현재)
```html
<nav class="site-nav">
  <ul>
    <li><a href="dashboard.html">📊 대시보드</a></li>
    <li><a href="chart.html">📈 매출 현황</a></li>
    <li><a href="diagram.html">🔄 업무 프로세스</a></li>
    <li><a href="report.html">📋 사이트 분석</a></li>
  </ul>
</nav>
```

### GitHub 푸시 절차
```bash
# 변경 파일 스테이징
git add 파일명

# 커밋
git commit -m "커밋 메시지"

# 푸시 (토큰은 .env 파일 참고)
git remote set-url origin https://{GITHUB_TOKEN}@github.com/hellovr-dev/secretary-test.git
git push origin master
```

### 데이터 파일 위치
| 파일 | 내용 |
|------|------|
| `김비서-데이터/매출데이터.csv` | 날짜/제품/카테고리/수량/단가/매출액/지역 |
| `김비서-데이터/업무목록.csv` | 업무/우선순위/상태/담당자/마감일/카테고리 |
| `김비서-데이터/주간일정.txt` | 2026년 3월 10일~14일 일정 |
| `김비서-데이터/프로젝트현황.csv` | 프로젝트명/진행률/상태/담당자/예산/집행 |
| `김비서-데이터/회의록.txt` | 회의 내용 |

---

## 📌 매출 데이터 집계 (사전 계산값)

| 항목 | 금액 |
|------|------|
| 누적 총매출 | 71,006,000원 |
| 1월 매출 | 46,499,000원 |
| 2월 매출 (일부) | 24,507,000원 |
| 전자기기 | 53,316,000원 (75.1%) |
| 생활용품 | 17,690,000원 (24.9%) |
| 무선 이어폰 | 28,836,000원 |
| 블루투스 스피커 | 9,600,000원 |
| 보조배터리 | 9,030,000원 |
| 무선 충전기 | 5,850,000원 |
| 텀블러 | 11,525,000원 |
| 에코백 | 6,165,000원 |
