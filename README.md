# OneByOne 디자인 회사 웹 프로젝트 요약

## 📌 프로젝트 개요

- **프로젝트명**: OneByOne Studio 웹사이트
- **구조**: React Frontend + Django DRF Backend + Docker
- **Git 방식**: Submodule (메인 저장소에서 frontend/backend 연결)

### Git 저장소
```
Main: https://github.com/ykh9871/onebyone-main.git
├── Frontend: https://github.com/ykh9871/onebyone-frontend.git
└── Backend: https://github.com/ykh9871/onebyone-backend.git
```

---

## 📁 Frontend 디렉토리 구조

```
frontend/
├── public/
│   ├── index.html
│   ├── videos/
│   │   ├── whatwedo-bg.mp4          # What We Do 섹션 배경 영상
│   │   └── slogan-bg.mp4            # Slogan 섹션 배경 영상
│   ├── images/
│   │   ├── category/                # 카테고리 썸네일
│   │   │   ├── media-art.jpg
│   │   │   ├── interactive.jpg
│   │   │   ├── exhibition.jpg
│   │   │   └── web.jpg
│   │   └── portfolio/               # 포트폴리오 이미지들
│   └── files/
│       └── company-profile.pdf      # 회사 소개서
│
├── src/
│   ├── index.js                     # React 진입점
│   ├── index.css                    # 글로벌 스타일 (Tailwind directives)
│   ├── App.js                       # 라우팅 설정
│   ├── App.css
│   │
│   ├── assets/
│   │   ├── logo.avif                # 메인 로고 (파티클용)
│   │   └── smallLogo.avif           # 네비게이션 로고
│   │
│   ├── components/
│   │   ├── index.js                 # 컴포넌트 통합 export
│   │   ├── Navbar.jsx               # 네비게이션 바 + 풀스크린 메뉴
│   │   ├── Footer.jsx               # 푸터
│   │   ├── PageTransition.jsx       # 페이지 전환 효과 (눈 깜빡임)
│   │   ├── ScrollToTop.jsx          # 페이지 이동 시 스크롤 최상단
│   │   ├── CategoryLayout.jsx       # 카테고리 페이지 공통 레이아웃
│   │   │
│   │   └── home/                    # 홈 페이지 섹션 컴포넌트
│   │       ├── index.js
│   │       ├── LandingSection.jsx   # 파티클 로고 효과
│   │       ├── WhatWeDoSection.jsx  # 배경 영상 + 텍스트
│   │       ├── PortfolioSection.jsx # 카테고리 슬라이드인
│   │       ├── SloganSection.jsx    # 배경 영상 + 슬로건
│   │       └── ContactSection.jsx   # 연락처 + 복사 기능
│   │
│   └── pages/
│       ├── index.js                 # 페이지 통합 export
│       ├── Home.jsx                 # 메인 페이지
│       ├── About.jsx                # 소개 페이지
│       ├── Portfolio.jsx            # 포트폴리오 전체
│       ├── PortfolioDetail.jsx      # 포트폴리오 상세
│       ├── Lab.jsx                  # 랩 페이지
│       ├── Contact.jsx              # 연락처 페이지
│       ├── MediaArt.jsx             # 카테고리: 미디어아트
│       ├── Interactive.jsx          # 카테고리: 인터랙티브
│       ├── Exhibition.jsx           # 카테고리: 전시
│       └── Web.jsx                  # 카테고리: 웹
│
├── tailwind.config.js
├── postcss.config.js
├── package.json
└── Dockerfile
```

---

## 🛣️ 라우팅 구조

| 경로 | 페이지 | 설명 |
|------|--------|------|
| `/` | Home | 메인 페이지 (5개 섹션) |
| `/about` | About | 회사 소개 |
| `/portfolio` | Portfolio | 포트폴리오 전체 |
| `/portfolio/:id` | PortfolioDetail | 포트폴리오 상세 |
| `/lab` | Lab | 실험실/랩 |
| `/contact` | Contact | 연락처 |
| `/category/media-art` | MediaArt | 미디어아트 카테고리 |
| `/category/interactive` | Interactive | 인터랙티브 카테고리 |
| `/category/exhibition` | Exhibition | 전시 카테고리 |
| `/category/web` | Web | 웹 카테고리 |

---

## 🏠 메인 페이지 (Home) 5개 섹션

### 1. LandingSection (파티클 로고)
- 높이: 250vh (스크롤 범위 확장)
- 로고 이미지(`logo.avif`)를 파티클로 분해
- 스크롤 시 파티클 흩어짐 + 페이드아웃
- 마우스 호버 시 파티클 밀어내기 효과
- sticky로 화면 고정

### 2. WhatWeDoSection
- 배경 영상 루핑 (`whatwedo-bg.mp4`)
- 페이드인 텍스트 애니메이션

