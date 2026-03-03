# OneByOne Studio 웹 프로젝트

> 최종 업데이트: 2026년 3월 4일

---

## 📌 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | OneByOne Studio 웹사이트 |
| **목적** | 미디어아트 스튜디오 포트폴리오 및 회사 소개 웹사이트 |
| **Production** | https://onebyonestudio.com |
| **Frontend (Dev)** | http://ces2025.iptime.org:30000 |
| **Backend API (Dev)** | http://ces2025.iptime.org:38000 |
| **Production API** | https://api.onebyonestudio.com |
| **구조** | 모노레포 (Frontend `src/` + Backend `onebyone-backend/` 분리) |

---

## 🛠 기술 스택

### Frontend

| 기술 | 버전/설명 |
|------|----------|
| React | 18.x |
| Vite | 빌드 도구 |
| React Router | 클라이언트 라우팅 |
| Tailwind CSS | 유틸리티 기반 스타일링 |
| Three.js | 3D WebGL 렌더링 |
| @react-three/fiber | React Three.js 래퍼 |
| @react-three/drei | Three.js 유틸리티 헬퍼 |
| Axios | HTTP 클라이언트 (인터셉터 기반 JWT 처리) |

### Backend

| 기술 | 버전/설명 |
|------|----------|
| Python | 3.12 |
| Django | 5.2.6 |
| Django REST Framework | 3.16.1 — RESTful API 구축 |
| djangorestframework-simplejwt | 5.5.1 — JWT 인증 |
| PyJWT | 2.10.1 — JWT 토큰 처리 |
| django-cors-headers | 4.8.0 — CORS 처리 |
| django-filter | 24.3 — 쿼리셋 필터링 |
| django-admin-sortable2 | 2.2.4 — Admin 정렬 |
| django-storages | 1.14.6 — AWS S3 파일 스토리지 |
| boto3 | 1.40.32 — AWS SDK |
| botocore | 1.40.32 — boto3 코어 라이브러리 |
| s3transfer | 0.14.0 — S3 파일 전송 |
| Pillow | 11.3.0 — 이미지 처리 |
| psycopg2-binary | 2.9.10 — PostgreSQL 어댑터 |
| python-decouple | 3.8 — 환경변수 관리 |
| requests | 2.31.0 — HTTP 클라이언트 |
| PostgreSQL | 데이터베이스 |
| Docker | 컨테이너화 |

### 인프라 및 배포

| 기술 | 설명 |
|------|------|
| AWS S3 | 미디어/정적 파일 스토리지 (선택적) |
| AWS CloudFront | CDN (선택적) |
| AWS Amplify | 프론트엔드 호스팅 (`main.d2e20hsqeo3cjt.amplifyapp.com`) |
| Docker | 백엔드 컨테이너화 (`python:3.12` 기반) |

---

## 📁 프로젝트 구조

