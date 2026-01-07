# OneByOne 디자인 회사 웹 프로젝트 요약

## 📌 프로젝트 개요

- **프로젝트명**: OneByOne Studio 웹사이트
- **구조**: React Frontend + Django DRF Backend + Docker
- **Git 방식**: Submodule (메인 저장소에서 frontend/backend 연결)
- **상태**: 프론트엔드 완성 ✅ / 백엔드 개발 예정 ⏳

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
│   ├── models/
│   │   └── submarine.glb              # 3D 모델 파일
│   ├── videos/
│   │   ├── whatwedo-bg.mp4            # What We Do 섹션 배경 영상
│   │   ├── slogan-bg.mp4              # Slogan 섹션 배경 영상
│   │   └── lab/                       # Lab 페이지 영상들
│   ├── images/
│   │   ├── category/                  # 카테고리 썸네일
│   │   ├── portfolio/                 # 포트폴리오 이미지들
│   │   └── lab/                       # Lab 페이지 이미지들
│   └── files/
│       └── company-profile.pdf        # 회사 소개서
│
├── src/
│   ├── index.js                       # React 진입점
│   ├── index.css                      # 글로벌 스타일 (Tailwind directives)
│   ├── App.jsx                        # 라우팅 설정
│   ├── App.css
│   │
│   ├── assets/
│   │   ├── logo.avif                  # 메인 로고 (파티클용)
│   │   └── smallLogo.avif             # 네비게이션 로고
│   │
│   ├── components/
│   │   ├── index.js                   # 컴포넌트 통합 export
│   │   ├── Navbar.jsx                 # 네비게이션 바 + 풀스크린 메뉴
│   │   ├── Footer.jsx                 # 푸터
│   │   ├── PageTransition.jsx         # 페이지 전환 효과 (눈 깜빡임)
│   │   ├── ScrollToTop.jsx            # 페이지 이동 시 스크롤 최상단
│   │   ├── CategoryLayout.jsx         # 카테고리 페이지 공통 레이아웃
│   │   │
│   │   ├── about/
│   │   │   ├── index.js
│   │   │   └── LandingSection.jsx     # About 파티클 로고 효과
│   │   │
│   │   └── home/
│   │       ├── index.js
│   │       ├── LandingSection.jsx     # 파티클 로고 효과
│   │       ├── ThreeDSection.jsx      # 3D 모델 섹션 (PC/모바일 반응형) ✅ NEW
│   │       ├── MobileThreeDSection.jsx # 모바일용 3D 섹션 (별도 파일) ✅ NEW
│   │       ├── WhatWeDoSection.jsx    # 배경 영상 + 텍스트
│   │       ├── PortfolioSection.jsx   # 카테고리 슬라이드인
│   │       ├── SloganSection.jsx      # 배경 영상 + 슬로건
│   │       └── ContactSection.jsx     # 연락처 + 복사 기능
│   │
│   └── pages/
│       ├── index.js                   # 페이지 통합 export
│       ├── Home.jsx                   # 메인 페이지 (6개 섹션)
│       ├── About.jsx                  # 소개 페이지
│       ├── Portfolio.jsx              # 포트폴리오 전체
│       ├── PortfolioDetail.jsx        # 포트폴리오 상세
│       ├── Lab.jsx                    # 랩 페이지
│       ├── Contact.jsx                # 연락처 페이지
│       ├── MediaArt.jsx               # 카테고리: 미디어아트
│       ├── Interactive.jsx            # 카테고리: 인터랙티브
│       ├── Exhibition.jsx             # 카테고리: 전시
│       └── Web.jsx                    # 카테고리: 웹
│
├── tailwind.config.js
├── postcss.config.js
├── package.json
└── Dockerfile
```

---

## 🛣️ 라우팅 구조

| 경로 | 페이지 | 설명 | 상태 |
|------|--------|------|------|
| `/` | Home | 메인 페이지 (6개 섹션) | ✅ 완료 |
| `/about` | About | 회사 소개 | ✅ 완료 |
| `/portfolio` | Portfolio | 포트폴리오 전체 | ✅ 완료 |
| `/portfolio/:id` | PortfolioDetail | 포트폴리오 상세 | ✅ 완료 |
| `/lab` | Lab | 실험실/랩 | ✅ 완료 |
| `/contact` | Contact | 연락처 | ✅ 완료 |
| `/category/media-art` | MediaArt | 미디어아트 카테고리 | ✅ 완료 |
| `/category/interactive` | Interactive | 인터랙티브 카테고리 | ✅ 완료 |
| `/category/exhibition` | Exhibition | 전시 카테고리 | ✅ 완료 |
| `/category/web` | Web | 웹 카테고리 | ✅ 완료 |

---

## 🏠 메인 페이지 (Home) 6개 섹션

### 1. LandingSection (파티클 로고)
- 높이: 250vh (스크롤 범위 확장)
- 로고 이미지(`logo.avif`)를 파티클로 분해
- 스크롤 시 파티클 흩어짐 + 페이드아웃
- 마우스 호버 시 파티클 밀어내기 효과
- sticky로 화면 고정

### 2. ThreeDSection (3D 모델) ✅ NEW
- 높이: 100vh
- GLB 3D 모델 (`/models/submarine.glb`) 로드
- **PC/모바일 반응형 분기** (768px 기준)

**PC 버전**:
- 중앙 모델: 마우스 따라 바라봄 + 두둥실 애니메이션
- 주변 6개 모델: 원형 배치 (x-y 평면)
- 좌클릭: 팝업 열기
- 우클릭 드래그: 모델 Y축 회전
- 마우스 스포트라이트 효과
- 배경 파티클 효과
- 호버 시 글로우 + 라벨 표시

**모바일 버전**:
- 단일 3D 모델 표시 (자동 회전)
- 좌우 스와이프로 프로젝트 전환
- 좌우 네비게이션 버튼
- 하단 페이지 인디케이터
- 탭하여 팝업 열기

**6개 프로젝트 데이터**:
```javascript
const SURROUNDING_MODELS = [
  { id: 1, title: 'Media Art', path: '/portfolio/1' },
  { id: 2, title: 'Interactive', path: '/portfolio/2' },
  { id: 3, title: 'Exhibition', path: '/portfolio/3' },
  { id: 4, title: 'Web Development', path: '/portfolio/4' },
  { id: 5, title: 'Motion Graphics', path: '/portfolio/5' },
  { id: 6, title: 'Installation', path: '/portfolio/6' },
];
```

### 3. WhatWeDoSection
- 배경 영상 루핑 (`whatwedo-bg.mp4`)
- 페이드인 텍스트 애니메이션

### 4. PortfolioSection
- "PORTFOLIO" 글자별 순차 애니메이션
- 4개 카테고리 카드 (우측에서 슬라이드인)
- 카테고리: MEDIA ART, INTERACTIVE, EXHIBITION, WEB

### 5. SloganSection
- 배경 영상 루핑 (`slogan-bg.mp4`)
- 라인별 슬라이드인 텍스트

### 6. ContactSection
- 회사 소개서 다운로드 버튼
- 연락처 정보 + 클릭 시 복사 기능
- Contact Us 버튼

---

## 🎨 3D 섹션 상세 (ThreeDSection)

### 사용 라이브러리
```json
{
  "@react-three/fiber": "^9.0.0",
  "@react-three/drei": "^10.0.0",
  "three": "^0.172.0"
}
```

### PC 버전 컴포넌트 구조
```
ThreeDSection
├── Canvas (camera, shadows, gl settings)
│   └── DesktopScene
│       ├── BackgroundParticles (100개 파티클)
│       ├── ambientLight
│       ├── MouseSpotlight (마우스 따라다니는 조명)
│       ├── pointLight x2 (인디고/핑크 분위기 조명)
│       ├── CenterModel (마우스 방향 바라봄)
│       └── SurroundingModel x6 (원형 배치)
├── 인터랙션 힌트 (상단)
├── 스크롤 인디케이터 (하단)
└── ModelPopup (팝업)
```

### 모바일 버전 컴포넌트 구조
```
ThreeDSection (isMobile 분기)
└── MobileView
    ├── Canvas
    │   └── MobileScene
    │       ├── ambientLight + directionalLight + pointLight
    │       └── MobileModel (자동 회전)
    ├── 상단 안내 텍스트
    ├── 좌/우 네비게이션 버튼
    ├── 하단 정보 영역 (제목, 설명, View Project 버튼)
    ├── 페이지 인디케이터
    └── 팝업
