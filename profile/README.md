<div align="center">

# 📚 BookStore - 도서 쇼핑몰 프로젝트

<!-- 프로젝트 로고 이미지가 있으면 아래 주석을 해제하고 URL을 교체하세요 -->
<!-- <img src="https://github.com/user-attachments/assets/YOUR_IMAGE_ID" width="200"> -->

도서 판매/구매, 장바구니, 주문, 리뷰, 관리자 기능을 갖춘 풀스택 도서 쇼핑몰 플랫폼

</div>

## 📖 목차

- [🎯 프로젝트 소개](#-프로젝트-소개)
- [🏠 홈페이지](#-홈페이지)
- [📌 기능 구성도](#-기능-구성도)
- [📌 API 명세서](#-api-명세서)
- [💻 코드](#-코드)
- [📱 App 설치](#-app-설치)
- [🎬 시연 동영상](#-시연-동영상)
- [🏆 작년 우수팀과의 비교표](#-작년-우수팀과의-비교표)
- [👥 팀원 소개](#-팀원-소개)

## 🎯 프로젝트 소개

온라인 도서 쇼핑몰로, 사용자에게 편리한 도서 검색 및 구매 경험을 제공하고 관리자에게는 효율적인 도서 관리 도구를 제공합니다.

### 핵심 기능
- 도서 검색 및 카테고리별 조회 (신간 / 인기 / 전체)
- 장바구니 담기 및 주문/결제 시스템
- 도서 리뷰 작성 및 조회
- JWT 기반 사용자 인증 (회원가입/로그인/로그아웃)
- 관리자 도서 등록/삭제 및 이미지 관리 (AWS S3)
- **Android, iOS, 데스크탑** 모두에서 사용 가능 – 크로스플랫폼 지원

## 🏠 홈페이지

https://web-tau-ten-59.vercel.app/

## 📌 기능 구성도

<details>
<summary>기능 구성도 보기</summary>

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

## 📌 API 명세서

<details>
<summary>API 명세서 보기</summary>

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

## 💻 코드

[🔗 백엔드](https://github.com/2026-2-web-capstone/Backend)
[🔗 리액트](https://github.com/2026-2-web-capstone/web)
[🔗 안드로이드](https://github.com/2026-2-web-capstone/android)
[🔗 아이폰](https://github.com/2026-2-web-capstone/mobile)

## 📱 App 설치

[🔗 안드로이드]
[[🔗 아이폰](https://testflight.apple.com/join/T15w35Pe)]

## 🎬 시연 동영상

- [리액트(PC) 시연 영상](https://youtu.be/tdA5p82Bdbk)
- [리액트(모바일) 시연 영상](https://youtu.be/HaC7KlDspks)
- [Android 시연영상](https://youtu.be/2Y3XVmpbMD0)
- [iOS 시연영상](https://youtube.com/shorts/DwBnLXyKG1Q?feature=share)

## 🏆 작년 우수팀과의 비교표

| 항목 | BookStore | 최우수 | 우수1 | 우수2 | 우수3 |
|------|-----------|--------|-------|-------|-------|
| Code | ✅ | ✅ | ✅ | ✅ | ✅ |
| Doc | ✅ | ✅ | ✅ | ❌ | ✅ |
| 영상 | ✅ | ✅ | ✅ | ❌ | ✅ |
| 화면 | W, A, I | R | R | R | R |
| AppStore/GooglePlay | ✅ | ❌ | ❌ | ❌ | ❌ |

최우수 : 황치즈 https://github.com/HwangCheese/VideoSummary<br>
우수1 : 황금토끼 https://github.com/GolddBunny/Domain_QA_Gen<br>
우수2 : 초신성 https://github.com/kola0709/2025Capstone/tree/master (작품설명 없음)<br>
우수3 : Prism https://github.com/hsu-capstone-prism/DamSeol

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
