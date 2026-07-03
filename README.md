# 🏨 Cloud-Based Hotel Reservation System
> **비관적 락(Pessimistic Lock)을 활용한 신뢰성 높은 호텔 예약 플랫폼**
> * 🔗 **라이브 데모:** https://hotel.calmee.store *

<br>

## 📖 프로젝트 소개 (Project Overview)
**호텔 예약 시스템**은 사용자(Guest), 호텔 업주(Owner), 관리자(Admin)를 위한 통합 숙박 예약 플랫폼입니다.
실제 OTA(Online Travel Agency) 서비스의 핵심 기능을 벤치마킹하여 설계되었으며, 특히 동시성 이슈(오버부킹)를 원천 차단하여 데이터 무결성을 보장하는 데 초점을 맞췄습니다.

* **개발 기간:** 2025.10 ~ 2025.11 (약 7주)
* **팀 구성:** 5인 1팀 (팀장: 이준서)

  <br>

## ⚙️ 핵심 기능 (Key Features)

### 1. 예약 안정성 및 동시성 제어 (Concurrency Control)
* [cite_start]**비관적 락(Pessimistic Lock):** 예약 시점의 재고(Inventory) 데이터에 `SELECT FOR UPDATE`를 사용하여 동시 접속 상황에서의 중복 예약을 물리적으로 차단 [cite: 31, 33, 34]
* [cite_start]**Hold & TTL:** 결제 진입 시 임시 점유(Hold) 상태를 생성하고 일정 시간 내 미결제 시 자동 해제하여 재고 누수 방지 [cite: 35, 102]

### 2. 사용자 (User)
* [cite_start]**통합 검색:** 지역/날짜/인원 기반 검색 및 필터링(평점, 가격 등) [cite: 125, 131]
* [cite_start]**예약 및 결제:** 쿠폰 적용 및 토스페이먼츠(Toss) 연동 결제 [cite: 145, 148]
* [cite_start]**마이페이지:** 예약 내역 확인(티켓 출력/PDF 저장), 1:1 문의, 리뷰 관리 [cite: 154, 159, 168]

### 3. 호텔 업주 (Owner)
* [cite_start]**대시보드:** 매출 추이 그래프, 체크인/아웃 현황, 예약 통계 시각화 [cite: 255, 260]
* [cite_start]**PMS (객실 관리):** 캘린더 형태의 객실 재고/가격 관리, 호실 배정 시스템 [cite: 263, 278]
* [cite_start]**리뷰 관리:** 투숙객 리뷰 조회 및 악성 리뷰 신고 기능 [cite: 288]

### 4. 관리자 (Admin)
* [cite_start]**입점 심사:** 호텔 등록 요청에 대한 승인/반려 처리 [cite: 203]
* [cite_start]**정산 시스템:** 수수료 자동 계산, 정산서 생성 및 지급 처리 [cite: 244, 250]
* [cite_start]**CS 관리:** 공지사항, FAQ 관리 및 1:1 문의 답변, 신고된 리뷰 처리 [cite: 221, 227, 215]

<br>

## 🚀 트러블 슈팅 (Troubleshooting)
### 오버부킹(Overbooking) 방지 전략
* **문제:** 인기 있는 호텔 객실의 경우, 다수의 사용자가 동시에 결제를 시도할 때 재고보다 많은 예약이 발생하는 동시성 문제 발생
* **해결:** 데이터베이스 레벨에서 **비관적 락(Pessimistic Lock)**을 적용하여, 한 트랜잭션이 재고를 점유하는 동안 다른 트랜잭션의 접근을 대기시키도록 구현. [cite_start]이를 통해 데이터 정합성을 100% 보장함. [cite: 33, 34]

<br>

## 🧑‍💻 담당 역할 및 기여 (My Contribution)
**이준서 (Team Leader & Full Stack Developer)**
> **"사용자의 관점에서 서비스를 설계하고, 핵심 기술 구현부터 인프라 배포까지 프로젝트 전반을 주도했습니다 아래의 모든 내용들은 제가 진행한 파트들을 정리한 내용들입니다. 전체 프로젝트의 흐름에 대한 내용은 상단의 노션 링크를 참고해주시기 바랍니다."**

### 1. Project Management & Design
* [cite_start]**Team Leading:** 전체 일정 관리, 요구사항 정의, 팀원 간 기술 이슈 조율 및 코드 리뷰 리딩 [cite: 2, 4, 19]
* [cite_start]**User-Centric UX Design:** 사용자 입장에서의 예약 흐름을 시뮬레이션하여 직관적인 UI/UX 프로세스 및 화면 설계 , 요구사항 명세서 및 다이어그램 작성, 기능 요구사항 명세서 작성 [cite: 37-40]
* [cite_start]**Database Modeling:** 사용자, 호텔, 객실, 예약, 결제, 정산 등 전체 서비스의 정규화된 ERD 설계 (MariaDB) [cite: 68-113]