```

### 주요 기능
| 기능 | PC | 모바일 |
|------|-----|--------|
| 모델 표시 | 중앙 1개 + 주변 6개 | 1개 (스와이프로 전환) |
| 회전 조작 | 우클릭 드래그 | 자동 회전 |
| 프로젝트 선택 | 좌클릭 | 탭 |
| 조명 | 스포트라이트 + 파티클 | 기본 조명 |
| 프로젝트 전환 | 클릭으로 선택 | 스와이프/버튼 |

---

## 📄 완료된 페이지 요약

| 페이지 | 주요 기능 |
|--------|----------|
| **Home** | 6개 섹션 (파티클 로고, 3D 모델, What We Do, Portfolio, Slogan, Contact) |
| **About** | 회사 소개 (파티클 로고 효과) |
| **Portfolio** | 전체 목록 + 카테고리 필터 + hover 슬라이드 타이틀 |
| **PortfolioDetail** | 상세 페이지 (이미지/영상, Prev/Next 네비게이션) |
| **Lab** | 실험 프로젝트 목록 (이미지/영상 지원) |
| **Contact** | 문의 폼 + 눈 컴포넌트 (마우스 추적) |
| **Category 페이지** | 공통 레이아웃 (CategoryLayout.jsx) |

---

## 🧭 Navbar 기능

- 상단 고정 (fixed, z-50)
- 좌측: 로고 (홈 링크)
- 우측: ABOUT, PORTFOLIO, LAB, CONTACT 메뉴 + 햄버거 버튼
- 풀스크린 메뉴 (z-300): 햄버거 클릭 시 전체 화면 검정 배경
- 메뉴 항목 순차 애니메이션

---

## 🔄 PageTransition (눈 깜빡임 효과)

- 상단/하단에서 검정 바가 화면 중앙으로 닫힘 (0.4초)
- 페이지 컨텐츠 변경
- 검정 바가 다시 열림 (0.4초)
- z-index: 200

---

## 🎨 디자인 테마

| 항목 | 값 |
|------|-----|
| 배경 | 검정 (`bg-black`) |
| 텍스트 | 흰색 (`text-white`) |
| 보조 텍스트 | 회색 (`text-zinc-300`, `text-zinc-400`) |
| 강조 색상 | 인디고/핑크 (`#6366f1`, `#ec4899`) |
| 전환 효과 | 300-700ms duration |