```
onebyone-studio/
├── src/                          # Frontend (React)
│   ├── api/                      # API 통신 모듈
│   │   ├── config.js             # Axios 인스턴스 + 인터셉터 (JWT 자동 갱신)
│   │   ├── admin.js              # Admin API (인증, CRUD, 토글, 유튜브 미디어 등)
│   │   ├── portfolio.js          # Public 포트폴리오 API
│   │   ├── contact.js            # 문의 등록 API
│   │   ├── lab.js                # Lab 프로젝트 API
│   │   └── index.js
│   ├── components/
│   │   ├── home/
│   │   │   ├── LandingSection.jsx
│   │   │   ├── ThreeDSection.jsx      # 3D 모델 렌더링 (Three.js, ~1,096줄)
│   │   │   ├── WhatWeDoSection.jsx
│   │   │   ├── PortfolioSection.jsx   # 카테고리 캐러셀 + 클라이언트 로고
│   │   │   ├── ContactSection.jsx
│   │   │   └── index.js
│   │   ├── about/
│   │   │   ├── AboutSection.jsx
│   │   │   └── index.js
│   │   ├── Navbar.jsx
│   │   ├── Footer.jsx
│   │   ├── PageTransition.jsx
│   │   ├── ScrollToTop.jsx
│   │   ├── CategoryLayout.jsx
│   │   └── index.js
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   ├── Portfolio.jsx
│   │   ├── PortfolioDetail.jsx
│   │   ├── Lab.jsx
│   │   ├── Contact.jsx
│   │   ├── MediaArt.jsx
│   │   ├── Interactive.jsx
│   │   ├── Exhibition.jsx
│   │   ├── Web.jsx
│   │   └── index.js
│   ├── admin/
│   │   ├── AdminRoutes.jsx
│   │   ├── index.js
│   │   ├── components/
│   │   │   ├── AdminLayout.jsx
│   │   │   └── PrivateRoute.jsx
│   │   └── pages/
│   │       ├── AdminLogin.jsx
│   │       ├── AdminDashboard.jsx
│   │       ├── AdminPortfolios.jsx
│   │       ├── AdminPortfolioEdit.jsx
│   │       ├── AdminCategories.jsx
│   │       ├── AdminLab.jsx
│   │       ├── AdminLabEdit.jsx
│   │       ├── AdminContacts.jsx
│   │       └── index.js
│   ├── contexts/
│   │   └── AuthContext.jsx
│   ├── assets/
│   │   ├── logo.avif
│   │   ├── logo.png
│   │   └── smallLogo.avif
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── index.js
│
└── onebyone-backend/
    ├── config/
    │   ├── settings.py
    │   ├── urls.py
    │   ├── views.py
    │   ├── asgi.py
    │   └── wsgi.py
    ├── apps/
    │   ├── portfolio/
    │   │   ├── models.py
    │   │   ├── views.py
    │   │   ├── serializers.py
    │   │   ├── urls.py
    │   │   ├── admin_views.py
    │   │   ├── admin_serializers.py
    │   │   ├── admin_urls.py
    │   │   └── admin.py
    │   ├── lab/
    │   │   ├── models.py
    │   │   ├── views.py
    │   │   ├── serializers.py
    │   │   ├── urls.py
    │   │   ├── admin_views.py
    │   │   ├── admin_serializers.py
    │   │   ├── admin_urls.py
    │   │   └── admin.py
    │   └── contact/
    │       ├── models.py
    │       ├── views.py
    │       ├── serializers.py
    │       ├── urls.py
    │       ├── admin_views.py
    │       ├── admin_serializers.py
    │       ├── admin_urls.py
    │       └── admin.py
    ├── mediafiles/
    ├── staticfiles/
    ├── requirements.txt
    ├── Dockerfile
    └── manage.py
```

---

## 🔐 인증 시스템

JWT (JSON Web Token) 기반 인증을 사용합니다.

| 항목 | 설정 |
|------|------|
| Access Token 수명 | 12시간 |
| Refresh Token 수명 | 7일 |
| Refresh Rotation | 활성화 (갱신 시 새 Refresh 발급) |
| Blacklist | 설정값 활성화 ⚠️ 앱 미등록으로 실제 미동작 |
| Header 형식 | `Authorization: Bearer <token>` |

**프론트엔드 토큰 흐름**: Axios 인터셉터가 모든 요청에 자동으로 Bearer 토큰을 첨부하며, 401 응답 시 Refresh Token으로 자동 갱신을 시도합니다. 갱신 실패 시 localStorage 토큰 제거 후 `/admin/login`으로 리다이렉트됩니다.

> ⚠️ **알려진 이슈**: `BLACKLIST_AFTER_ROTATION: True`가 설정되어 있으나 `rest_framework_simplejwt.token_blacklist`가 `INSTALLED_APPS`에 포함되어 있지 않아 블랙리스트가 실제로 동작하지 않습니다. → **향후 개선 사항** 참조

---

## 🗄 데이터 모델

### Category

| 필드 | 타입 | 설명 |
|------|------|------|
| name | CharField(100) | 한글 카테고리명 |
| name_en | CharField(100) | 영문 카테고리명 |
| slug | SlugField (unique) | URL 식별자 |
| thumbnail | ImageField | 카테고리 대표 이미지 (`upload_to="category/"`, blank 허용) |
| bg_color | CharField(7) | 배경 HEX 색상 (기본: `#1a1a2e`) |
| order | PositiveIntegerField | 정렬순서 (기본: 0) |

**기본 정렬**: `order` → `name`

### Portfolio

| 필드 | 타입 | 설명 |
|------|------|------|
| title | CharField(200) | 제목 |
| subtitle | CharField(200) | 부제목 (blank 허용) |
| description | TextField | 설명 |
| category | FK → Category | 카테고리 (`on_delete=CASCADE`) |
| keywords | JSONField | 키워드 배열 (기본: `[]`) |
| year | CharField(10) | 연도 |
| client | CharField(100) | 클라이언트명 (blank 허용) |
| thumbnail | ImageField | 썸네일 (`upload_to="portfolio/thumbnails/"`) |
| model_file | CharField(20) | 3D 모델 선택 (홈 화면용, **중복 선택 불가**) |
| is_pinned | BooleanField | 상단 고정 여부 (기본: False) |
| is_active | BooleanField | 공개 여부 (기본: True) |
| order | PositiveIntegerField | 정렬순서 (기본: 0) |
| created_at | DateTimeField | 생성일 (auto_now_add) |
| updated_at | DateTimeField | 수정일 (auto_now) |