### 2. Key Feature Implementation (Core Logic)
* [cite_start]**Social Login (OAuth 2.0):** Google, Kakao, Naver 3사 OAuth 연동을 통한 간편 로그인 및 회원가입 프로세스 직접 구현 [cite: 59, 121]
* [cite_start]**Location Service:** Kakao Map API를 활용하여 호텔 위치 시각화 및 지도 기반 정보 제공 [cite: 141]
* [cite_start]**Search Engine:** 위치, 날짜, 인원 및 상세 필터(가격, 편의시설, 등급)를 포함한 동적 검색 쿼리 구현 [cite: 131-135]
* [cite_start]**Owner System:** 업주용 대시보드(매출 통계), 예약 캘린더(Drag & Drop 재고 관리) 등 복잡한 비즈니스 로직 구현 [cite: 254-269]

### 3. Security & DevOps
* **Security:** XSS/SQL Injection 방지 및 민감 정보 암호화 적용, JWT 기반 인증 보안 강화
* **Deployment:** Oracle Cloud 환경 구축 및 서버 배포·운영

<br>

## 🛠 기술 스택 (Tech Stack)

| 구분 | 기술 (Technology) |
|:---:|:---|
| **Language & Framework** | Java 17, Spring Boot 3.x, JPA (Hibernate) |
| **Frontend** | HTML5, CSS3, JavaScript, Vue.js (or React/Thymeleaf) |
| **Database** | [cite_start]MariaDB
| **Payment & Map** | [cite_start]Toss Payments API, Kakao Map API [cite: 148, 141] |
| **Auth** | OAuth 2.0 (Google, Kakao, Naver), JWT |
| **Infrastructure** | Oracle Cloud (ARM Compute), Docker, Caddy, Git/GitHub |
| **Tools** | Notion, Figma, IntelliJ IDEA |



## 🗂 데이터베이스 설계 (ERD)
> 데이터 무결성을 최우선으로 고려하여 정규화된 데이터베이스를 설계했습니다.
> (User, Hotel, Room, Booking, Payment, Settlement 등 주요 모듈 분리) [cite_start] https://dbdiagram.io/d/68da7fd9d2b621e422662ea5


<br>

## 📸 프로젝트 스크린샷 (Screenshots)

| **메인 & 검색 (User)** | **호텔 상세 & 지도 (User)** | **지역/날짜/인원 검색 및 추천 호텔** | **Kakao Map API 연동 위치 정보** |

|:---:|:---:|
| ![Main]<img width="1037" height="500" alt="image" src="https://github.com/user-attachments/assets/74157d47-65da-407e-8af3-3f78f917c0c1" />
| ![Detail] <img width="590" height="473" alt="image" src="https://github.com/user-attachments/assets/ab292e9e-0509-49f8-bb45-3bed7d068f60" /> <img width="1064" height="471" alt="image" src="https://github.com/user-attachments/assets/4469ce26-259d-48e7-ae1e-f10f21572541" /> <img width="567" height="474" alt="image" src="https://github.com/user-attachments/assets/6e25e6b2-abda-408a-9827-6566085a0baf" />


| **예약 캘린더 및 예약 내역 (Owner)** | **호실 배정 및 객실관리 (Owner)** |
|:---:|:---:|
| ![Calendar]<img width="1098" height="596" alt="image" src="https://github.com/user-attachments/assets/a025c4c9-1536-4e36-9c0d-c6e62f97fe47" /> <img width="992" height="490" alt="image" src="https://github.com/user-attachments/assets/94c4e868-7484-4c41-9452-e9a0b16b5071" /> <img width="633" height="508" alt="image" src="https://github.com/user-attachments/assets/a7e8c00e-1206-4f3d-bef6-8d1d9ef84415" /> <img width="617" height="498" alt="image" src="https://github.com/user-attachments/assets/6414b537-bf6b-47b1-bb76-568f56ec7df0" />


 | ![management]<img width="1021" height="483" alt="image" src="https://github.com/user-attachments/assets/6a62a4c9-b685-4fe9-88ca-8328c928ba88" /> <img width="1030" height="490" alt="image" src="https://github.com/user-attachments/assets/5e66893d-5fdd-41d3-9240-9e71be2a3394" />

 |


 

<br>

## 📖 License & Reference
* 이 프로젝트는 포트폴리오 목적으로 제작되었습니다.
* 📝 상세 설명: [프로젝트 노션 문서](https://www.notion.so/1-2892245db6a2801f9462ec61b24c29ea)
