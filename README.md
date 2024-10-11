<p align="center">
  <a href="https://github.com/orgs/ChatTalk/repositories">
    <img width="70%" src="https://github.com/user-attachments/assets/bdcd934e-848a-4b8c-93ad-70dc44c9f225" alt="ChatTalk">
  </a>
</p>

<h3 align="center">
  실시간 통신 트래픽 제어 & MSA 마이그레이션 스터디 프로젝트
</h4>

---

#### 📖 목차

>[1. Introduction](#-introduction) <br/>
>[2. Link](#-link) <br />
>[3. Architecture](#%EF%B8%8F-architecture) <br />
>[4. Features](#-features) <br />
>[5. Skills](#%EF%B8%8F-skills) <br/>
>[6. Trouble Shooting](#-trouble-shooting) <br/>

---

## 📝 Introduction

HTTP, WebSocket 프로토콜에서의 로직 구현 및 **MSA** 기반 인프라 구축, 트래픽 제어를 목표로 하는 스터디 프로젝트입니다. <br />
도전적인 기능들을 구현하고 테스트를 근거로 성능 개선을 이뤄내는 **채팅 애플리케이션 서비스 프레임**을 구현하였습니다.

<br />

## 🔗 Link


<div>
  <img src="https://github.com/kimD0ngjun/memory_test/assets/129869700/5dc82abc-8f2e-4b9d-8e2e-73406979c61e" alt="velog" width="20" height="21" align="center"/>
  <b>벨로그 개발일지 : </b>
  <a href="https://velog.io/@kim00ngjun_0112/series/chat" target="_blank">
    https://velog.io/@kim00ngjun_0112/series/chat
  </a>
</div>
<div>
  <img src="https://github.com/user-attachments/assets/bf824549-5a2a-4b42-b2ed-5b182a9d24aa" alt="youtubue" width="23" height="24" align="center"/>
  <b>1차 시연 영상 : </b>
  <a href="https://www.youtube.com/watch?v=FZV4JvbwLrQ" target="_blank">
    https://www.youtube.com/watch?v=FZV4JvbwLrQ
  </a>
</div>
<div>
  <img src="https://github.com/user-attachments/assets/4837274a-c842-451e-ad9e-56d37ae2fa6f" alt="deploy" width="23" height="24" align="center"/>
  <b>1차 배포 링크 : </b>
  <a href="https://chattalk-three.vercel.app" target="_blank">
    https://chattalk-three.vercel.app
  </a>
</div>

<br />

<div>
  <img src="https://github.com/user-attachments/assets/d57687b1-7246-444d-9449-ed4284c0c8f0" alt="github" width="23" height="24" align="center"/>
  <b>MSA 인스턴스 repo : </b>
  <a href="https://github.com/orgs/ChatTalk/repositories" target="_blank">
    https://github.com/orgs/ChatTalk/repositories
  </a>
</div>
<div>
  <img src="https://github.com/kimD0ngjun/memory_test/assets/129869700/953ff03f-479d-4761-b6d0-f7f294a3f6d6" alt="gmail_contact" width="23" height="24" align="center"/>
  <b>개발자 이메일 : </b>
  <a href="mailto:chickentasty0112@gmail.com" target="_blank">
    chickentasty0112@gmail.com
  </a>
</div>

<br />

*비용 문제 및 인프라 개선으로 인해 현재 서버 인스턴스 연결이 끊어져있기 때문에 기왕이면 시연 영상을 참고 바랍니다*
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<br />

## 🏗️ Architecture
<br/>
<p align="center">
  <img src="https://github.com/user-attachments/assets/46d45f80-c5be-432d-9e51-d181b69dbfac" alt="architecture" width="700" height="647.5" align="center" />
</p>
<br />

## ✨ Features

### 1. 채팅 실시간 메세징 기능

<img src="https://github.com/user-attachments/assets/0cbf1d9b-0911-4c52-8adf-e3b9743bcf9a" alt="message" width="380" height="400" align="center"/> 

<br />
<br />


- **WebSocket STOMP**를 기반으로 ws 프로토콜에서의 실시간 사용자간 메세지 송수신 기능을 구현했습니다
- 웹소켓 서버 스케일링에 대응하고 메세지 신뢰성 보장을 위한 고성능 메세지 큐인 **Kafka**를 구축하였습니다

<br />

### 2. 채팅 참여자 현황 표시 기능

<img src="https://github.com/user-attachments/assets/c73a17d6-be30-48dd-93c2-fe0753abaae1" alt="participant" width="400" height="400" align="center"/> 

<br />
<br />


- 별개의 추가 **WebSocket** 인스턴스로 동작하되, 메세징 인스턴스와 이벤트 기반으로 상호 작용하여 실시간으로 참여자를 관리합니다
- 가볍게 처리하고 별개의 기록을 남길 필요가 없기에 **Redis Pub Sub** 메세지브로커로 구현했습니다

<br />

### 3. 미접속 채팅 메세지 보관 출력 기능

<img src="https://github.com/user-attachments/assets/5664d4b4-6f0b-485c-b61b-8ded44de1b93" alt="save" width="580" height="400" align="center"/> 

<br />
<br />


- 접속을 끊었지만 서버 내에서 구독을 유지하고 있는 채팅 내에서 이뤄진 메세지를 저장하여 재접속할 때 출력해줍니다
- 구조적 데이터 관리가 용이하고 실시간 처리가 뛰어난 **MongoDB**를 기반으로 구현했습니다

<br />

## 🛠️ Skills


### 🔧 BackEnd

<p>
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/SpringBoot-6DB33F?style=for-the-badge&logo=Spring&logoColor=white" />
  <img src="https://img.shields.io/badge/Spring Data JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
  <img src="https://img.shields.io/badge/Spring Cloud-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
  <img src="https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white" /> <br />
  <img src ="https://img.shields.io/badge/postgresql-4169e1?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" />
  <img src="https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white" />
  <img src="https://img.shields.io/badge/-MongoDB-13aa52?style=for-the-badge&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/docker-257bd6?style=for-the-badge&logo=docker&logoColor=white" />
</p>

### 🖥️ FrontEnd

<p>
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/-ReactJs-61DAFB?logo=react&logoColor=white&style=for-the-badge" />
  <img src="https://img.shields.io/badge/-Redux-purple?style=for-the-badge&logo=redux" />
  <img src="https://img.shields.io/badge/axios-854195?style=for-the-badge&logo=axios&logoColor=5A29E4" />
  <img src ="https://img.shields.io/badge/Styled_Components-DB7093?style=for-the-badge&logo=styled-components&logoColor=white" />
  <img src="https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" />
</p>

<br />

## 🔍 Trouble Shooting

### 1. 인증 기능의 관심사 분리에 따른 인증 여부 데이터 송수신 정합성 이슈

#### ❓ 문제 상황

- **Netty** 엔진을 기반으로 구축된 API Gateway에게 라우팅 및 필터링 책임만을 분배하고 인증 책임을 별도의 인스턴스에 위임
- 이를 통해 향후 인증 방식이 바뀌어도 API Gateway의 로직을 수정할 필요가 없어짐으로써 수평적 확장성을 도모
- 비동기 요청 처리에 필요한 요구 사항을 충족시키기 위해서. 인스턴스 간의 통신 수단을 **Kafka**로 구축한 시점
- 자연스럽게 Kafka를 통한 인증 인스턴스와 API Gateway 간의 인증 정보 송수신을 생각

<br />

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/d7f1521b-f9a2-4980-b06f-28a1995e7d2b/image.png" />
</p>

<br />

- 인증 인스턴스에서 받아온 인증 정보를 요청의 헤더에 커스텀해서 보내줌
- 각 인스턴스의 필터 단계에서 인증 객체를 생성해서 인증함으로써 최종 인증 로직 종료

```java
// ...

        SecurityContext context = SecurityContextHolder.createEmptyContext();
        context.setAuthentication(createAuthentication(username));
        SecurityContextHolder.setContext(context);
    }

    // Authentication 객체 생성 (UPAT 생성)
    private Authentication createAuthentication(String username) {
        UserDetails userDetails = userDetailsService.loadUserByUsername(username);
        return new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
    }
```

#### ❗ 문제 발생


```java
// Auth Filter in API Gateway

// 인증 요청 Kafka 전송
return kafkaProducerTemplate.send(topic, id.toString(), tokenDTO)
        .then(Mono.defer(() -> {
            // 인증 응답 대기
            return kafkaReceiver
                    .receive()
                    .filter(record -> record.key().equals(id.toString()))
                    .next()
                    .map(ConsumerRecord::value)
                    .flatMap(userInfoDTO -> {
                        // ...
```

- 카프카 기반 요청을 보내는 로직에서 인증 응답을 대기하는, **요청 - 응답 모델**을 활용해서 인증 처리 로직 구축
- 테스트 결과, **인증을 전제로 하는 로그아웃을 비롯한 API 호출의 99% 이상 실패** 기록

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/ebf8e0f1-abf1-45f2-874a-c82ef224dfc3/image.png" />
</p>

<div align="center"> 
  <p style="font-size:12px; color:#808080;">Kafka 요청 - 응답 모델에서의 테스트</p>
</div>

#### 💬 문제 파악

- 서버 내부의 에러(500)라는 것은 응답 수신 대기 과정에서의 타임아웃 가능성 
- 논블로킹 방식의 요청 - 응답은 **Kafka의 비동기성 및 이벤트 스트리밍 취지**를 위배
- Netty 기반의 비동기 로직으로 이뤄진 API Gateway에서 인증 결과를 직접 조회시키는 방향으로 개선
- 인증 인스턴스의 처리 결과를 **Redis에 바로 저장해서 캐시 데이터로 활용**, API Gateway에서 **직접 Redis 조회**

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/d6e04c8d-bba5-4ec8-a2e8-a6c2a81f03f7/image.png" />
</p>

#### 💡 문제 해결

```java
// Auth Filter in API Gateway

// 인증 요청 Kafka 전송
return kafkaProducerTemplate.send(topic, tokenDTO)
        .flatMap(result -> {
            // Kafka에 메시지 전송 후 Redis에서 결과를 비동기적으로 조회
            return checkRedisForUserInfo(id)
                    .flatMap(userInfoDTO -> {
                    // ...
```

- 카프카 응답 수신 로직을 걷어내고, 레디스 조회 메소드를 통해 결과를 반환받는 방향으로 리팩토링
- 고려할 점으로 API Gateway의 Redis 조회가 인증 작업보다 빠른 것에 대한 대비책, 엑세스 토큰의 파싱 속도보다 API Gateway의 조회 속도가 더 빠를 경우

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/ba3d32d2-d0c9-40ec-a8fa-e1d2d1dd719a/image.png" />
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">API Gateway의 조회와 엑세스 토큰 파싱의 비정합성</p>
</div>

- 레디스 조회에서 수신 대기 메소드를 추가로 작성해서 활용
- 0.05초 간격으로 재시도 로직을 수행해서 인증 정보를 받아올 수 있도록 처리
- 최대 타임아웃으로 10초를 설정하여 인증 로직 혹은 Redis에 문제가 발생해 캐시가 조회되지 않으면 예외 처리

```java
// redis 캐시 조회 메소드
private Mono<UserInfoDTO> checkRedisForUserInfo(String id) {
    return Mono.defer(() -> {
            UserInfoDTO userInfo = userInfoTemplate.opsForValue().get(REDIS_ACCESS_KEY + id);

                if (userInfo != null) {
                    log.info("Redis에서 사용자 정보 조회 성공 - UserInfo: {}", userInfo);  // 성공 시 로그 추가

                    if (!id.equals(userInfo.getId())) {
                        userInfoTemplate.delete(REDIS_ACCESS_KEY + id);
                        userInfoTemplate.opsForValue().set(REDIS_ACCESS_KEY + userInfo.getId(), userInfo, 120 * 30, TimeUnit.SECONDS);
                    }

                    return Mono.just(userInfo);
                } else {
                    log.info("Redis에서 사용자 정보가 없음 - ID: {}\n 조회하는 시간: {}", id, System.nanoTime());  // 데이터가 없는 경우 로그 추가
                    return Mono.empty();
                }
            })
            .repeatWhenEmpty(flux -> flux
                    .delayElements(Duration.ofMillis(50)) // 0.05초 간격으로 재시도
                    .take(200)) // 재시도
            .timeout(Duration.ofSeconds(10)) // 타임아웃 설정
            .onErrorResume(e ->
                    Mono.error(new ResponseStatusException(
                            HttpStatus.INTERNAL_SERVER_ERROR, "레디스 유저 임시정보 조회 에러", e)));
    }
```




- Redis에 캐시가 있을 때는 굳이 인증 인스턴스를 거치지 않고 바로 요청을 라우팅 처리
- 캐시가 없으면 인증 인스턴스로 Kafka를 통해 송신해서 인증 정보를 캐시 조회로 받아오는 방식으로 최종 리팩토링
- 문제 해결

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/92749318-3c16-409b-9a0b-8a8fbe9208f5/image.png" />
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">Redis에 캐시가 존재할 경우</p>
</div>

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/006c53f0-acb7-4bdd-9856-e2032e3f44af/image.png" />
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">Redis에 캐시가 존재하지 않을 경우</p>
</div>

<p align="center">
  <img width="60%" src="https://velog.velcdn.com/images/kim00ngjun_0112/post/2fa9ded0-841a-4b5e-a420-4f760f6a83f8/image.png" />
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">Kafka 전파 - Redis 캐시 조회 모델에서의 테스트</p>
</div>

<br />

### 2. 클라이언트 레벨 구독 종료 & 서버 레벨 구독 유지 상황에서의 채팅 메세지 보존

#### ❓ 문제 상황
#### ❗ 문제 발생
#### 💬 문제 파악
#### 💡 문제 해결

### 3. 웹소켓 기반 이벤트 트리거와 별개의 웹소켓 구독 시점 어긋남으로 인한 데이터 소실 

#### ❓ 문제 상황
#### ❗ 문제 발생
#### 💬 문제 파악
#### 💡 문제 해결
