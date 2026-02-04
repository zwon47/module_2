# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

시스템 로그를 실시간으로 수집하고 분석하여 시각화하는 웹 기반 어드민 페이지입니다.
React + TypeScript 기반의 Frontend와 Node.js + Express 기반의 Backend로 구성된 풀스택 애플리케이션입니다.

## 기술 스택

- **Frontend**: React 18.2.0, TypeScript 5.0.0, Vite 4.3.0, Tailwind CSS 3.3.0, Recharts 2.5.0
- **Backend**: Node.js 18.16.0, Express 4.18.2, TypeScript 5.0.0
- **Database**: PostgreSQL 15.3
- **DevOps**: Docker 24.0.0, Docker Compose 2.18.0, Nginx 1.24.0

## 아키텍처

### Frontend 구조
- `frontend/src/components/`: 재사용 가능한 React 컴포넌트
- `frontend/src/pages/`: 페이지별 컴포넌트 (라우팅 단위)
- `frontend/src/services/`: Backend API 호출 로직
- `frontend/src/utils/`: 공통 유틸리티 함수

### Backend 구조
- `backend/src/controllers/`: HTTP 요청 처리 및 응답 반환
- `backend/src/routes/`: API 엔드포인트 정의
- `backend/src/services/`: 비즈니스 로직 구현
- `backend/src/models/`: 데이터베이스 모델 정의
- `backend/logs/`: 로그 파일 저장 디렉토리

### 데이터 흐름
1. Frontend에서 API 요청 (services 레이어)
2. Backend의 routes에서 요청 수신
3. Controllers가 요청 파싱 및 검증
4. Services에서 비즈니스 로직 실행
5. Models를 통한 데이터베이스 접근
6. 응답을 Frontend로 반환

## 개발 환경 설정

### 환경 변수

**Backend (.env)**
```
DB_HOST=localhost
DB_PORT=5432
DB_NAME=log_admin
DB_USER=admin
DB_PASSWORD=your_password
PORT=5000
NODE_ENV=development
JWT_SECRET=your_jwt_secret
```

**Frontend (.env)**
```
VITE_API_URL=http://localhost:5000/api
```

### 로컬 개발 서버 실행

```bash
# Backend 개발 서버
cd backend
npm run dev

# Frontend 개발 서버
cd frontend
npm run dev
```

### 데이터베이스 마이그레이션

```bash
cd backend
npm run migrate
```

## 빌드 및 배포

### 개발 빌드
```bash
# Frontend
cd frontend
npm run build

# Backend
cd backend
npm run build
```

### Docker 배포
```bash
# 전체 스택 실행
docker-compose up -d

# 로그 확인
docker-compose logs -f

# 개별 서비스 재시작
docker-compose restart frontend
docker-compose restart backend
```

## 접속 정보

- Frontend: http://localhost:3000
- Backend API: http://localhost:5000
- API 문서: http://localhost:5000/api-docs
- Health Check: http://localhost:5000/health

## 주요 개발 시 고려사항

### TypeScript 사용
- Frontend와 Backend 모두 TypeScript로 작성
- 타입 정의는 명확하게 작성
- `any` 타입 사용 최소화

### API 통신
- Frontend의 services 레이어를 통해 API 호출
- axios 또는 fetch를 일관되게 사용
- 에러 핸들링 및 로딩 상태 관리

### 로그 데이터 처리
- Backend의 `logs/` 디렉토리에 로그 파일 저장
- 로그 파싱 로직은 services 레이어에 구현
- 대용량 로그 처리 시 페이지네이션 및 스트리밍 고려

### 데이터베이스
- PostgreSQL 15.3 사용
- 마이그레이션 파일은 `database/migrations/`에 관리
- 초기 데이터는 `database/seeds/`에 정의

### 인증 및 권한
- JWT 토큰 기반 인증
- 기본 관리자 계정: admin / admin123
- 최초 로그인 후 비밀번호 변경 필수
