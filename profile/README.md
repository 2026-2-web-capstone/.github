# 📚 도서 쇼핑몰 (Bookstore)

도서 판매/구매, 장바구니, 주문, 리뷰, 관리자 기능을 갖춘 **풀스택 도서 쇼핑몰** 프로젝트입니다.

## 프로젝트 구조

```
web-capstone/
├── Backend/     # Spring Boot REST API 서버
├── web/         # React 웹 프론트엔드 (Vite + Tailwind)
├── android/     # React Native/Expo 모바일 앱 (API 연동)
└── mobile/      # React Native/Expo 모바일 앱 (Mock 데이터)
```

## 기술 스택

### Backend
| 기술 | 버전 |
|------|------|
| Java | 21 |
| Spring Boot | 3.2.5 |
| Spring Security | JWT 인증 |
| MySQL | 8.0 |
| Flyway | DB 마이그레이션 |
| AWS S3 | 이미지 업로드 |
| Swagger UI | API 문서 |
| Docker | 배포 |
| Prometheus + Grafana | 모니터링 |

### Web Frontend
| 기술 | 버전 |
|------|------|
| React | 18 |
| Vite | 5 |
| Tailwind CSS | 3 |
| React Router | 6 |
| react-hook-form | 폼 관리 |
| lucide-react | 아이콘 |

### Mobile (android / mobile)
| 기술 | 버전 |
|------|------|
| React Native | 0.81.5 |
| Expo | ~54 |
| React Navigation | Bottom Tabs + Native Stack |
| axios | API 통신 (android만) |
| react-hook-form | 폼 관리 |
| lucide-react-native | 아이콘 |

## 주요 기능

### 사용자
- 회원가입 / 로그인 / 로그아웃 (JWT)
- 도서 목록 조회 (신간, 인기, 카테고리별)
- 도서 검색
- 도서 상세 조회 및 리뷰
- 장바구니 담기 / 수량 변경 / 삭제
- 주문 / 결제 / 취소 / 환불
- 마이페이지 (내 정보, 구매 목록, 내 리뷰)

### 관리자
- 도서 등록 / 수정 / 삭제
- 이미지 업로드 (S3)

## API 엔드포인트

Base URL: `/api/v1`

| 도메인 | 엔드포인트 | 설명 |
|--------|-----------|------|
| **인증** | `POST /users/signup` | 회원가입 |
| | `POST /users/signin` | 로그인 |
| | `POST /users/signout` | 로그아웃 |
| | `GET /users/me` | 내 정보 조회 |
| | `DELETE /users/me` | 회원 탈퇴 |
| **도서** | `GET /home` | 홈 (신간 + 인기) |
| | `GET /books` | 전체 도서 목록 |
| | `GET /books/new` | 신간 도서 |
| | `GET /books/popular` | 인기 도서 |
| | `GET /books/search?keyword=` | 도서 검색 |
| | `GET /books/{bookId}` | 도서 상세 |
| **카테고리** | `GET /categories` | 카테고리 목록 |
| | `GET /categories/{id}/books` | 카테고리별 도서 |
| **장바구니** | `GET /cart` | 장바구니 조회 |
| | `POST /cart/items` | 장바구니 담기 |
| | `DELETE /cart/items/{id}` | 장바구니 삭제 |
| **주문** | `POST /orders` | 주문 생성 |
| | `GET /orders/{orderId}` | 주문 상세 |
| | `POST /orders/{orderId}/cancel` | 주문 취소 |
| | `POST /orders/{orderId}/refund` | 환불 요청 |
| **리뷰** | `GET /books/{bookId}/reviews` | 리뷰 목록 |
| | `POST /books/{bookId}/reviews` | 리뷰 작성 |
| | `DELETE /reviews/{reviewId}` | 리뷰 삭제 |
| **관리자** | `POST /admin/books` | 도서 등록 |
| | `DELETE /admin/books/{bookId}` | 도서 삭제 |
| | `POST /admin/media` | 이미지 업로드 |

## 실행 방법

### Backend

```bash
cd Backend

# MySQL 시작 (Homebrew)
./start-mysql.sh

# DB & 사용자 생성 (최초 1회)
mysql -u root -p
> CREATE DATABASE bookstore CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
> CREATE USER 'bookstore'@'localhost' IDENTIFIED BY 'bookstore1234';
> GRANT ALL PRIVILEGES ON bookstore.* TO 'bookstore'@'localhost';
> FLUSH PRIVILEGES;

# 서버 실행
./gradlew bootRun
```

Swagger UI: http://localhost:8080/swagger-ui.html

### Web

```bash
cd web
npm install
npm run dev
```

http://localhost:5173 에서 확인

### Android (API 연동)

```bash
cd android
npm install
npx expo start
```

에뮬레이터에서 `a` 키로 실행

### Mobile (Mock 데이터)

```bash
cd mobile
npm install
npx expo start
```

## Docker 배포

```bash
cd Backend
docker compose up -d --build
```

| 서비스 | 포트 | 설명 |
|--------|------|------|
| Spring Boot | 8080 | API 서버 |
| MySQL | 3306 | 데이터베이스 |
| Prometheus | 9090 | 메트릭 수집 |
| Grafana | 3000 | 모니터링 대시보드 |

## 화면 구성

### 앱 네비게이션

```
Stack Navigator
├── Main (Tab Navigator)
│   ├── 홈          - 신간/인기 도서
│   ├── 도서        - 전체 도서 목록
│   ├── 장바구니     - 장바구니 관리
│   ├── 마이페이지   - 내 정보/주문/리뷰
│   └── 관리자      - 도서 등록/수정/삭제 (관리자만)
├── BookDetail      - 도서 상세
├── Login           - 로그인
├── Register        - 회원가입
└── Search          - 도서 검색
```

### 웹 라우팅

| 경로 | 페이지 |
|------|--------|
| `/` | 홈 |
| `/books` | 도서 목록 |
| `/books/:id` | 도서 상세 |
| `/search` | 검색 |
| `/login` | 로그인 |
| `/register` | 회원가입 |
| `/cart` | 장바구니 |
| `/mypage` | 마이페이지 |
| `/admin` | 관리자 |

## 프로젝트 비교

| 구분 | Backend | android | mobile | web |
|------|---------|---------|--------|-----|
| 역할 | REST API 서버 | 모바일 앱 | 모바일 앱 | 웹 프론트엔드 |
| 데이터 | MySQL + S3 | API 연동 | Mock 데이터 | Mock 데이터 |
| 인증 | JWT 발급/검증 | API 로그인 | Mock 로그인 | Mock 로그인 |
| 배포 | Docker | Expo | Expo | Vite build |

## 테스트 계정

| 구분 | 이메일 | 비밀번호 |
|------|--------|---------|
| 일반 사용자 | user@example.com | password |
| 관리자 | admin@example.com | password |
