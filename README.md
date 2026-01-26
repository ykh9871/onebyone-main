# OneByOne Studio 웹 프로젝트 요약

> 최종 업데이트: 2025년 1월 26일

---

## 📌 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | OneByOne Studio 웹사이트 |
| **목적** | 미디어아트 스튜디오 포트폴리오 및 회사 소개 웹사이트 |
| **Frontend** | http://ces2025.iptime.org:30000 |
| **Backend API** | http://ces2025.iptime.org:38000 |
| **구조** | Git Submodule (Frontend + Backend 분리) |

---

## 🛠 기술 스택

### Frontend
| 기술 | 버전/설명 |
|------|----------|
| React | 18.x |
| Vite | 빌드 도구 |
| React Router | 라우팅 |
| Tailwind CSS | 스타일링 |
| Three.js | 3D 렌더링 |
| @react-three/fiber | React Three.js 래퍼 |
| @react-three/drei | Three.js 헬퍼 |
| Axios | HTTP 클라이언트 |

### Backend
| 기술 | 버전/설명 |
|------|----------|
| Python | 3.11+ |
| Django | 4.x |
| Django REST Framework | API 구축 |
| PostgreSQL | 데이터베이스 |
| Docker | 컨테이너화 |
| Gunicorn | WSGI 서버 |

---

## 📁 프로젝트 구조

```
onebyone-studio/
├── frontend/
│   ├── public/
│   │   ├── models/          # 3D GLB 모델 파일
│   │   │   ├── field.glb
│   │   │   ├── logo.glb
│   │   │   ├── submarine.glb
│   │   │   ├── arrow.glb
│   │   │   ├── car.glb
│   │   │   ├── character.glb
│   │   │   ├── stamp.glb
│   │   │   └── ice_cream.glb
│   │   └── images/
│   │       └── logo/        # 클라이언트 로고
│   │           ├── LH.png
│   │           ├── sk.png
│   │           ├── 국가유산진흥원.png
│   │           ├── 국립국악원.png
│   │           ├── 부산엑스포.png
│   │           ├── 서울문화재단.png
│   │           ├── 에버랜드.png
│   │           ├── 전주문화재단.png
│   │           └── 한국중부발전소.png
│   └── src/
│       ├── api/             # API 통신
│       ├── components/
│       │   └── home/
│       │       ├── ThreeDSection.jsx
│       │       └── PortfolioSection.jsx
│       ├── admin/
│       │   └── pages/
│       │       ├── AdminDashboard.jsx
│       │       ├── AdminContacts.jsx
│       │       └── AdminPortfolioEdit.jsx
│       └── pages/
│
└── backend/
    └── apps/
        ├── contact/
        │   ├── models.py
        │   ├── admin_views.py
        │   └── admin_serializers.py
        ├── portfolio/
        │   ├── models.py
        │   ├── serializers.py
        │   ├── admin_views.py
        │   └── admin_serializers.py
        └── lab/
            └── admin_views.py
```

---

## 🎯 주요 기능

### 1. 홈페이지 3D 섹션 (ThreeDSection)

#### 구현 내용
- **6개 포트폴리오 모델** - 플랫폼 위에 3D 모델 배치
- **중앙 로고 모델** - `logo.glb` 표시
- **Isometric 카메라** - FOV 20으로 외곽 왜곡 최소화
- **무한 바닥** - Field 외곽이 보이지 않도록 처리
- **조명 시스템**
  - 중앙 고정 스포트라이트 (로고용)
  - 마우스 따라다니는 스포트라이트
  - 바닥 조명 반사 제거
- **상시 회전** - 모든 포트폴리오 모델 자동 회전 (로고 제외)
- **인터랙션** - 드래그/줌 비활성화, 클릭으로 포트폴리오 이동

#### 사용 가능한 3D 모델
| 모델명 | 파일 | 설명 |
|--------|------|------|
| submarine | submarine.glb | 잠수함 |
| arrow | arrow.glb | 화살표 |
| car | car.glb | 자동차 |
| character | character.glb | 캐릭터 |
| stamp | stamp.glb | 도장 |
| ice_cream | ice_cream.glb | 아이스크림 |
| logo | logo.glb | 중앙 로고 (고정) |

### 2. 포트폴리오 섹션 (PortfolioSection)

#### 구현 내용
- **카테고리 캐러셀** - 드래그/휠 스크롤로 탐색
- **부드러운 스크롤** - requestAnimationFrame 기반 이징
- **클라이언트 로고 마퀴** - 무한 스크롤 애니메이션
  - 9개 클라이언트 로고
  - 호버 시 일시정지
  - 그레이스케일 → 컬러 전환 효과

### 3. Admin 시스템

#### Dashboard
- 통계 카드 (포트폴리오, 문의, 카테고리)
- 최근 문의 목록 (읽음/안읽음 표시)
- 문의 클릭 시 AdminContacts로 이동 (선택 상태 유지)

#### Portfolio 관리
- CRUD 기능
- 상단 고정 (is_pinned) 기능
- **3D 모델 선택** - 상단 고정 시 3D 모델 지정 가능

#### Contact 관리
- 문의 목록 조회
- 읽음 처리 (POST 요청)
- URL 파라미터로 초기 선택 처리

---

## 🔧 버그 수정 내역

### 1. Contact 읽음 처리 버그
- **파일**: `backend/apps/contact/admin_views.py`
- **문제**: POST 메서드가 허용되지 않음
- **해결**: `http_method_names`에 "post" 추가