---

## 🔧 공통 패턴

### 디바이스 타입 감지
```javascript
const useDeviceType = () => {
  const [isMobile, setIsMobile] = useState(false);
  
  useEffect(() => {
    const checkDevice = () => setIsMobile(window.innerWidth <= 768);
    checkDevice();
    window.addEventListener('resize', checkDevice);
    return () => window.removeEventListener('resize', checkDevice);
  }, []);
  
  return { isMobile };
};
```

### 터치 디바이스 감지
```javascript
const [isTouchDevice, setIsTouchDevice] = useState(false);

useEffect(() => {
  const checkTouchDevice = () => {
    setIsTouchDevice(
      'ontouchstart' in window || 
      navigator.maxTouchPoints > 0 ||
      window.matchMedia('(hover: none)').matches
    );
  };
  checkTouchDevice();
}, []);
```

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

---

## ✅ Frontend 완료 상태

### 완료된 작업
- [x] 모든 페이지 UI 구현
- [x] 파티클 로고 효과 (LandingSection)
- [x] 3D 모델 섹션 (ThreeDSection) - PC/모바일 반응형
- [x] 페이지 전환 효과 (PageTransition)
- [x] 네비게이션 + 풀스크린 메뉴
- [x] 카테고리 레이아웃 (hover/터치 분기)
- [x] 포트폴리오 상세 페이지
- [x] Contact 폼 + 눈 컴포넌트
- [x] Lab 페이지 (이미지/영상 지원)
- [x] 반응형 디자인 (PC/모바일)

