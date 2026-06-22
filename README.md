# All About AMHS

SK하이닉스 IT(AMHS) 직무 지원을 위한 **자동반송시스템(AMHS) 학습·시뮬레이션 정적 웹 앱**입니다.
여러 Claude 도구를 조합해 *데이터 수집 → 정리 → 개발 → 검증 → 배포*의 전 사이클을 자율 실행했습니다.

> 🔗 배포 URL: `https://<username>.github.io/all-about-amhs/` (GitHub Pages 활성화 후)

---

## 핵심 기능

| 탭 | 기능 |
|----|------|
| 📚 **AMHS Study** | 학습 카드(카테고리 필터·전문 검색), 개념 사전, 4지선다 퀴즈(점수 추적·취약분야 차트), 용어 플래시카드(뒤집기) |
| 🎮 **Control 실습** | Three.js 3D FAB 레이아웃, OHT 비히클 이동 애니메이션, **A\* 최단경로 탐색 직접 구현**, 속도·우선순위·처리량 제어 패널 |
| 🛠️ **개발 과정** | 프로젝트 타임라인, Claude 도구별 역할 갤러리, 데이터 현황 대시보드(도넛 차트), Self-feedback |

직무 연계: 공식 JD의 4대 업무 — **AMHS 구축(OHT·Robot·Conveyor) / 제어(MES 연계) / SW개발(반송로직·스케줄링·경로탐색) / 운영(Data 분석)** 을 데이터와 시뮬레이션에 반영했습니다.

---

## 사용한 Claude 도구

- **Claude Cowork** — 프로젝트 총괄(PM), 단계별 자율 실행, Self-feedback 루프
- **Claude in Chrome** — SK하이닉스 뉴스룸 자동 크롤링 + 직무기술서 반영
- **Claude Code** — Three.js 3D 시뮬레이션 및 A\* 경로탐색 알고리즘 개발

## 기술 스택

HTML / CSS / Vanilla JS / **Three.js r128** / **Chart.js 4** / **PapaParse 5** · 데이터: **Google Sheets (gviz CSV)** · 배포: **GitHub Pages (서버리스)**

---

## 파일 구조

```
/
├── index.html              # 메인 진입점 · 3탭 통합
├── css/style.css           # SK하이닉스 컬러 · 반응형 · 다크모드
├── js/
│   ├── config.js           # Sheets URL · 앱 설정
│   ├── fallback-data.js     # 내장 폴백 데이터(오프라인/미연결 시)
│   ├── data.js             # CSV fetch + PapaParse + 24h 캐시
│   ├── study.js            # Tab1: 카드·퀴즈·플래시카드
│   ├── simulation.js       # Tab2: Three.js 3D + A* 경로탐색
│   └── devlog.js           # Tab3: 타임라인·대시보드
├── data/                   # Google Sheets 입력용 CSV 원본
│   ├── articles.csv  concepts.csv  quiz_bank.csv  glossary.csv  dev_log.csv
└── README.md
```

---

## 데이터 연동 (Google Sheets)

앱은 **Sheets 미연결 상태에서도 내장 폴백 데이터로 정상 작동**합니다. 라이브 연동을 켜려면:

1. Google Sheets에 5개 탭 생성 — 탭 이름은 정확히 `articles`, `concepts`, `quiz_bank`, `dev_log`, `glossary`
2. `data/*.csv` 내용을 각 탭에 붙여넣기 (1행=헤더)
3. **공유 → "링크가 있는 모든 사용자: 뷰어"** 로 설정 (gviz CSV 접근에 필요)
4. 끝. `js/config.js`의 문서 ID는 이미 적용되어 있습니다.

> 라이브 연동 실패 시 자동으로 내장 데이터로 대체되며, 하단에 출처가 표시됩니다.

---

## 로컬 실행

```bash
# 정적 서버 권장 (fetch CORS 때문에 file:// 보다 안전)
python3 -m http.server 8000
# → http://localhost:8000
```

## GitHub Pages 배포

1. `all-about-amhs` 레포 생성(Public) 후 전체 파일 push
2. Settings → Pages → Source: `main` branch / `root`
3. 1~2분 후 `https://<username>.github.io/all-about-amhs/` 접속

---

*개발: 2026.06 · Claude Cowork · Claude in Chrome · Claude Code*
