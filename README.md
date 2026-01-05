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
│   │   ├── slogan-bg.mp4            # Slogan 섹션 배경 영상
│   │   └── lab/                     # Lab 페이지 영상들
│   ├── images/
│   │   ├── category/                # 카테고리 썸네일
│   │   │   ├── media-art.jpg
│   │   │   ├── interactive.jpg
│   │   │   ├── exhibition.jpg
│   │   │   └── web.jpg
│   │   ├── portfolio/               # 포트폴리오 이미지들
│   │   └── lab/                     # Lab 페이지 이미지들
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
│   │   ├── CategoryLayout.jsx       # 카테고리 페이지 공통 레이아웃 ✅ 완료
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
│       ├── Portfolio.jsx            # 포트폴리오 전체 ✅ 완료
│       ├── PortfolioDetail.jsx      # 포트폴리오 상세 ✅ 완료
│       ├── Lab.jsx                  # 랩 페이지 ✅ 완료
│       ├── Contact.jsx              # 연락처 페이지 ✅ 완료
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

| 경로 | 페이지 | 설명 | 상태 |
|------|--------|------|------|
| `/` | Home | 메인 페이지 (5개 섹션) | ✅ 완료 |
| `/about` | About | 회사 소개 | ⏳ TODO |
| `/portfolio` | Portfolio | 포트폴리오 전체 | ✅ 완료 |
| `/portfolio/:id` | PortfolioDetail | 포트폴리오 상세 | ✅ 완료 |
| `/lab` | Lab | 실험실/랩 | ✅ 완료 |
| `/contact` | Contact | 연락처 | ✅ 완료 |
| `/category/media-art` | MediaArt | 미디어아트 카테고리 | ✅ 완료 |
| `/category/interactive` | Interactive | 인터랙티브 카테고리 | ✅ 완료 |
| `/category/exhibition` | Exhibition | 전시 카테고리 | ✅ 완료 |
| `/category/web` | Web | 웹 카테고리 | ✅ 완료 |

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
- Contact Us → 버튼 (Contact 페이지로 이동)

---

## 📄 완료된 페이지 상세

### 1. CategoryLayout.jsx
**위치**: `src/components/CategoryLayout.jsx`

**기능**:
- 카테고리별 포트폴리오 그리드 (미디어아트, 인터랙티브, 전시, 웹)
- 3열 그리드 (모바일 1열), 카드 간격 있음 (`gap-4 md:gap-5 lg:gap-6`)
- 테두리 없음, `rounded-lg` 모서리

**PC (hover 가능)**:
- hover 시 화면 좌측 하단에 큰 제목 `fixed` 표시
- hover된 카드 밝게, 나머지 어둡게 (`bg-black/70`)
- 우측 상단 화살표 아이콘 표시

**터치 디바이스**:
- 카드 내부 하단에 제목 항상 표시
- 하단 그라데이션 오버레이
- 화살표 항상 표시 (약간 투명)

**터치 디바이스 감지 코드**:
```javascript
useEffect(() => {
  const checkTouchDevice = () => {
    setIsTouchDevice(
      'ontouchstart' in window || 
      navigator.maxTouchPoints > 0 ||
      window.matchMedia('(hover: none)').matches
    );
  };
  checkTouchDevice();
  window.addEventListener('resize', checkTouchDevice);
  return () => window.removeEventListener('resize', checkTouchDevice);
}, []);
```

---

### 2. Portfolio.jsx
**위치**: `src/pages/Portfolio.jsx`

**기능**:
- 전체 포트폴리오 목록 + 카테고리 필터링
- 중앙 상단 "PROJECT" 타이틀 (글자별 애니메이션)
- 필터: ALL, MEDIA ART, INTERACTIVE, EXHIBITION, WEB

**필터 UI**:
- PC: 언더라인 탭 스타일 (hover 시 언더라인 확장)
- 모바일: 드롭다운 select

**hover 타이틀 슬라이드인/아웃 효과**:
- 별도 `SlideTitle` 컴포넌트 분리
- hover 변경 시: 슬라이드아웃 (500ms) → 새 타이틀 슬라이드인
- hover 해제 시: 슬라이드아웃 후 컴포넌트 언마운트
- `isTransitioning` 상태로 빠른 hover 변경 처리
- `pendingItemRef`로 트랜지션 중 새 hover 대기

**SlideTitle 컴포넌트**:
```javascript
const SlideTitle = ({ title, isVisible, delay = 300 }) => {
  const [isAnimating, setIsAnimating] = useState(false);

  useEffect(() => {
    if (isVisible) {
      const timer = setTimeout(() => setIsAnimating(true), delay);
      return () => clearTimeout(timer);
    } else {
      setIsAnimating(false);
    }
  }, [isVisible, delay]);

  return (
    <div className="pb-8 overflow-hidden md:pb-10">
      <h2 className={`text-4xl font-bold text-white md:text-6xl lg:text-7xl xl:text-9xl 
        drop-shadow-2xl leading-tight transform-gpu transition-transform duration-500 ease-out 
        ${isAnimating ? 'translate-y-0' : 'translate-y-[150%]'}`}
      >
        {title}
      </h2>
    </div>
  );
};
```