### 프론트엔드 더미 데이터
현재 모든 데이터는 각 컴포넌트 내부에 하드코딩되어 있음.
백엔드 연동 시 API 호출로 대체 필요.

---

## 📋 Backend 개발 TODO

### 필요한 API 엔드포인트

| 엔드포인트 | 메서드 | 설명 |
|-----------|--------|------|
| `/api/portfolios/` | GET | 포트폴리오 목록 (카테고리 필터) |
| `/api/portfolios/:id/` | GET | 포트폴리오 상세 |
| `/api/categories/` | GET | 카테고리 목록 |
| `/api/lab/` | GET | Lab 프로젝트 목록 |
| `/api/contact/` | POST | 문의 폼 제출 |
| `/api/company/` | GET | 회사 정보 |

### 필요한 모델

**Portfolio**
```python
class Portfolio(models.Model):
    title = models.CharField(max_length=200)
    subtitle = models.CharField(max_length=200, blank=True)
    description = models.TextField()
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    keywords = models.JSONField(default=list)  # ['Media Art', 'Interactive']
    year = models.CharField(max_length=10)
    client = models.CharField(max_length=100, blank=True)
    thumbnail = models.ImageField(upload_to='portfolio/thumbnails/')
    created_at = models.DateTimeField(auto_now_add=True)
    order = models.IntegerField(default=0)
```

**PortfolioMedia**
```python
class PortfolioMedia(models.Model):
    portfolio = models.ForeignKey(Portfolio, related_name='media', on_delete=models.CASCADE)
    type = models.CharField(choices=[('image', 'Image'), ('video', 'Video')])
    file = models.FileField(upload_to='portfolio/media/')
    order = models.IntegerField(default=0)
```

**Category**
```python
class Category(models.Model):
    name = models.CharField(max_length=100)  # Media Art, Interactive, Exhibition, Web
    slug = models.SlugField(unique=True)     # media-art, interactive, exhibition, web
    thumbnail = models.ImageField(upload_to='category/')
```

**LabProject**
```python
class LabProject(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField()
    date = models.CharField(max_length=20)  # "2024.12"
    thumbnail = models.FileField(upload_to='lab/')
    type = models.CharField(choices=[('image', 'Image'), ('video', 'Video')])
    created_at = models.DateTimeField(auto_now_add=True)
```

**ContactInquiry**
```python
class ContactInquiry(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    subject = models.CharField(max_length=200)
    message = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    is_read = models.BooleanField(default=False)
```

---

## 🔗 회사 정보

- **회사명**: 원바이원 스튜디오 (1BY1 STUDIO)
- **E-mail**: onebyone@1-1studio.net
- **사업자등록번호**: 507-86-02842
- **주소**: 서울특별시 강남구 역삼로 77길 6, 2층

---

## 💻 실행 명령어

```bash
# Frontend 개발 서버
cd frontend
npm install
npm start

# Docker 빌드 및 실행
docker-compose up --build

# Git Submodule 클론
git clone --recursive https://github.com/ykh9871/onebyone-main.git
```

---

## 📦 주요 패키지

### Frontend
```json
{
  "react": "^19.0.0",
  "react-router-dom": "^7.x",
  "@react-three/fiber": "^9.0.0",
  "@react-three/drei": "^10.0.0",
  "three": "^0.172.0",
  "tailwindcss": "^3.x",
  "framer-motion": "^11.x"
}
```

### Backend (예정)
```
Django==5.x
djangorestframework==3.x
django-cors-headers
Pillow
psycopg2-binary
python-dotenv
```