**model_file 선택지**: `""` (선택 안함), `submarine`, `arrow`, `car`, `character`, `stamp`, `ice_cream`

**model_file 중복 검증**: `PortfolioAdminCreateUpdateSerializer`에서 동일 model_file을 다른 포트폴리오가 이미 사용 중인 경우 `ValidationError` 발생 (수정 시 자기 자신 제외)

**기본 정렬**: `-is_pinned` → `order` → `-created_at`

### PortfolioMedia

| 필드 | 타입 | 설명 |
|------|------|------|
| portfolio | FK → Portfolio | 소속 포트폴리오 (`on_delete=CASCADE`) |
| type | CharField(10) | `image`, `video`, 또는 `youtube` |
| file | FileField | 미디어 파일 (`upload_to="portfolio/media/"`, blank 허용) |
| video_url | URLField(500) | 유튜브 URL (youtube 타입 전용, `youtube.com/watch?v=` 또는 `youtu.be/` 형식) |
| order | PositiveIntegerField | 정렬순서 (기본: 0) |

**제한**: 포트폴리오당 최대 10개  
**기본 정렬**: `order`

### LabProject

| 필드 | 타입 | 설명 |
|------|------|------|
| title | CharField(200) | 제목 |
| description | TextField | 설명 |
| date | CharField(20) | 날짜 표시 (예: `2024.12`) |
| thumbnail | FileField | 썸네일 (`upload_to="lab/"`) |
| type | CharField(10) | `image` 또는 `video` (기본: `image`) |
| is_active | BooleanField | 공개 여부 (기본: True) |
| order | PositiveIntegerField | 정렬순서 (기본: 0) |
| created_at | DateTimeField | 생성일 (auto_now_add) |
| updated_at | DateTimeField | 수정일 (auto_now) |

**기본 정렬**: `order` → `-created_at`

> **참고**: Public API(`LabProjectSerializer`)에서는 `id`, `title`, `description`, `date`, `thumbnail`, `type`만 노출됩니다. `is_active`, `order`, `created_at`, `updated_at`는 Admin API에서만 접근 가능합니다.

### ContactInquiry

| 필드 | 타입 | 설명 |
|------|------|------|
| name | CharField(100) | 이름 |
| email | EmailField | 이메일 |
| subject | CharField(200) | 제목 |
| message | TextField | 내용 |
| is_read | BooleanField | 읽음 여부 (기본: False) |
| created_at | DateTimeField | 문의일 (auto_now_add) |

**기본 정렬**: `-created_at`

---

## 📝 API 엔드포인트

### 인증

| Method | Endpoint | 설명 |
|--------|----------|------|
| POST | `/api/auth/login/` | JWT 토큰 발급 (username + password) |
| POST | `/api/auth/refresh/` | Access Token 갱신 |
| GET | `/api/auth/me/` | 현재 로그인 사용자 정보 🔒 |

### Public — Portfolio

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/portfolio/` | 포트폴리오 목록 (`?category=<slug>`, `?pinned=true`, `?search=`, `?ordering=`) |
| GET | `/api/portfolio/<id>/` | 포트폴리오 상세 (이전/다음 네비게이션 포함) |
| GET | `/api/portfolio/featured/` | 3D 모델이 배정된 포트폴리오 (최대 6개, 홈 3D용) |
| GET | `/api/portfolio/categories/` | 카테고리 목록 (slug 기반 lookup) |
| GET | `/api/portfolio/categories/<slug>/` | 카테고리 상세 |
| GET | `/api/portfolio/categories/<slug>/portfolios/` | 카테고리별 포트폴리오 |

### Public — Lab

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/lab/` | Lab 프로젝트 목록 (is_active=True만) |
| GET | `/api/lab/<id>/` | Lab 프로젝트 상세 |

### Public — Contact

| Method | Endpoint | 설명 |
|--------|----------|------|
| POST | `/api/contact/` | 문의 등록 |