**hover 상태 관리**:
```javascript
const [hoveredItem, setHoveredItem] = useState(null);
const [displayedItem, setDisplayedItem] = useState(null);
const [isTitleVisible, setIsTitleVisible] = useState(false);
const [isTransitioning, setIsTransitioning] = useState(false);
const pendingItemRef = useRef(null);

useEffect(() => {
  if (isTransitioning) {
    pendingItemRef.current = hoveredItem;
    return;
  }

  if (hoveredItem !== null) {
    if (displayedItem === null) {
      // 처음 hover: 바로 슬라이드인
      setDisplayedItem(hoveredItem);
      setIsTitleVisible(true);
    } else if (hoveredItem !== displayedItem) {
      // 다른 아이템으로 변경: 슬라이드아웃 → 슬라이드인
      setIsTransitioning(true);
      setIsTitleVisible(false);
      
      setTimeout(() => {
        setDisplayedItem(hoveredItem);
        setIsTitleVisible(true);
        setTimeout(() => {
          setIsTransitioning(false);
          if (pendingItemRef.current !== null && pendingItemRef.current !== hoveredItem) {
            setHoveredItem(pendingItemRef.current);
          }
          pendingItemRef.current = null;
        }, 100);
      }, 500);
    }
  } else {
    // hover 해제
    setIsTitleVisible(false);
    setTimeout(() => setDisplayedItem(null), 500);
  }
}, [hoveredItem, displayedItem, isTransitioning]);
```

---

### 3. Lab.jsx
**위치**: `src/pages/Lab.jsx`

**기능**:
- 실험적 프로젝트 목록
- 타이틀: "Exploring the Unknown" (글자별 애니메이션)
- 부제: "An ongoing laboratory where art and technology continuously converge."
- **세부 페이지 없음** (Link 제거, 화살표 아이콘 제거)
- 이미지 또는 영상 지원 (`type: 'image' | 'video'`)
- 영상: `autoPlay`, `loop`, `muted`, `playsInline`

**hover/터치 효과**:
- PC: hover 시 카드 어두워지며 (`bg-black/60`) 날짜/제목/설명 표시
- 터치: 항상 날짜/제목/설명 표시

**데이터 구조**:
```javascript
const labItems = [
  {
    id: 1,
    title: 'Particle System Experiment',
    date: '2024.12',
    description: '파티클 시스템을 활용한 인터랙티브 비주얼 실험 프로젝트',
    thumbnail: '/images/lab/lab-1.jpg', // 또는 /videos/lab/lab-1.mp4
    type: 'image', // 'image' 또는 'video'
  },
  // ...
];
```

**이미지/영상 조건부 렌더링**:
```jsx
{item.type === 'video' ? (
  <video
    className="absolute inset-0 w-full h-full object-cover ..."
    src={item.thumbnail}
    autoPlay
    loop
    muted
    playsInline
  />
) : (
  <div 
    className="absolute inset-0 bg-center bg-cover ..."
    style={{ backgroundImage: `url(${item.thumbnail})` }}
  />
)}
```

---

### 4. Contact.jsx
**위치**: `src/pages/Contact.jsx`

**기능**:
- 문의 폼 (NAME, EMAIL, SUBJECT, MESSAGE)
- 타이틀: "Please feel free to contact us." (글자별 애니메이션)
- 이메일 복사 버튼 (`or onebyone@1-1studio.net [Copy]`)
- 컨텐츠 수직 중앙 정렬 (`flex items-center min-h-screen`)
- Send 버튼 + 로딩 스피너

**픽셀아트 눈 2개** (PC lg 이상에서만 표시):
- `absolute` 포지션 (페이지 내에서만 고정, 스크롤 시 따라오지 않음)
- 흰색 사각형 + 검정 눈동자 + 흰색 하이라이트
- 마우스 위치에 따라 눈동자 이동 (최대 8px)

**PixelEye 컴포넌트**:
```javascript
const PixelEye = () => (
  <div className="relative w-16 h-16 md:w-20 md:h-20 bg-white">
    <div 
      className="absolute w-6 h-6 bg-black md:w-8 md:h-8"
      style={{
        left: '50%',
        top: '50%',
        transform: `translate(calc(-50% + ${pupilPosition.x}px), calc(-50% + ${pupilPosition.y}px))`,
        transition: 'transform 0.1s ease-out',
      }}
    >
      <div className="absolute top-0 right-0 w-2 h-2 bg-white md:w-3 md:h-3" />
    </div>
  </div>
);
```

**마우스 추적**:
```javascript
useEffect(() => {
  const handleMouseMove = (e) => {
    if (!eyesRef.current) return;

    const eyes = eyesRef.current.getBoundingClientRect();
    const eyesCenterX = eyes.left + eyes.width / 2;
    const eyesCenterY = eyes.top + eyes.height / 2;

    const angle = Math.atan2(e.clientY - eyesCenterY, e.clientX - eyesCenterX);
    const distance = Math.min(
      Math.hypot(e.clientX - eyesCenterX, e.clientY - eyesCenterY) / 15,
      8
    );

    const x = Math.cos(angle) * distance;
    const y = Math.sin(angle) * distance;

    setPupilPosition({ x, y });
  };

  window.addEventListener('mousemove', handleMouseMove);
  return () => window.removeEventListener('mousemove', handleMouseMove);
}, []);
```