### 3. PortfolioSection
- "PORTFOLIO" 글자별 순차 애니메이션 (한 글자씩 아래에서 위로)
- 4개 카테고리 카드 (우측에서 슬라이드인)
- 카테고리: MEDIA ART, INTERACTIVE, EXHIBITION, WEB
- 이미지 비율: 16:9 (aspect-video)
- 각 카드 클릭 시 해당 카테고리 페이지로 이동

### 4. SloganSection
- 배경 영상 루핑 (`slogan-bg.mp4`)
- 라인별 슬라이드인 텍스트

### 5. ContactSection
- 제목: "Where Art and Technology Converge, Without Boundaries"
- 부제: "예술과 기술의 융합을 통해 미디어아트와 인터렉션 아트를 경계없이 창조합니다"
- 회사 소개서 다운로드 버튼
- 연락처 정보 (E-mail, OFFICE, PHONE) + 클릭 시 복사 기능

---

## 🧭 Navbar 기능

- 상단 고정 (fixed, z-50)
- 좌측: 로고 (홈 링크)
- 우측: ABOUT, PORTFOLIO, LAB, CONTACT 메뉴 + 햄버거 버튼
- 풀스크린 메뉴 (z-300): 햄버거 클릭 시 전체 화면 검정 배경
- 메뉴 항목 순차 애니메이션
- 메뉴 닫힌 후 300ms 뒤 페이지 이동 (전환 효과와 충돌 방지)

---

## 🔄 PageTransition (눈 깜빡임 효과)

- 상단/하단에서 검정 바가 화면 중앙으로 닫힘 (0.4초)
- 페이지 컨텐츠 변경
- 검정 바가 다시 열림 (0.4초)
- z-index: 200
- 첫 로딩 시 애니메이션 없음

---

## 🎨 디자인 테마

| 항목 | 값 |
|------|-----|
| 배경 | 검정 (`bg-black`) |
| 텍스트 | 흰색 (`text-white`) |
| 보조 텍스트 | 회색 (`text-gray-300`, `text-gray-400`) |
| 강조 색상 | 파란색 (`text-blue-400`) |
| 전환 효과 | 300ms duration |

---

## 🐳 Docker 구성

### docker-compose.yml
```yaml
services:
  db:
    image: postgres
    ports: 54320:5432
    
  backend:
    build: ./backend
    ports: 8000:8000
    
  frontend:
    build: ./frontend
    ports: 3000:3000
```

### 환경변수 (.env)
```
POSTGRES_DB=onebyone
POSTGRES_USER=onebyone_user
POSTGRES_PASSWORD=your_secure_password
POSTGRES_HOST=db
POSTGRES_PORT=5432
SECRET_KEY=your-django-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
TZ=Asia/Seoul
```

---

## ⚙️ 필수 설정 파일

### tailwind.config.js
```javascript
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}", "./public/index.html"],
  theme: {
    extend: {
      transitionDuration: { '400': '400ms' }
    }
  },
  plugins: [],
}
```

### postcss.config.js
```javascript
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

### index.css (필수!)
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* ... 기타 스타일 */

#root {
  overflow-x: clip;  /* 가로 스크롤 방지 (sticky 영향 없음) */
}
```

---

## ✅ 해결된 이슈들

1. **Tailwind 미적용**: index.css에 `@tailwind` directives 추가
2. **햄버거 메뉴 떨림**: z-index 조정 (메뉴 z-300 > PageTransition z-200)
3. **파티클 띠용띠용 효과**: 속도 기반 → 직접 선형 보간으로 변경
4. **마우스 좌표 불일치**: sticky 상태에서 clientX/Y 직접 사용
5. **모바일 가로 스크롤**: `overflow-x: clip` 사용 (hidden 대신)
6. **페이지 이동 시 스크롤 유지**: ScrollToTop 컴포넌트 추가

---

## 📋 남은 작업 (TODO)

- [ ] About 페이지 디자인
- [ ] Portfolio 페이지 디자인
- [ ] PortfolioDetail 페이지 디자인
- [ ] Lab 페이지 디자인
- [ ] Contact 페이지 디자인
- [ ] Backend API 연동
- [ ] 카테고리 페이지 API 연동
- [ ] 반응형 디자인 테스트/수정
- [ ] 이미지/영상 에셋 준비

---

## 🔗 회사 정보

- **회사명**: 원바이원 스튜디오 (1BY1 STUDIO)
- **E-mail**: onebyone@1-1studio.net
- **사업자등록번호**: 507-86-02842
- **주소**: 서울특별시 강남구 역삼로 77길 6, 2층

---

## 💻 실행 명령어

```bash
# Docker 빌드 및 실행
docker-compose up --build

# 백그라운드 실행
docker-compose up -d --build

# 종료
docker-compose down

# 볼륨까지 삭제 (DB 초기화)
docker-compose down -v

# Git Submodule 클론
git clone --recursive https://github.com/ykh9871/onebyone-main.git
```