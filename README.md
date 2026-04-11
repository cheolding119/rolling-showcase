## 서비스 소개

Rolling은 흩어져 있는 주짓수 오픈매트 정보와 대회 정보를 한곳에서 모아 보여주는 서비스입니다.  
사용자는 지역과 일정 기준으로 정보를 탐색하고, 오픈매트 신청, 공지 확인, 알림 확인, 문의 등록까지 앱 안에서 처리할 수 있습니다.

주짓수 커뮤니티에서는 오픈매트 공지와 대회 정보가 주로 인스타그램 스토리, 단체 채팅방, 외부 사이트, 개별 게시물처럼 여러 채널에 흩어져 있어 필요한 정보를 제때 찾기 어렵다는 문제가 있었습니다.  
특히 지역별로 어떤 오픈매트가 열리는지, 참가 가능한 대회가 무엇인지 한눈에 비교하기 어려워 사용자는 반복적으로 여러 채널을 확인해야 했습니다.

Rolling은 이런 비효율을 줄이기 위해 오픈매트와 대회 정보를 한곳에 모아 탐색, 신청, 알림 확인까지 이어지는 흐름을 하나의 서비스로 통합했습니다.  
단순한 정보 나열이 아니라 실제 참여 행동까지 연결되는 구조를 목표로 했고, 사용자용 Flutter 앱과 운영용 React 관리자 페이지를 함께 구성해 확장 가능한 서비스 형태로 설계했습니다.

---

## 팀 / 역할

| 이름 | 역할 |
| --- | --- |
| 정원철  | 1인 개발로 서비스 기획부터 UI 설계, Flutter 앱 개발, React 관리자 페이지 개발, Spring 백엔드 API 개발, 데이터베이스 설계, 배포/모니터링 구조 설계까지 전 과정을 직접 수행 |

---

## 문제 정의

- 오픈매트 공지와 대회 정보가 SNS, 커뮤니티, 외부 사이트에 흩어져 있어 한눈에 확인하기 어렵습니다.
- 지역과 일정 기준으로 필요한 정보를 빠르게 탐색하기 어려워 사용자 탐색 비용이 큽니다.
- 정보 확인 이후 참가 신청, 변경사항 확인, 문의 처리까지의 흐름이 분리되어 있어 사용성이 떨어집니다.
- 초기에는 단일 API 서버 중심으로 시작했지만, 서비스가 커지면서 관리자 페이지, 랜딩 페이지, 운영 모니터링, 배포 자동화까지 함께 고려해야 했습니다.


---


## 해결 방식

- 오픈매트와 대회 정보를 하나의 앱 안에서 통합 조회할 수 있도록 구성했습니다.
- 지역, 일정, 상태 중심으로 정보를 탐색할 수 있게 해 사용자 탐색 비용을 줄였습니다.
- 신청, 알림, 공지, 문의 기능을 함께 제공해 정보 확인 이후의 행동까지 하나의 흐름으로 연결했습니다.
- 사용자 앱과 관리자 웹을 분리하고, `Nginx` + `Docker Compose` 기반 라우팅 및 배포 구조를 구성해 운영 확장성을 확보했습니다.
- `Prometheus`, `Grafana`, `Slack Webhook`, `Actuator` 기반 운영 관측 체계를 도입해 프로덕션 대응 기반을 마련했습니다.

---

## 핵심 기능

- 오픈매트 목록 조회 및 상세 확인
- 오픈매트 신청 및 취소
- 내가 신청한 오픈매트 / 내가 개최한 오픈매트 관리
- 대회 목록 조회 및 상세 확인
- 공지사항 조회
- 앱 내 알림 확인
- 1:1 문의 등록 및 답변 확인
- 관리자 전용 운영 기능
  공지 운영, 문의 답변, 신고 처리, 대회 크롤링 실행

## 사용자 흐름

