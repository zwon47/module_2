# 시스템 로그 분석 웹 어드민

## 프로젝트 개요

시스템 로그를 실시간으로 수집하고 분석하여 시각화하는 웹 기반 어드민 페이지입니다.
로그 데이터의 검색, 필터링, 통계 분석 기능을 제공하며, 관리자가 시스템 상태를 모니터링하고 이상 징후를 빠르게 파악할 수 있도록 지원합니다.

## 기술 스택

### Frontend
- React: 18.2.0
- TypeScript: 5.0.0
- Vite: 4.3.0
- Tailwind CSS: 3.3.0
- Recharts: 2.5.0

### Backend
- Node.js: 18.16.0
- Express: 4.18.2
- TypeScript: 5.0.0
- PostgreSQL: 15.3

### DevOps
- Docker: 24.0.0
- Docker Compose: 2.18.0
- Nginx: 1.24.0

## 디렉토리 구조

```
module_2/
├── frontend/                 # 프론트엔드 애플리케이션
│   ├── src/
│   │   ├── components/      # React 컴포넌트
│   │   ├── pages/           # 페이지 컴포넌트
│   │   ├── services/        # API 서비스
│   │   ├── utils/           # 유틸리티 함수
│   │   └── App.tsx          # 메인 앱 컴포넌트
│   ├── public/              # 정적 파일
│   └── package.json
│
├── backend/                  # 백엔드 API 서버
│   ├── src/
│   │   ├── controllers/     # 컨트롤러
│   │   ├── models/          # 데이터 모델
│   │   ├── routes/          # API 라우트
│   │   ├── services/        # 비즈니스 로직
│   │   └── app.ts           # Express 앱
│   ├── logs/                # 로그 파일 저장
│   └── package.json
│
├── database/                 # 데이터베이스 관련
│   ├── migrations/          # DB 마이그레이션
│   └── seeds/               # 초기 데이터
│
├── docker/                   # Docker 설정
│   ├── frontend/
│   ├── backend/
│   └── nginx/
│
├── docker-compose.yml        # Docker Compose 설정
└── README.md                 # 프로젝트 문서
```

## 포팅 메뉴얼

### 1. 사전 요구사항

- Node.js 18.16.0 이상
- Docker 24.0.0 이상
- Docker Compose 2.18.0 이상
- PostgreSQL 15.3 이상 (Docker 사용 시 불필요)

### 2. 환경 설정

#### 환경 변수 설정

**Backend (.env)**
```bash
# 데이터베이스
DB_HOST=localhost
DB_PORT=5432
DB_NAME=log_admin
DB_USER=admin
DB_PASSWORD=your_password

# 서버
PORT=5000
NODE_ENV=production

# JWT
JWT_SECRET=your_jwt_secret
```

**Frontend (.env)**
```bash
VITE_API_URL=http://localhost:5000/api
```

### 3. 로컬 개발 환경 설치

#### 3.1 저장소 클론 및 의존성 설치

```bash
# 의존성 설치
# Frontend
cd frontend
npm install

# Backend
cd ../backend
npm install
```

#### 3.2 데이터베이스 설정

```bash
# PostgreSQL 데이터베이스 생성
createdb log_admin

# 마이그레이션 실행
cd backend
npm run migrate
```

#### 3.3 개발 서버 실행

```bash
# Backend 서버 실행 (터미널 1)
cd backend
npm run dev

# Frontend 서버 실행 (터미널 2)
cd frontend
npm run dev
```

### 4. Docker를 이용한 배포

#### 4.1 Docker Compose로 전체 스택 실행

```bash
# 컨테이너 빌드 및 실행
docker-compose up -d

# 로그 확인
docker-compose logs -f
```

#### 4.2 개별 서비스 재시작

```bash
# Frontend 재시작
docker-compose restart frontend

# Backend 재시작
docker-compose restart backend
```

### 5. 프로덕션 빌드

#### 5.1 Frontend 빌드

```bash
cd frontend
npm run build
```

#### 5.2 Backend 빌드

```bash
cd backend
npm run build
```

### 6. 접속 정보

- Frontend: http://localhost:3000
- Backend API: http://localhost:5000
- 기본 관리자 계정: admin / admin123 (최초 로그인 후 비밀번호 변경 필요)

### 7. 트러블슈팅

#### 포트 충돌 시
```bash
# 사용 중인 포트 확인
netstat -ano | findstr :3000
netstat -ano | findstr :5000

# docker-compose.yml에서 포트 변경
```

#### 데이터베이스 연결 오류 시
```bash
# 데이터베이스 컨테이너 상태 확인
docker-compose ps

# 데이터베이스 로그 확인
docker-compose logs postgres
```

### 8. 추가 정보

- API 문서: http://localhost:5000/api-docs (Swagger)
- 모니터링: http://localhost:5000/health
