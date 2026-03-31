# EveryHealth

건강한 생활 습관 형성을 돕는 건강 관리 웹 애플리케이션입니다.  
운동 기록, 식단 관리, 신체 측정, 커뮤니티 기능을 통해 사용자의 건강 목표 달성을 지원합니다.

---

## 주요 기능

| 기능 | 설명 |
|------|------|
| 회원 관리 | 회원가입, 로그인, 비밀번호 변경, 이메일 찾기 |
| 운동 기록 | 날짜별 운동 종목 및 세트/횟수 기록, 운동 가이드 GIF 제공 |
| 식단 기록 | 날짜별 식단 및 칼로리 기록 |
| 신체 측정 | 날짜별 체중, 체지방률 등 신체 지표 기록 |
| 커뮤니티 | 게시글 작성/수정/삭제, 이미지 첨부, 내가 쓴 글 조회 |
| 운동 프로그램 | 추천 운동 루틴 및 프로그램 참고 |

---

## 기술 스택

### Backend
- Java 21
- Spring Boot 3.3.5
- Spring Security + JWT (Access Token / Refresh Token)
- Spring Data JPA (Hibernate)
- MySQL
- Gradle

### Frontend
- Vue 3
- Vue Router 4
- Axios
- v-calendar

---

## 프로젝트 구조

```
EveryHealth/
├── src/
│   └── main/
│       ├── java/com/example/EveryHealth/
│       │   ├── controller/     # REST API 컨트롤러
│       │   ├── service/        # 비즈니스 로직
│       │   ├── entity/         # JPA 엔티티
│       │   ├── repository/     # Spring Data 레포지토리
│       │   ├── dto/            # 데이터 전송 객체
│       │   └── security/       # JWT 인증 필터 및 설정
│       └── resources/
│           ├── application.yml # 애플리케이션 설정
│           └── static/         # 빌드된 Vue 정적 파일 (Spring Boot가 서빙)
└── frontend/
    └── src/
        ├── components/         # Vue 컴포넌트
        ├── router/             # Vue Router 설정
        └── assets/             # 이미지, 아이콘
```

---

## 환경 설정 및 실행 방법

### 1. 사전 준비
- Java 21
- Node.js 18+
- MySQL 8.0+

### 2. 데이터베이스 생성

```sql
CREATE DATABASE DB_Project CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'your_username'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON DB_Project.* TO 'your_username'@'localhost';
```

### 3. 환경변수 설정

`.env.example`을 참고하여 환경변수를 설정합니다.

**IntelliJ IDEA 사용 시**: Run/Debug Configurations → Environment variables에 아래 항목 추가

```
DB_URL=jdbc:mysql://localhost:3306/DB_Project
DB_USERNAME=your_db_username
DB_PASSWORD=your_db_password
JWT_SECRET=your_jwt_secret_key
```

**터미널 사용 시**:
```bash
export DB_URL=jdbc:mysql://localhost:3306/DB_Project
export DB_USERNAME=your_db_username
export DB_PASSWORD=your_db_password
export JWT_SECRET=your_jwt_secret_key
```

### 4. 백엔드 실행

```bash
# 프로젝트 루트에서
./gradlew bootRun
```

서버는 `http://localhost:8081`에서 실행됩니다.

### 5. 프론트엔드 개발 서버 실행 (선택)

```bash
cd frontend
npm install
npm run serve
```

> 프론트엔드 빌드 결과물은 이미 `src/main/resources/static/`에 포함되어 있으므로,  
> 백엔드만 실행해도 `http://localhost:8081`에서 서비스를 이용할 수 있습니다.

---

## API 엔드포인트

| Method | Endpoint | 설명 |
|--------|----------|------|
| POST | `/user/save` | 회원가입 |
| POST | `/user/login` | 로그인 |
| GET | `/user/mypage` | 마이페이지 조회 |
| PUT | `/user/change-password` | 비밀번호 변경 |
| GET | `/user/find-email` | 이메일 찾기 |
| POST | `/token/refresh` | Access Token 재발급 |
| GET | `/body/list` | 신체 기록 목록 조회 |
| POST | `/body/save` | 신체 기록 저장 |
| GET | `/diet/list` | 식단 기록 목록 조회 |
| POST | `/diet/save` | 식단 기록 저장 |
| GET | `/exercise/list` | 운동 기록 목록 조회 |
| POST | `/exercise/save` | 운동 기록 저장 |
| GET | `/board/list` | 게시글 목록 조회 |
| POST | `/board/save` | 게시글 작성 |
| GET | `/board/{id}` | 게시글 상세 조회 |
| PUT | `/board/update/{id}` | 게시글 수정 |
| DELETE | `/board/delete/{id}` | 게시글 삭제 |