1. 사용자가 Google 또는 Kakao 소셜 로그인으로 앱에 진입한다.
2. 오픈매트 / 대회 정보를 지역과 일정 기준으로 탐색한다.
3. 원하는 오픈매트에 참가 신청한다.
4. 공지사항과 알림을 통해 변경사항을 확인한다.
5. 필요하면 문의를 남기고 답변을 확인한다.
6. 운영자는 React 관리자 페이지에서 공지, 문의, 신고, 크롤링을 관리한다.


## 주요 화면

| 로그인 | 메인 페이지 | 오픈매트 목록 |
| :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/cf6fae43-f176-43c3-8901-5ea35bbc7ae7" width="250"> | <img src="https://github.com/user-attachments/assets/cf7bbe7e-704d-45d8-b517-5fe2f882f376" width="250"> | <img src="https://github.com/user-attachments/assets/fd034c76-6d6d-462d-863d-58775601888c" width="250"> |

| 오픈매트 신청 | 개최한 오픈매트 | 대회 목록 |
| :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/14a6ec50-ad1f-4d46-8bb1-8f8711783008" width="250"> | <img src="https://github.com/user-attachments/assets/1e0d991b-3a2d-40d7-ad5a-a7e99f504a1d" width="250"> | <img src="https://github.com/user-attachments/assets/da3a5e7d-afb0-482c-835b-3adedd62be7c" width="250"> |

### 관리자 주요 화면


| 운영 대시보드 | 신고 관리 |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/71508f66-74eb-477f-88fd-6c0596008c42" width="420"> | <img src="https://github.com/user-attachments/assets/7bdb1b6f-ad86-46b7-b940-3ccf6482385c" width="420"> |

| 문의 관리 | 문의 답변 |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/439d8b8a-9607-405f-9001-c0faa321273c" width="420"> | <img src="https://github.com/user-attachments/assets/b65d2f32-4dcb-47ca-b383-14b94d07289d" width="420"> |

| 공지사항 관리 | 공지사항 작성 |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/f6b04cff-379a-4f74-9e07-de0aa2d6f112" width="420"> | <img src="https://github.com/user-attachments/assets/4157f9a2-6314-445c-8d5e-854c706fc4e4" width="420"> |

| 대회 운영 | 대회 수동 등록 |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/45c74c47-54ca-4644-a50c-56cc88af9aa0" width="420"> | <img src="https://github.com/user-attachments/assets/b8edceb5-5638-4602-a66a-b29b3c00f6e6" width="420"> |

| 대회 크롤링 실행 |  |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/42f28e90-ad9f-41e5-8e0b-fd64b973577a" width="420"> |  |

## 기술 스택

### Frontend

**App Development**
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)

**State Management / Architecture**
![GetX](https://img.shields.io/badge/GetX-8A2BE2?style=for-the-badge&logo=flutter&logoColor=white)

**Admin Web**
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)