### Admin — Dashboard 🔒

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/admin/dashboard/` | 통합 대시보드 통계 (포트폴리오, 카테고리, Lab, 문의, 최근 항목) |

### Admin — Category 🔒

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/admin/categories/` | 카테고리 목록 (포트폴리오 수 포함) |
| POST | `/api/admin/categories/` | 카테고리 생성 (multipart) |
| GET | `/api/admin/categories/<id>/` | 카테고리 상세 |
| PATCH | `/api/admin/categories/<id>/` | 카테고리 수정 |
| DELETE | `/api/admin/categories/<id>/` | 카테고리 삭제 |

### Admin — Portfolio 🔒

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/admin/portfolios/` | 포트폴리오 관리 목록 (`?category`, `?is_active`, `?is_pinned`, `?search`) |
| POST | `/api/admin/portfolios/` | 포트폴리오 생성 (multipart) |
| GET | `/api/admin/portfolios/<id>/` | 포트폴리오 상세 (미디어 포함) |
| PATCH | `/api/admin/portfolios/<id>/` | 포트폴리오 수정 |
| DELETE | `/api/admin/portfolios/<id>/` | 포트폴리오 삭제 |
| POST | `/api/admin/portfolios/<id>/toggle_pinned/` | 고정 상태 토글 |
| POST | `/api/admin/portfolios/<id>/toggle_active/` | 공개 상태 토글 |
| GET | `/api/admin/portfolios/model_usage/` | 현재 사용 중인 3D 모델 목록 |
| POST | `/api/admin/portfolios/<id>/upload_media/` | 미디어 업로드 (자동 타입 감지, 순서 부여) |
| POST | `/api/admin/portfolios/<id>/add_youtube/` | 유튜브 URL 미디어 추가 (`video_url` 파라미터) |
| DELETE | `/api/admin/portfolios/<id>/media/<media_id>/` | 미디어 삭제 |
| POST | `/api/admin/portfolios/<id>/reorder_media/` | 미디어 순서 변경 (`media_ids` 배열) |

### Admin — Lab 🔒

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/admin/lab/` | Lab 프로젝트 목록 (`?is_active`, `?type`, `?search`) |
| POST | `/api/admin/lab/` | Lab 프로젝트 생성 |
| GET | `/api/admin/lab/<id>/` | Lab 프로젝트 상세 |
| PATCH | `/api/admin/lab/<id>/` | Lab 프로젝트 수정 |
| DELETE | `/api/admin/lab/<id>/` | Lab 프로젝트 삭제 |
| POST | `/api/admin/lab/<id>/toggle_active/` | 공개 상태 토글 |

