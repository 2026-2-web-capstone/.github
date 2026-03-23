<div align="center">

# 📚 BookStore - 도서 쇼핑몰 프로젝트

<!-- 프로젝트 로고 이미지가 있으면 아래 주석을 해제하고 URL을 교체하세요 -->
<!-- <img src="https://github.com/user-attachments/assets/YOUR_IMAGE_ID" width="200"> -->

도서 판매/구매, 장바구니, 주문, 리뷰, 관리자 기능을 갖춘 풀스택 도서 쇼핑몰 플랫폼

</div>

## 📚 목차
- 홈페이지: https://booksstore.o-r.kr
- [프로젝트 소개](#-프로젝트-소개)
- [기술 스택](#-기술-스택)
- [시스템 아키텍처](#-시스템-아키텍처)
- [기능 구성도](#-기능-구성도)
- [API 명세서](#-api-명세서)
- [코드 저장소](#-코드-저장소)
- [App 설치](#-app-설치)
- [시연 영상](#-시연-영상)
- [작년 우수팀 비교표](#-작년-우수팀-비교표)
- [팀원 소개](#-팀원-소개)

## 🛒 프로젝트 소개

온라인 도서 쇼핑몰로, 사용자에게 편리한 도서 검색 및 구매 경험을 제공하고 관리자에게는 효율적인 도서 관리 도구를 제공합니다.

### 핵심 기능
- 도서 검색 및 카테고리별 조회 (신간 / 인기 / 전체)
- 장바구니 담기 및 주문/결제 시스템
- 도서 리뷰 작성 및 조회
- JWT 기반 사용자 인증 (회원가입/로그인/로그아웃)
- 관리자 도서 등록/삭제 및 이미지 관리 (AWS S3)
- Prometheus + Grafana 기반 서버 모니터링

## 🛠 기술 스택

<details>
<summary>기술 스택 (클릭하면 내용 보입니다)</summary>

### Backend
<img src="https://img.shields.io/badge/Java 21-007396?style=flat&logo=java&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Boot 3.2.5-6DB33F?style=flat&logo=springboot&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Security-6DB33F?style=flat&logo=springsecurity&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Data JPA-6DB33F?style=flat&logo=spring&logoColor=white"/>
<img src="https://img.shields.io/badge/JWT-000000?style=flat&logo=jsonwebtokens&logoColor=white"/>
<img src="https://img.shields.io/badge/Flyway-CC0200?style=flat&logo=flyway&logoColor=white"/>
<img src="https://img.shields.io/badge/Swagger-85EA2D?style=flat&logo=swagger&logoColor=black"/>

### Database & Storage
<img src="https://img.shields.io/badge/MySQL 8.0-4479A1?style=flat&logo=mysql&logoColor=white"/>
<img src="https://img.shields.io/badge/AWS S3-569A31?style=flat&logo=amazons3&logoColor=white"/>

### Web Frontend
<img src="https://img.shields.io/badge/React 18-61DAFB?style=flat&logo=react&logoColor=black"/>
<img src="https://img.shields.io/badge/Vite 5-646CFF?style=flat&logo=vite&logoColor=white"/>
<img src="https://img.shields.io/badge/Tailwind CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white"/>
<img src="https://img.shields.io/badge/React Router 6-CA4245?style=flat&logo=reactrouter&logoColor=white"/>

### Mobile App
<img src="https://img.shields.io/badge/React Native 0.81-61DAFB?style=flat&logo=react&logoColor=black"/>
<img src="https://img.shields.io/badge/Expo 54-000020?style=flat&logo=expo&logoColor=white"/>
<img src="https://img.shields.io/badge/React Navigation-6b52ae?style=flat&logo=react&logoColor=white"/>
<img src="https://img.shields.io/badge/Axios-5A29E4?style=flat&logo=axios&logoColor=white"/>

### DevOps & Monitoring
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white"/>
<img src="https://img.shields.io/badge/GitHub Actions-2088FF?style=flat&logo=githubactions&logoColor=white"/>
<img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white"/>
<img src="https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white"/>

</details>

## 🏗 시스템 아키텍처

<!-- 시스템 아키텍처 이미지가 있으면 아래 주석을 해제하고 URL을 교체하세요 -->
<!-- <img src="https://github.com/user-attachments/assets/YOUR_IMAGE_ID" width="800"> -->

```
┌──────────────────────────────────────────────────────────────┐
│                        Client Layer                          │
│  ┌──────────┐    ┌──────────────┐    ┌────────────────────┐  │
│  │ Web (React│    │ Android (Expo│    │ iOS (Expo)         │  │
│  │ + Vite)  │    │ + Axios)     │    │                    │  │
│  └─────┬────┘    └──────┬───────┘    └────────┬───────────┘  │
│        │                │                     │              │
└────────┼────────────────┼─────────────────────┼──────────────┘
         │   HTTPS/REST   │                     │
         ▼                ▼                     ▼
┌──────────────────────────────────────────────────────────────┐
│                     Server Layer (Docker)                     │
│  ┌──────────────────────────────────────────────────────┐    │
│  │            Spring Boot API (Port 8080)                │    │
│  │  ┌──────────┐ ┌──────────┐ ┌───────────────────────┐ │    │
│  │  │ Security │ │ REST API │ │ Swagger UI            │ │    │
│  │  │ (JWT)    │ │Controller│ │ /swagger-ui.html      │ │    │
│  │  └──────────┘ └──────────┘ └───────────────────────┘ │    │
│  │  ┌──────────┐ ┌──────────┐ ┌───────────────────────┐ │    │
│  │  │ JPA      │ │ Flyway   │ │ Actuator + Micrometer │ │    │
│  │  └────┬─────┘ └──────────┘ └───────────┬───────────┘ │    │
│  └───────┼────────────────────────────────┼─────────────┘    │
│          │                                │                  │
│  ┌───────▼───────┐  ┌────────┐  ┌────────▼──────┐           │
│  │  MySQL 8.0    │  │ AWS S3 │  │  Prometheus   │           │
│  │  (Port 3306)  │  │ Images │  │  (Port 9090)  │           │
│  └───────────────┘  └────────┘  └───────┬───────┘           │
│                                         │                    │
│                                 ┌───────▼───────┐           │
│                                 │   Grafana      │           │
│                                 │  (Port 3000)   │           │
│                                 └───────────────┘           │
└──────────────────────────────────────────────────────────────┘
```

## 💡 기능 구성도

<details>
<summary>기능 구성도 (클릭하면 내용 보입니다)</summary>

```
도서 쇼핑몰
├── 사용자 기능
│   ├── 인증
│   │   ├── 회원가입
│   │   ├── 로그인 (JWT)
│   │   ├── 로그아웃
│   │   └── 회원 탈퇴
│   ├── 도서 조회
│   │   ├── 홈 (신간 + 인기)
│   │   ├── 전체 도서 목록
│   │   ├── 신간 도서
│   │   ├── 인기 도서
│   │   ├── 카테고리별 조회
│   │   ├── 도서 검색
│   │   └── 도서 상세
│   ├── 장바구니
│   │   ├── 장바구니 담기
│   │   ├── 장바구니 조회
│   │   └── 장바구니 삭제
│   ├── 주문/결제
│   │   ├── 장바구니 주문
│   │   ├── 바로 구매
│   │   ├── 주문 상세 조회
│   │   ├── 주문 취소
│   │   └── 환불 요청
│   ├── 리뷰
│   │   ├── 리뷰 목록 조회
│   │   ├── 리뷰 작성
│   │   └── 리뷰 삭제
│   └── 마이페이지
│       ├── 내 정보 조회/수정
│       ├── 주문 내역
│       ├── 구매 목록
│       ├── 환불 목록
│       └── 내 리뷰
└── 관리자 기능
    ├── 도서 등록
    ├── 도서 수정
    ├── 도서 삭제
    └── 이미지 업로드 (S3)
```

</details>

## 📋 API 명세서

<details>
<summary>전체 API 명세 보기 (클릭하면 내용 보입니다)</summary>

Base URL: `/api/v1`

### 👤 인증/회원 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| POST | `/api/v1/users/signup` | 회원가입 | - |
| POST | `/api/v1/users/signin` | 로그인 | - |
| POST | `/api/v1/users/signout` | 로그아웃 | Bearer |
| GET | `/api/v1/users/me` | 내 정보 조회 | Bearer |
| PATCH | `/api/v1/users/me` | 내 정보 수정 | Bearer |
| DELETE | `/api/v1/users/me` | 회원 탈퇴 | Bearer |
| GET | `/api/v1/users/me/orders` | 내 주문 내역 | Bearer |
| GET | `/api/v1/users/me/purchases` | 내 구매 목록 | Bearer |
| GET | `/api/v1/users/me/refunds` | 내 환불 목록 | Bearer |
| GET | `/api/v1/users/me/reviews` | 내 리뷰 목록 | Bearer |

### 📖 도서 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| GET | `/api/v1/home` | 홈 (신간 + 인기) | - |
| GET | `/api/v1/books` | 전체 도서 목록 | - |
| GET | `/api/v1/books/new` | 신간 도서 | - |
| GET | `/api/v1/books/popular` | 인기 도서 | - |
| GET | `/api/v1/books/search?keyword=` | 도서 검색 | - |
| GET | `/api/v1/books/{bookId}` | 도서 상세 | - |

### 📂 카테고리 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| GET | `/api/v1/categories` | 카테고리 목록 | - |
| GET | `/api/v1/categories/{categoryId}/books` | 카테고리별 도서 | - |

### 🛒 장바구니 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| GET | `/api/v1/cart` | 장바구니 조회 | Bearer |
| POST | `/api/v1/cart/items` | 장바구니 담기 | Bearer |
| DELETE | `/api/v1/cart/items/{cartItemId}` | 장바구니 삭제 | Bearer |

### 📦 주문 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| POST | `/api/v1/orders` | 장바구니 주문 | Bearer |
| POST | `/api/v1/orders/direct` | 바로 구매 | Bearer |
| GET | `/api/v1/orders/{orderId}` | 주문 상세 | Bearer |
| POST | `/api/v1/orders/{orderId}/cancel` | 주문 취소 | Bearer |
| POST | `/api/v1/orders/{orderId}/refund` | 환불 요청 | Bearer |

### ⭐ 리뷰 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| GET | `/api/v1/books/{bookId}/reviews` | 리뷰 목록 | - |
| POST | `/api/v1/books/{bookId}/reviews` | 리뷰 작성 | Bearer |
| PATCH | `/api/v1/reviews/{reviewId}` | 리뷰 수정 | Bearer |
| DELETE | `/api/v1/reviews/{reviewId}` | 리뷰 삭제 | Bearer |

### 🔧 관리자 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| POST | `/api/v1/admin/books` | 도서 등록 | Bearer (ADMIN) |
| PATCH | `/api/v1/admin/books/{bookId}` | 도서 수정 | Bearer (ADMIN) |
| DELETE | `/api/v1/admin/books/{bookId}` | 도서 삭제 | Bearer (ADMIN) |
| POST | `/api/v1/admin/media` | 이미지 업로드 | Bearer (ADMIN) |

### 🖼 미디어 API

| Method | URI | Description | Auth |
|--------|-----|-------------|------|
| GET | `/api/v1/media/{mediaId}` | 이미지 조회 | - |

</details>

## 📁 코드 저장소

- [Spring Backend](https://github.com/2026-2-web-capstone/Backend)
- [React Web Frontend](https://github.com/2026-2-web-capstone/web)
- [Android App](https://github.com/2026-2-web-capstone/android)
- [iOS App](https://github.com/2026-2-web-capstone/mobile)

## 📲 App 설치

- [AppStore]
- [GooglePlay]

## 🎥 시연 영상

- [웹 시연영상](https://youtu.be/WWsBcoMzGnw)
- [Android 시연영상](https://youtu.be/2Y3XVmpbMD0)
- [iOS 시연영상](https://www.youtube.com/watch?v=taRLrG_HhLY)

## 📊 작년 우수팀 비교표

|  | BookStore | 최우수 | 우수1 | 우수2 | 우수3 |
|------|--------|---------|---------|---------|---------|
| Code | ✅ | ✅ | ✅ | ✅ | ✅ |
| Doc | ✅ | ✅ | ✅ | ❌ | ✅ |
| 영상 | ✅ | ✅ | ❌ | ❌ | ❌ |
| 화면 | W,A,I | R | R | R | R |
| AppStore/GooglePlay | ✅ | ❌ | ❌ | ❌ | ❌ |

최우수 : https://github.com/capstone-aloha</br>
우수1 : https://github.com/TeamCookCaps</br>
우수2 : https://github.com/godi00/capstone</br>
우수3 : https://github.com/Capic2024/server-flask

## 👥 팀원 소개

<!-- 팀원 정보를 아래 표에 입력하세요 -->
| 역할 | 이름 | GitHub |
|------|------|--------|
| 백엔드 | 신정호 | https://github.com/hoya04 |
| 웹 프론트엔드 | 박세웅 | https://github.com/hardwoong |
| Android | 윤예진 | https://github.com/nyun-nye |
| iOS | 구혁모 | https://github.com/9hkmo |

<div align="center">
Copyright © 2026 BookStore. All rights reserved.
</div>