**Networking / Storage**
![HTTP](https://img.shields.io/badge/HTTP-00599C?style=for-the-badge&logo=flutter&logoColor=white)
![Flutter Secure Storage](https://img.shields.io/badge/Secure_Storage-4A148C?style=for-the-badge&logo=flutter&logoColor=white)
![Dotenv](https://img.shields.io/badge/flutter_dotenv-222222?style=for-the-badge&logo=.env&logoColor=white)

**Authentication / Notification**
![Google Sign-In](https://img.shields.io/badge/Google_Sign--In-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Kakao Login](https://img.shields.io/badge/Kakao-FFCD00?style=for-the-badge&logo=kakaotalk&logoColor=000000)
![Firebase](https://img.shields.io/badge/Firebase_Messaging-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)


---

### Backend

**Core**
![Java](https://img.shields.io/badge/Java_17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_4.0.1-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)

**Security / Auth**
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)

**Data / API**
![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-59666C?style=for-the-badge&logo=spring&logoColor=white)
![Hibernate](https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=hibernate&logoColor=white)
![Validation](https://img.shields.io/badge/Spring_Validation-0A7E07?style=for-the-badge)
![OpenAPI](https://img.shields.io/badge/OpenAPI-6BA539?style=for-the-badge&logo=openapiinitiative&logoColor=white)
![Flyway](https://img.shields.io/badge/Flyway-CC0200?style=for-the-badge&logo=flyway&logoColor=white)

**Integration / Utility**
![Jsoup](https://img.shields.io/badge/Jsoup-2E7D32?style=for-the-badge)
![Firebase Admin](https://img.shields.io/badge/Firebase_Admin_SDK-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![AWS S3](https://img.shields.io/badge/AWS_S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)

**Database / Monitoring**
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Spring Actuator](https://img.shields.io/badge/Spring_Actuator-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Micrometer](https://img.shields.io/badge/Micrometer-455A64?style=for-the-badge)

---

### Infrastructure / Operation

**Cloud / Delivery**
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Amazon S3](https://img.shields.io/badge/Amazon_S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)
![Lightsail](https://img.shields.io/badge/AWS_Lightsail-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

**Container / Routing**
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker_Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

**Push Notification**
![Firebase Cloud Messaging](https://img.shields.io/badge/FCM-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)

**Monitoring / Health**
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Spring Actuator](https://img.shields.io/badge/Health_Check-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Slack](https://img.shields.io/badge/Slack_Webhook-4A154B?style=for-the-badge&logo=slack&logoColor=white)

**Documentation**
![Swagger](https://img.shields.io/badge/Swagger/OpenAPI-85EA2D?style=for-the-badge&logo=swagger&logoColor=black)

## 프로젝트 구조

### Frontend

- Flutter 앱과 React 관리자 웹을 분리해 사용자 기능과 운영 기능을 구분
- Feature-based 구조
- MVVM 기반 화면 구성
- GetX를 이용한 상태 관리, 의존성 주입, 라우팅

### Backend

- REST API 기반 서버
- 인증/인가 분리
- 도메인별 API 구성
- 관리자 기능 별도 운영 API 제공
- 스케줄러, 알림, 모니터링, 운영 정책을 포함한 구조

## API / 도메인 구성

- **인증(Auth)**: 소셜 로그인, 토큰 발급 및 갱신, 로그아웃, 회원 탈퇴 예약/자동 처리 배치와 같은 사용자 인증 흐름을 담당합니다.
- **사용자(User)**: 내 정보 조회 및 수정, FCM 토큰 등록 및 삭제, 사용자 차단 기능을 제공합니다.
- **오픈매트(OpenMat)**: 오픈매트 생성, 수정, 삭제, 목록/상세 조회, 참가 신청 및 취소, 내가 신청한 목록과 내가 개최한 목록 조회, 모집 상태 변경, 참가자 관리 기능을 담당합니다.
- **대회(Tournament)**: 대회 목록 및 상세 조회, 수동 등록/수정/삭제, 관리자 전용 크롤링 실행 기능을 제공합니다.
- **알림(Notification)**: 사용자 알림 목록 조회와 읽음 처리 기능을 담당하며, 오픈매트 변경/삭제와 문의 답변 같은 이벤트를 관리합니다.
- **공지사항(Notice)**: 일반 사용자 대상 공지사항 목록/상세 조회와 관리자 전용 공지 등록, 수정, 삭제 기능으로 구성됩니다.
- **문의(Inquiry)**: 사용자의 문의 등록, 내 문의 목록/상세 조회 기능과 관리자 전용 문의 답변 및 상태 변경 기능을 포함합니다.
- **신고(Report)**: 신고 생성, 관리자 전용 신고 목록/상세 조회, 상태 변경, 누적 신고 대상 요약 기능을 포함합니다.
- **관리자(Admin)**: 공지 운영, 대회 크롤링 실행, 문의 응답 처리, 신고 및 운영 데이터 관리 등 서비스 운영을 위한 관리자 전용 기능을 담당합니다.


## 운영 정책 또는 비즈니스 규칙

- 오픈매트는 생성, 신청, 취소, 모집 상태 변경 흐름을 기준으로 관리되며 삭제 시에는 soft delete 정책을 사용합니다.
- 오픈매트는 정원 초과, 종료 시간, 신고 누적 상태에 따라 신청 가능 여부가 제한됩니다.
- 공지사항은 일반 사용자에게는 조회 전용으로 제공되며, 관리자만 생성, 수정, 삭제할 수 있습니다.
- 알림은 FCM 수신 여부와 별개로 백엔드에 저장된 알림 데이터를 기준으로 관리합니다.
- 문의 기능은 사용자는 본인 문의만 조회할 수 있고, 관리자는 전체 문의 조회 및 답변 처리를 수행할 수 있습니다.
- 관리자 기능은 `Authorization: Bearer {accessToken}` 기반 인증과 `ROLE_ADMIN` 권한 검사로 보호됩니다.
- 운영 환경 DB 스키마는 `Flyway` 기반 버전 관리로 반영합니다.
- 스케줄러와 외부 의존성 상태는 `Actuator`와 커스텀 메트릭을 통해 모니터링합니다.


## 트러블슈팅

### 1. API, 랜딩 페이지, 관리자 페이지를 함께 운영해야 하는 배포 구조 문제
- 문제: 초기에는 Spring Boot 단일 서버 중심으로 개발했지만, 서비스가 커지면서 API 서버와 랜딩 페이지, 관리자 페이지를 함께 운영해야 했습니다.
- 원인: 단일 애플리케이션만으로는 서로 다른 웹 진입점과 정적 리소스, 운영 도메인 구조를 유연하게 분리하기 어려웠습니다.
- 해결: `Nginx` 리버스 프록시를 도입해 API, 랜딩 페이지, 관리자 페이지 라우팅을 분리하고, `Docker Compose` 기반으로 서비스 구성을 정리해 배포와 운영 구조를 일관되게 관리할 수 있도록 개선했습니다.

### 2. 프로덕션 장애를 실시간으로 감지하기 어려웠던 문제
- 문제: 운영 중에는 스케줄러 실패, 메트릭 수집 실패, FCM 실패율 증가 같은 이슈를 사용자가 제보하기 전에 먼저 파악할 필요가 있었습니다.
- 원인: 기능은 구현되어 있었지만, 서버 상태와 운영 이벤트를 지속적으로 관찰할 수 있는 모니터링 및 알림 체계가 부족했습니다.
- 해결: `Spring Actuator`, `Micrometer`, `Prometheus`, `Grafana`, `Slack Webhook`을 연동해 헬스체크, 커스텀 메트릭, 대시보드, 운영 알림 체계를 구성했습니다. 이를 통해 스케줄러 상태와 외부 의존성 이상 여부를 실시간으로 추적할 수 있도록 확장했습니다.

### 3. 수동 배포로 인한 운영 부담과 배포 일관성 문제
- 문제: 빌드와 배포를 수동으로 진행하면 반복 작업이 많아지고, 환경별 반영 과정에서 누락이나 실수가 발생할 여지가 있었습니다.
- 원인: 코드 변경 이후 빌드, 이미지 반영, 서버 배포 과정을 사람이 직접 수행하면 배포 절차의 재현성과 속도가 떨어졌기 때문입니다.
- 해결: `GitHub Actions` 기반 CI/CD 파이프라인을 구성하고 `AWS Lightsail` 배포를 자동화해, 코드 변경 이후 빌드와 배포가 일관된 절차로 반복되도록 개선했습니다.

### 4. 오픈매트 신청 시 정원 초과가 발생할 수 있는 동시성 문제
- 문제: 정원이 1명 남은 오픈매트에 여러 사용자가 동시에 신청하면 중복 신청이 발생할 수 있었습니다.
- 원인: 단순 조회 후 신청하는 구조만으로는 동시에 들어온 요청 간 정합성을 보장하기 어려웠기 때문입니다.
- 해결: 신청/취소 흐름에 동시성 제어를 고려한 접근을 적용하고, 정원 경계 상황을 검증하는 통합 테스트를 추가해 한 명만 성공하도록 보장했습니다.