---

### 5. PortfolioDetail.jsx
**위치**: `src/pages/PortfolioDetail.jsx`

**기능**:
- 포트폴리오 세부 페이지
- URL: `/portfolio/:id`
- "Back to Portfolio" 버튼 **fixed 고정** (스크롤해도 보임)
- 좌우 여백 넓음 (`px-8 md:px-16 lg:px-24 xl:px-32`)
- SHARE + 링크 복사 버튼
- Prev/Next Project 네비게이션

**레이아웃**:
```
┌─────────────────────────────────────────────────────────────────┐
│ ← Back to Portfolio (fixed 고정)                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│    [타이틀 - 큰 글씨]        │  [설명 텍스트]                   │
│    [부제 - 작은 글씨]        │                                  │
│                              │  [키워드] [키워드] [키워드]      │
│    YEAR     CLIENT           │  (타원 테두리)                   │
│    2024     Samsung          │                                  │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [이미지/영상 1 - 중앙 정렬]                        │
│              [이미지/영상 2]                                    │
│              ... (최대 10개)                                    │
│                                                                 │
│                    SHARE  [🔗 Copy Link]                        │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│ ← Prev Project                              Next Project →     │
└─────────────────────────────────────────────────────────────────┘
```

**데이터 구조**:
```javascript
{
  title: 'Media Project One',
  subtitle: 'Interactive Media Installation',
  description: '미디어 아트와 기술의 융합을...',
  keywords: ['Media Art', 'Interactive', 'Installation'],
  year: '2024',
  client: 'Samsung',
  media: [
    { type: 'image', src: '/images/portfolio/...' },
    { type: 'video', src: '/videos/portfolio/...' },
  ],
}
```


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
| 보조 텍스트 | 회색 (`text-gray-300`, `text-gray-400`, `text-gray-500`) |
| 강조 색상 | 파란색 (`text-blue-400`) |
| 전환 효과 | 300-700ms duration |
| 둥근 모서리 | `rounded-lg`, `rounded-full` (버튼/태그) |
| hover 효과 | 밝기 변화, 스케일 변화, 색상 변화 |

---

## 🔧 공통 패턴

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
  window.addEventListener('resize', checkTouchDevice);
  return () => window.removeEventListener('resize', checkTouchDevice);
}, []);
```

### 페이지 진입 애니메이션
```javascript
const [isVisible, setIsVisible] = useState(false);

useEffect(() => {
  setIsVisible(true);
}, []);

// 사용
className={`... transition-all duration-700 ${
  isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
}`}
```

### 글자별 애니메이션
```javascript
const titleLetters = title.split('');

{titleLetters.map((letter, index) => (
  <span
    key={index}
    className={`inline-block transition-transform duration-700 ease-out ${
      isVisible ? 'translate-y-0' : 'translate-y-full'
    }`}
    style={{ transitionDelay: `${index * 50}ms` }}
  >
    {letter === ' ' ? '\u00A0' : letter}
  </span>
))}
```

### 이메일/링크 복사
```javascript
const [copied, setCopied] = useState(false);

const handleCopy = async (text) => {
  try {
    await navigator.clipboard.writeText(text);
    setCopied(true);
    setTimeout(() => setCopied(false), 2000);
  } catch (err) {
    console.error('복사 실패:', err);
  }
};
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

/* 스크롤바 숨기기 */
.scrollbar-hide {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}

#root {
  overflow-x: clip;  /* 가로 스크롤 방지 (sticky 영향 없음) */
}
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

## ✅ 해결된 이슈들

1. **Tailwind 미적용**: index.css에 `@tailwind` directives 추가
2. **햄버거 메뉴 떨림**: z-index 조정 (메뉴 z-300 > PageTransition z-200)
3. **파티클 띠용띠용 효과**: 속도 기반 → 직접 선형 보간으로 변경
4. **마우스 좌표 불일치**: sticky 상태에서 clientX/Y 직접 사용
5. **모바일 가로 스크롤**: `overflow-x: clip` 사용 (hidden 대신)
6. **페이지 이동 시 스크롤 유지**: ScrollToTop 컴포넌트 추가
7. **hover 시 타이틀 슬라이드**: 아이템 변경 시 슬라이드아웃 → 슬라이드인 순서
8. **터치 디바이스 대응**: hover 불가 환경에서 카드 내부에 정보 항상 표시
9. **fixed vs absolute**: 눈 컴포넌트가 스크롤 따라오는 문제 → absolute로 변경

---

## 📋 남은 작업 (TODO)

- [ ] About 페이지 디자인
- [ ] Backend API 연동
- [ ] 반응형 디자인 테스트/수정
- [ ] 이미지/영상 에셋 준비
- [ ] SEO 메타 태그 추가

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