### 2. Portfolio 500 에러
- **파일**: `backend/apps/portfolio/admin_serializers.py`
- **문제**: PortfolioMedia에 없는 created_at 필드 참조
- **해결**: PortfolioMediaSerializer에서 created_at 제거

### 3. Admin 필터링 빈 문자열 버그
- **영향 파일**:
  - `backend/apps/contact/admin_views.py`
  - `backend/apps/portfolio/admin_views.py`
  - `backend/apps/lab/admin_views.py`
- **문제**: `?is_read=` 빈 문자열이 `is not None` 통과
- **해결**: `if param in ["true", "false"]:` 명시적 체크

```python
# 수정 전
is_read = request.query_params.get("is_read")
if is_read is not None:
    queryset = queryset.filter(is_read=is_read == "true")

# 수정 후
is_read = request.query_params.get("is_read")
if is_read in ["true", "false"]:
    queryset = queryset.filter(is_read=is_read == "true")
```

---

## ✨ 신규 기능

### 1. 포트폴리오별 3D 모델 선택

#### Backend 변경
```python
# backend/apps/portfolio/models.py
MODEL_FILE_CHOICES = [
    ("", "선택 안함"),
    ("submarine", "Submarine (잠수함)"),
    ("arrow", "Arrow (화살표)"),
    ("car", "Car (자동차)"),
    ("character", "Character (캐릭터)"),
    ("stamp", "Stamp (도장)"),
    ("ice_cream", "Ice Cream (아이스크림)"),
]

model_file = models.CharField(
    "3D 모델", max_length=20, blank=True, default="",
    choices=MODEL_FILE_CHOICES,
)
```

#### Frontend 변경
- Admin에서 상단 고정 체크 시 3D 모델 선택 드롭다운 표시
- ThreeDSection에서 `model_file` 기반 모델 로딩

### 2. 클라이언트 로고 마퀴
- 무한 CSS 애니메이션 (`@keyframes marquee`)
- 30초 주기 반복
- 좌우 그라데이션 페이드

---

## 🗄 데이터베이스 마이그레이션

### 필수 실행 명령어
```bash
# Docker 환경
docker-compose exec backend python manage.py makemigrations portfolio
docker-compose exec backend python manage.py migrate

# 직접 실행
python manage.py makemigrations portfolio
python manage.py migrate
```

### 추가된 필드
| 앱 | 모델 | 필드 | 타입 |
|----|------|------|------|
| portfolio | Portfolio | model_file | CharField(max_length=20) |

---

## 📝 API 엔드포인트

### Public API
| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | /api/portfolios/ | 포트폴리오 목록 |
| GET | /api/portfolios/featured/ | 상단 고정 포트폴리오 |
| GET | /api/portfolios/{id}/ | 포트폴리오 상세 |
| GET | /api/categories/ | 카테고리 목록 |
| POST | /api/contact/ | 문의 등록 |

### Admin API
| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | /api/admin/dashboard/ | 대시보드 통계 |
| GET | /api/admin/portfolios/ | 포트폴리오 관리 목록 |
| POST | /api/admin/portfolios/ | 포트폴리오 생성 |
| PUT | /api/admin/portfolios/{id}/ | 포트폴리오 수정 |
| DELETE | /api/admin/portfolios/{id}/ | 포트폴리오 삭제 |
| GET | /api/admin/contacts/ | 문의 관리 목록 |
| POST | /api/admin/contacts/{id}/read/ | 문의 읽음 처리 |

---

## 🚀 배포 체크리스트

### Backend
- [ ] 마이그레이션 실행
- [ ] 정적 파일 수집 (`collectstatic`)
- [ ] 서버 재시작

### Frontend
- [ ] 3D 모델 파일 확인 (`/public/models/`)
- [ ] 클라이언트 로고 파일 확인 (`/public/images/logo/`)
- [ ] 빌드 (`npm run build`)
- [ ] 배포

---

## 📂 수정된 파일 목록

### Backend
| 파일 | 변경 내용 |
|------|----------|
| apps/contact/admin_views.py | 읽음 처리 POST 허용, 빈 문자열 필터 수정 |
| apps/portfolio/models.py | model_file 필드 추가 |
| apps/portfolio/serializers.py | model_file 필드 추가 |
| apps/portfolio/admin_serializers.py | model_file 필드 추가, created_at 제거 |
| apps/portfolio/admin_views.py | 빈 문자열 필터 수정 |
| apps/lab/admin_views.py | 빈 문자열 필터 수정 |

### Frontend
| 파일 | 변경 내용 |
|------|----------|
| src/components/home/ThreeDSection.jsx | 전면 리뉴얼 (조명, 로고, 카메라 등) |
| src/components/home/PortfolioSection.jsx | 클라이언트 로고 마퀴 추가 |
| src/admin/pages/AdminDashboard.jsx | Contacts 연동 |
| src/admin/pages/AdminContacts.jsx | URL 파라미터 초기 선택 |
| src/admin/pages/AdminPortfolioEdit.jsx | 3D 모델 선택 UI |

---

## 🔮 향후 개선 사항

1. **3D 섹션**
   - 로고 모델 애니메이션 추가
   - 모바일 터치 인터랙션 개선

2. **Admin**
   - 포트폴리오 미리보기 기능
   - 드래그 앤 드롭 정렬

3. **성능**
   - 3D 모델 압축 (Draco)
   - 이미지 최적화 (WebP)
   - 코드 스플리팅

---

## 📞 문의

개발 관련 문의사항은 프로젝트 관리자에게 연락 바랍니다.