### Admin — Contact 🔒

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/admin/contacts/` | 문의 목록 (`?is_read`, `?search`) |
| GET | `/api/admin/contacts/<id>/` | 문의 상세 |
| DELETE | `/api/admin/contacts/<id>/` | 문의 삭제 |
| POST | `/api/admin/contacts/<id>/mark_read/` | 읽음 처리 |
| POST | `/api/admin/contacts/<id>/mark_unread/` | 읽지 않음 처리 |
| POST | `/api/admin/contacts/mark_all_read/` | 전체 읽음 처리 |
| GET | `/api/admin/contacts/stats/` | 문의 통계 (total, unread, read) |

> 🔒 = `IsAdminUser` 권한 필요 (JWT Bearer 토큰)

---

## 🎯 주요 기능 상세

### 1. 홈페이지 3D 섹션 (ThreeDSection)

약 1,096줄의 Three.js 기반 인터랙티브 3D 씬입니다.

- **6개 포트폴리오 모델**: API에서 `featured` 포트폴리오의 `model_file` 기반으로 동적 로딩
- **중앙 로고 모델**: `logo.glb` 고정 배치
- **Isometric 카메라**: FOV 20으로 외곽 왜곡 최소화
- **무한 바닥**: `field.glb` 외곽이 보이지 않도록 처리
- **조명 시스템**: 중앙 고정 스포트라이트 (로고용) + 마우스 추적 스포트라이트 + 바닥 반사 제거
- **자동 회전**: 모든 포트폴리오 모델 상시 회전 (로고 제외)
- **인터랙션**: 드래그/줌 비활성화, 클릭 시 해당 포트폴리오 상세 페이지 이동

**사용 가능 3D 모델** (`/public/models/`):

| 모델명 | 파일 | 설명 |
|--------|------|------|
| submarine | submarine.glb | 잠수함 |
| arrow | arrow.glb | 화살표 |
| car | car.glb | 자동차 |
| character | character.glb | 캐릭터 |
| stamp | stamp.glb | 도장 |
| ice_cream | ice_cream.glb | 아이스크림 |
| logo | logo.glb | 중앙 로고 (고정, 선택 불가) |
| field | field.glb | 바닥 플랫폼 (자동) |

### 2. 포트폴리오 미디어 시스템

포트폴리오 상세 페이지에서 3가지 타입의 미디어를 지원합니다.

| 미디어 타입 | 업로드 방식 | 설명 |
|------------|-----------|------|
| `image` | `upload_media` (파일 업로드) | 이미지 파일, MIME 자동 감지 |
| `video` | `upload_media` (파일 업로드) | 비디오 파일, MIME 자동 감지 |
| `youtube` | `add_youtube` (URL 전송) | 유튜브 링크 (`video_url` 필드에 저장) |

### 3. 포트폴리오 섹션 (PortfolioSection)

- **카테고리 캐러셀**: 드래그/휠 스크롤 기반 탐색
- **부드러운 스크롤**: `requestAnimationFrame` 기반 이징 처리
- **클라이언트 로고 마퀴**: CSS `@keyframes marquee` 무한 스크롤 (30초 주기)
  - 9개 클라이언트 로고 (LH, SK, 국가유산진흥원, 국립국악원, 부산엑스포, 서울문화재단, 에버랜드, 전주문화재단, 한국중부발전소)
  - 호버 시 일시정지
  - 그레이스케일 → 컬러 전환 효과
  - 좌우 그라데이션 페이드

### 4. 프론트엔드 라우팅

**Public 라우트**:

| 경로 | 페이지 | 설명 |
|------|--------|------|
| `/` | Home | 랜딩 + 3D + 포트폴리오 + 문의 |
| `/about` | About | 회사 소개 |
| `/portfolio` | Portfolio | 전체 포트폴리오 |
| `/portfolio/:id` | PortfolioDetail | 포트폴리오 상세 (이전/다음) |
| `/lab` | Lab | Lab 프로젝트 |
| `/contact` | Contact | 문의 |
| `/category/media-art` | MediaArt | 카테고리: 미디어아트 |
| `/category/interactive` | Interactive | 카테고리: 인터랙티브 |
| `/category/exhibition` | Exhibition | 카테고리: 전시 |
| `/category/web` | Web | 카테고리: 웹 |

**Admin 라우트** (`/admin/*` — `AuthProvider` + `ProtectedLayout(PrivateRoute + AdminLayout)` 래핑):

| 경로 | 페이지 | 설명 |
|------|--------|------|
| `/admin/login` | AdminLogin | 로그인 (레이아웃 없음) |
| `/admin` | AdminDashboard | 대시보드 통계 |
| `/admin/portfolios` | AdminPortfolios | 포트폴리오 목록 |
| `/admin/portfolios/new` | AdminPortfolioEdit | 포트폴리오 생성 |
| `/admin/portfolios/:id/edit` | AdminPortfolioEdit | 포트폴리오 수정 |
| `/admin/categories` | AdminCategories | 카테고리 관리 |
| `/admin/lab` | AdminLab | Lab 목록 |
| `/admin/lab/new` | AdminLabEdit | Lab 생성 |
| `/admin/lab/:id/edit` | AdminLabEdit | Lab 수정 |
| `/admin/contacts` | AdminContacts | 문의 관리 |
| `/admin/*` (기타) | — | `/admin`으로 리다이렉트 |

**레이아웃 분기**: `Home`(`/`)과 `About`(`/about`) 페이지는 상단 패딩 없이 렌더링되며, 나머지 Public 라우트는 `pt-20` 패딩이 적용됩니다.

### 5. Admin 시스템

**Dashboard**: 포트폴리오(total/active/inactive/pinned), 카테고리(total), Lab(total/active/inactive), 문의(total/unread/read) 통계, 최근 문의 5건, 최근 포트폴리오 5건

**Portfolio 관리**: CRUD, 상단 고정 토글, 공개 상태 토글, 3D 모델 선택 (중복 선택 방지 검증), 미디어 업로드/삭제/정렬 (최대 10개), 유튜브 URL 미디어 추가, 3D 모델 사용현황 조회, 카테고리/활성/고정/검색 필터링

**Category 관리**: CRUD, 썸네일/배경색/슬러그 설정

**Lab 관리**: CRUD, 공개 상태 토글, 미디어 타입(이미지/영상) 필터링

**Contact 관리**: 목록 조회, 읽음/안읽음 처리, 전체 읽음, 삭제, 통계, 검색

### 6. Django Admin 인터페이스

Django 내장 Admin 사이트가 커스터마이징되어 있습니다:

- **사이트 헤더**: "OneByOne Studio 관리자"
- **사이트 타이틀**: "OneByOne Admin"
- **인덱스 타이틀**: "대시보드"
- **Portfolio/Category/Lab**: `SortableAdminMixin`(adminsortable2) 기반 드래그 정렬
- **PortfolioMedia**: 인라인 관리 (`SortableInlineAdminMixin`, max 10개)
- **ContactInquiry**: 읽기 전용 (admin에서 직접 추가 불가), 읽음/안읽음 일괄 액션

> ⚠️ **알려진 이슈**: Django Admin의 `PortfolioMediaInline`에 `video_url` 필드가 포함되어 있지 않아 YouTube 타입 미디어를 Django Admin에서 관리할 수 없습니다.

---

## ⚙️ 환경 설정

### 필수 환경변수 (`.env`)

```bash
# Django
SECRET_KEY=your-secret-key
DEBUG=True

# Database
POSTGRES_DB=onebyone
POSTGRES_USER=your-user
POSTGRES_PASSWORD=your-password
POSTGRES_HOST=localhost
POSTGRES_PORT=5432

# AWS S3 (선택)
USE_S3=False
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_STORAGE_BUCKET_NAME=
AWS_S3_REGION_NAME=ap-northeast-2
AWS_CLOUDFRONT_URL=              # 설정 시 S3 대신 CloudFront URL 사용

# Frontend 도메인
REACT_APP_DOMAIN=http://localhost:3000
```

### 파일 업로드 제한

| 설정 | 값 |
|------|-----|
| FILE_UPLOAD_MAX_MEMORY_SIZE | 100MB |
| DATA_UPLOAD_MAX_MEMORY_SIZE | 100MB |
| 포트폴리오 미디어 수 | 최대 10개 |
| 페이지네이션 | 기본 20건 |

### CORS 허용 Origin

- `http://localhost:3000`, `http://127.0.0.1:3000`
- `http://ces2025.iptime.org:30000`
- `https://onebyonestudio.com`, `https://www.onebyonestudio.com`
- `https://main.d2e20hsqeo3cjt.amplifyapp.com`

### CSRF_TRUSTED_ORIGINS

- `http://localhost:3000`
- `http://ces2025.iptime.org:30000`
- `https://onebyonestudio.com`, `https://www.onebyonestudio.com`
- `https://main.d2e20hsqeo3cjt.amplifyapp.com`

### ALLOWED_HOSTS

- `api.onebyonestudio.com`
- `ces2025.iptime.org`
- `localhost`, `127.0.0.1`

### 국제화 및 타임존

| 설정 | 값 |
|------|-----|
| LANGUAGE_CODE | `ko-kr` |
| TIME_ZONE | `Asia/Seoul` |
| USE_I18N | True |
| USE_TZ | True |

### 로깅 설정

`onebyone.log` 파일에 INFO 레벨 이상 기록, 콘솔에 DEBUG 레벨 출력. 로거 네임스페이스: `apps`

---

## 🚀 실행 방법

### Backend (Django)

```bash
cd onebyone-backend

# 의존성 설치
pip install -r requirements.txt

# 마이그레이션
python manage.py makemigrations
python manage.py migrate

# 슈퍼유저 생성
python manage.py createsuperuser

# 개발 서버
python manage.py runserver 0.0.0.0:8000
```

### Backend (Docker)

```bash
docker build -t onebyone-backend .
docker run -p 8000:8000 --env-file .env onebyone-backend
```

### Frontend

```bash
cd src/..  # 프론트엔드 루트

# 의존성 설치
npm install

# 개발 서버
npm run dev

# 프로덕션 빌드
npm run build
```

**API 연결 환경 설정** (`src/api/config.js`):
- Production: `https://api.onebyonestudio.com`
- DDNS 모드 (`REACT_APP_USE_DDNS=true`): `http://ces2025.iptime.org:38000`
- 기본 개발: `http://localhost:8000`

---

## 🔧 버그 수정 내역

### 1. Contact 읽음 처리 POST 미허용
- **파일**: `apps/contact/admin_views.py`
- **원인**: `http_method_names`에 `"post"` 누락
- **해결**: `http_method_names = ["get", "post", "patch", "delete"]` 명시

### 2. Portfolio 500 에러
- **파일**: `apps/portfolio/admin_serializers.py`
- **원인**: `PortfolioMedia`에 존재하지 않는 `created_at` 필드 참조
- **해결**: `PortfolioMediaSerializer`에서 `created_at` 필드 제거

### 3. Admin 필터링 빈 문자열 통과 버그
- **영향**: `contact/admin_views.py`, `portfolio/admin_views.py`, `lab/admin_views.py`
- **원인**: `?is_read=` 빈 문자열이 `is not None` 체크를 통과
- **해결**: `if param in ["true", "false"]:` 명시적 값 검증

```python
# Before (bug)
is_read = request.query_params.get("is_read")
if is_read is not None:
    queryset = queryset.filter(is_read=is_read == "true")

# After (fix)
is_read = request.query_params.get("is_read")
if is_read in ["true", "false"]:
    queryset = queryset.filter(is_read=is_read == "true")
```

---

## 🔮 향후 개선 사항

### 🚨 Critical — 즉시 수정 필요

1. **JWT Blacklist 미동작**: `BLACKLIST_AFTER_ROTATION: True` 설정이나 `rest_framework_simplejwt.token_blacklist`가 `INSTALLED_APPS`에 없음. 이전 Refresh Token이 무효화되지 않아 토큰 탈취 시 보안 취약점 발생.
   - **해결**: `INSTALLED_APPS`에 `"rest_framework_simplejwt.token_blacklist"` 추가 후 `python manage.py migrate` 실행

2. **SECRET_KEY 하드코딩 fallback**: `django-insecure-change-this-in-production` fallback이 존재하여, 환경변수 미설정 시 insecure 키로 실행됨.
   - **해결**: fallback 제거 또는 프로덕션에서 예외 발생하도록 변경

### ⚠️ High — 보안 및 안정성

3. **Dockerfile 프로덕션 최적화**: 현재 `runserver`로 실행 → Gunicorn/uWSGI 전환 필요
4. **DEFAULT_PERMISSION_CLASSES**: 현재 `AllowAny` → 프로덕션에서는 `IsAuthenticated`로 변경 검토
5. **파일 업로드 검증 강화**: 현재 MIME 기반만 → 확장자 화이트리스트, 용량 제한 세분화
6. **유튜브 URL 검증 강화**: 현재 빈 문자열만 체크 → 유효한 유튜브 URL 패턴 검증 추가 필요
7. **SessionAuthentication 제거 검토**: `REST_FRAMEWORK`에 `SessionAuthentication`이 포함되어 있으나 SPA 아키텍처에서는 불필요

### 📋 Medium — 코드 품질

8. **Django Admin PortfolioMediaInline**: `video_url` 필드 누락으로 YouTube 미디어 Django Admin 관리 불가
9. **CategoryAdminViewSet.get_queryset() 카운트 불일치**: 클래스 레벨 queryset은 `is_active=True` 필터, `get_queryset()`은 전체 카운트 반환
10. **api/config.js 미사용 export**: `put` 함수가 export되나 admin.js에서는 `api.patch()` 직접 사용, `patch` 헬퍼 미정의
11. **withCredentials 불일치**: Axios `withCredentials: false` vs Django `CORS_ALLOW_CREDENTIALS = True`
12. **Pagination 일관성**: Admin 리스트 페이지네이션 일관성 검토

### 🎨 Low — 기능 개선

13. **3D 섹션**: 로고 모델 애니메이션 추가, 모바일 터치 인터랙션 개선
14. **Admin**: 포트폴리오 미리보기, 드래그 앤 드롭 정렬
15. **성능**: 3D 모델 Draco 압축, 이미지 WebP 변환, 코드 스플리팅

---

## 📂 전체 파일 변경 내역

### Backend

| 파일 | 변경 내용 |
|------|----------|
| `config/settings.py` | Django 5.x 스토리지 설정, S3/CloudFront, JWT, CORS, 로깅 |
| `config/urls.py` | JWT 인증 + Dashboard + Public/Admin URL 통합, Django Admin 사이트 커스터마이징 |
| `config/views.py` | DashboardStatsView (포트폴리오/카테고리/Lab/문의 통계 + 최근 항목), CurrentUserView |
| `apps/contact/admin_views.py` | 읽음 처리 POST 허용, 빈 문자열 필터 수정, 통계/전체읽음 추가 |
| `apps/portfolio/models.py` | model_file 필드 추가, PortfolioMedia에 youtube 타입 및 video_url 필드 추가 |
| `apps/portfolio/serializers.py` | model_file 필드, video_url 필드, 이전/다음 네비게이션 |
| `apps/portfolio/admin_serializers.py` | model_file 중복 선택 방지 검증, video_url 필드, created_at 제거 |
| `apps/portfolio/admin_views.py` | 미디어 업로드/삭제/정렬, 유튜브 URL 추가(`add_youtube`), 모델 사용현황(`model_usage`), 토글 액션, 빈 문자열 필터 수정 |
| `apps/lab/admin_views.py` | 빈 문자열 필터 수정, toggle_active |

### Frontend

| 파일 | 변경 내용 |
|------|----------|
| `src/api/config.js` | JWT 인터셉터 (자동 갱신), 멀티 환경 URL, get/post/put/del 헬퍼 |
| `src/api/admin.js` | 전체 Admin API 함수 (인증, CRUD, 토글, 미디어, 통계, 유튜브 추가, 모델 사용현황) |
| `src/components/home/ThreeDSection.jsx` | 전면 리뉴얼 (조명, 로고, 카메라, API 연동) — 1,096줄 |
| `src/components/home/PortfolioSection.jsx` | 클라이언트 로고 마퀴 추가 |
| `src/admin/AdminRoutes.jsx` | ProtectedLayout 래핑, 전체 Admin 라우팅, 404 리다이렉트 |
| `src/admin/pages/AdminDashboard.jsx` | Contacts 연동, 최근 항목 |
| `src/admin/pages/AdminContacts.jsx` | URL 파라미터 초기 선택, 읽음/안읽음 토글 |
| `src/admin/pages/AdminPortfolioEdit.jsx` | 3D 모델 선택 UI, 유튜브 미디어 추가 UI |
| `src/admin/pages/AdminCategories.jsx` | 카테고리 CRUD |
| `src/admin/pages/AdminLab.jsx` | Lab 프로젝트 관리 |
| `src/admin/pages/AdminLabEdit.jsx` | Lab 프로젝트 생성/수정 |
| `src/contexts/AuthContext.jsx` | JWT Context (로그인/로그아웃/토큰 관리) |

---

## 📊 코드 분석 및 변경 요약 (2026-03-04 기준)

소스 코드 전수 분석을 통해 이전 README(2026-02-25) 대비 확인된 불일치 및 누락 사항입니다.

### 이전 README 대비 주요 변경점

| # | 항목 | 이전 상태 | 현재 코드 실제 상태 |
|---|------|----------|-------------------|
| 1 | JWT Blacklist | "활성화" 표기 | `token_blacklist` 앱 미등록 — **실제 미동작 (보안 이슈)** |
| 2 | ThreeDSection 줄 수 | "약 1,050줄" | **1,096줄** |
| 3 | PortfolioMedia video_url 형식 | `https://youtu.be/xxxx`만 기재 | `youtube.com/watch?v=` 및 `youtu.be/` **두 형식 모두 지원** |
| 4 | CSRF_TRUSTED_ORIGINS | 미기재 | 5개 Origin 설정 확인 및 문서화 |
| 5 | Django Admin 커스터마이징 | 미기재 | 사이트 헤더/타이틀/인덱스 타이틀 및 Sortable 설정 문서화 |
| 6 | Django Admin PortfolioMediaInline | 미기재 | `video_url` 필드 누락 이슈 문서화 |
| 7 | requirements.txt 패키지 | 일부 간접 의존성 누락 | `botocore`, `s3transfer`, `requests` 등 반영 |
| 8 | CategoryAdminViewSet 카운트 | 미기재 | `get_queryset()` 전체 카운트 vs 클래스 레벨 active 카운트 불일치 문서화 |
| 9 | 국제화/타임존/로깅 | 미기재 | `ko-kr`, `Asia/Seoul`, 파일 로깅 설정 문서화 |
| 10 | Admin 라우트 404 처리 | 미기재 | `Route path="*"` → `/admin` 리다이렉트 문서화 |
| 11 | config.js 헬퍼 불일치 | 미기재 | `put` 미사용, `patch` 미정의 이슈 문서화 |
| 12 | Public Lab API 응답 필드 | 미기재 | 6개 필드만 노출 명시 |
| 13 | Dashboard 통계 상세 | 간략 기재 | 카테고리 통계, 포트폴리오 inactive 포함 명시 |
| 14 | assets 파일 목록 | 미기재 | `logo.avif`, `logo.png`, `smallLogo.avif` |
| 15 | 향후 개선 우선순위 | 평면 나열 | Critical/High/Medium/Low 우선순위 분류 |

---

## 📞 문의

개발 관련 문의사항은 프로젝트 관리자에게 연락 바랍니다.