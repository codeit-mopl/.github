# 🎬 모두의 플리 (Mopl)
> **대규모 트래픽이 예상되는 글로벌 컨텐츠 평점 및 큐레이션 플랫폼**

"모두의 플리"는 영화, 드라마, 스포츠 등 다양한 콘텐츠를 큐레이팅하고 공유하며, 실시간으로 다른 사용자들과 소통할 수 있는 소셜 서비스입니다. 나만의 플레이리스트를 만들고 실시간 같이 보기 기능을 통해 콘텐츠 경험을 확장해 보세요.

---

## 🚀 Key Features

### 1. 콘텐츠 큐레이션 및 평가
* **글로벌 데이터 연동**: TMDB(영화/드라마) 및 The Sports DB(스포츠) API를 통한 방대한 콘텐츠 수집.
* **개인 맞춤형 플리**: '보고 싶은 콘텐츠', '비 오는 날 보기 좋은 콘텐츠' 등 테마별 플레이리스트 생성.
* **구독 시스템**: 취향이 맞는 유저의 플레이리스트를 구독하고 신규 업데이트 알림 수신.

### 2. 실시간 소통 (Real-time Interaction)
* **실시간 같이 보기**: 현재 동일한 콘텐츠를 시청 중인 유저 확인 및 실시간 채팅 (WebSocket).
* **소셜 네트워크**: 사용자 팔로우, 프로필 관리 및 실시간 활동 피드 알림.
* **DM (Direct Message)**: 1:1 메시징 및 실시간 알림 (SSE & WebSocket).

### 3. 관리자 시스템 (Admin DashBoard)
* **Spring Batch 기반 데이터 관리**: 대용량 콘텐츠 데이터의 안정적인 수집 및 배치 작업.
* **사용자 제어**: 계정 잠금, 권한 변경(Admin/User) 및 강제 로그아웃 처리.

---

## 🛠 Tech Stack

### Backend
- **Framework**: Java 17, Spring Boot 3.x
- **Data**: Spring Data JPA, Querydsl
- **Batch**: Spring Batch (Content Data 수집 및 처리)
- **Messaging/Real-time**: WebSocket, STOMP, SSE, Kafka
- **Security**: Spring Security, JWT, OAuth2 (Google, Kakao), CSRF Token

### Infrastructure & DevOps
- **Cloud**: AWS ECS (Fargate)
- **Proxy**: Nginx (Reverse Proxy)
- **CI/CD**: GitHub Actions
- **Container**: Docker, Docker Compose
- **Monitoring**: Spring Actuator, Logback

---

## 🏗 System Architecture



- **Scalability**: 분산 환경을 고려하여 JWT 세션 관리 및 Redis 캐싱 적용.
- **Reliability**: TDD(Test Driven Development)를 통한 테스트 커버리지 80% 이상 유지.
- **Event-Driven**: 서비스 간 느슨한 결합을 위해 Kafka 메시징 시스템 활용.

---

## 📋 API & WebSocket Specifications

### WebSocket Endpoints
| Function | Endpoint | Payload |
| :--- | :--- | :--- |
| 콘텐츠 시청 세션 | `/sub/contents/{contentId}/watch` | `WatchingSessionChange` |
| 콘텐츠 실시간 채팅 | `/sub/contents/{contentId}/chat` | `ContentChatDto` |
| DM 메시지 수신 | `/sub/conversations/{conversationId}/direct-messages` | `DirectMessageDto` |

### Server Sent Event (SSE)
- **Endpoint**: `/api/sse`
- **Events**: `notifications` (알림), `direct-messages` (DM 수신)

---
