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
- 참여자의 접속 현황은 **MongoDB**를 통해 채팅방 기준으로 접속자의 접속 여부, 퇴장 시간을 관리합니다
- 가볍게 처리하고 별개의 기록을 남길 필요가 없기에 **Redis Pub Sub** 메세지브로커로 구현했습니다

<br />

### 3. 미접속 채팅 메세지 보관 출력 기능

<img src="https://github.com/user-attachments/assets/5664d4b4-6f0b-485c-b61b-8ded44de1b93" alt="save" width="580" height="400" align="center"/> 

<br />
<br />


- 접속을 끊었지만 서버 내에서 구독을 유지하고 있는 채팅 내에서 이뤄진 메세지를 저장하여 재접속할 때 출력해줍니다
- 접속자 관리를 담당하는 MongoDB에서 **GraphQL**을 통해 받아온 퇴장 시간을 바탕으로 **PostgreSQL**에서 조회합니다

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
  <img src="https://img.shields.io/badge/GraphQL-E434AA?style=for-the-badge&logo=graphql&logoColor=white" />
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

### 1. 인증 기능의 관심사 분리에 따른 인증 로직 비동기 처리

#### ❓ 문제 상황

- **Netty** 엔진을 기반으로 구축된 API Gateway에게 라우팅 및 필터링 책임만을 분배하고 인증 책임을 별도의 인스턴스에 위임
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

### 2. 채팅방 구독에 대한 트래픽이 몰리는 상황에서의 동시성 제어

#### ❓ 문제 상황

- 2차 리팩토링 전의 채팅방 구독 관리는 접속 관리와 더불어 **NoSQL(Redis, MongoDB)** 에서 책임
- **polyglot persistence** 패턴 구현을 위해 **구독 관리를 RDBMS(PostgreSQL)** 에 넘기는 리팩토링 시행
- 현재 구독자 수 필드를 채팅방 엔티티에 추가하고, 구독 이벤트 로직 내에서 필드의 업데이트 처리
```java
// chat instance

@Getter
@Setter
@Entity
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@Table(name = "openchats")
@EntityListeners(AuditingEntityListener.class)
public class ChatRoom {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    // ...

    @Column(name = "personnel")
    private Integer personnel;
```
```java
// message instance

@Slf4j(topic = "ChatMessageService")
@Service
@RequiredArgsConstructor
public class ChatMessageService {

    // ...

    public void enter(ChatMessageDTO.Enter enter, @AuthenticationPrincipal UserDetailsImpl userDetails) {
        String username = userDetails.getUsername();
        String role = userDetails.getRole();

        // ...

        // GraphQL을 통해 chat instance에 있는 채팅방 엔티티 인스턴스 필드 업데이트
        graphqlService.incrementPersonnel(enter.getChatId(), username, role);
```


#### ❗ 문제 발생

- 메세지 인스턴스에서 GraphQL로 API 호출을 수행하면서 채팅 인스턴스에서의 현재 인원 업데이트 과정을 구현
- 플로우는 아래와 같음

<p align="center">
  <img width="60%" alt="rdbms에 위임" src="https://github.com/user-attachments/assets/eccc890d-4bdb-4c01-8606-613ee5c4f986">
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">현재 인원 업데이트 플로우</p>
</div>

<p align="center">
  <img width="60%" alt="rdbms에 위임" src="https://github.com/user-attachments/assets/d3ab47e8-7020-4dd8-a04f-f18c3f37842d">
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">PostgreSQL 테이블로 현재 인원 관리</p>
</div>

- NoSQL에서 RDBMS로 리팩토링을 하고 메세지 인스턴스에서 채팅 인스턴스로 구독 관리 책임을 분산시켜서 **JUnit** 기반으로 동시성 테스트 코드를 작성

```java
// 인메모리 데이터베이스 h2 기반 동시성 제어 테스트
// 메모리 기반이기 떄문에 테스트 종료시, 자동 휘발됨(데이터베이스까지!)
@Slf4j
@SpringBootTest
@ActiveProfiles("test")
public class ConcurrencyTest {

    @Autowired
    private ChatRoomRepository chatRoomRepository;

    @Autowired
    private ChatGraphqlServiceImpl chatGraphqlService;

    // ...

    @BeforeEach
    @DisplayName("임의의 채팅방 객체 생성")
    void setUp() {
        ChatRoomDTO dto = new ChatRoomDTO(TITLE, MAX_PERSONNEL);
        ChatRoom chatRoom = new ChatRoom(dto, "openUser");

        chatRoomRepository.save(chatRoom);
    }

    // ...

    @Test
    @DisplayName("트래픽이 몰리는 상황에서 정합성이 지켜지는지 테스트")
    void testWithNoLock() throws InterruptedException {
        // given & when...

        // 스레드 풀 및 동시 시작 장치
        ExecutorService executorService = Executors.newFixedThreadPool(CLIENT);
        CountDownLatch countDownLatch = new CountDownLatch(CLIENT);

        // 성공 결과를 담을 자료구조
        List<GraphqlDTO> result = new ArrayList<>();

        for (int i = 0; i < CLIENT; i++) {
            executorService.submit(() -> {
               try {
                   GraphqlDTO success =
                           chatGraphqlService
                                   .incrementPersonnel(chatRoom.getId().toString());
                   result.add(success);
                   log.info("입장 성공!: {}", success);
               } catch (Exception e) {
                   log.error("입장 실패! : {}", e.getMessage());
               } finally {
                   countDownLatch.countDown(); // 카운트 감소
               }
            });
        }

        countDownLatch.await(); // 스레드 종료 대기
        executorService.shutdown(); // 서비스 종료

        // then
        assertThat(result.size())
                .describedAs("예상 인원 수: %d, 실제 인원 수: %d", MAX_PERSONNEL, result.size())
                .isGreaterThan(MAX_PERSONNEL);
    }
```

- 테스트 수행 환경은 **채팅방의 제한 인원 대비 트래픽이 몰리는 상황**으로 설정
- 수행 결과 제한 인원보다 더 많은 스레드에서 입장 승인 처리 확인, 즉 **동시성 이슈 발생**

<p align="center">
  <img width="60%" alt="동시성이슈" src="https://github.com/user-attachments/assets/d1aef60a-8d91-4825-86c7-892088c82638">
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">JUnit 테스트 코드로 동시성 이슈 발생 확인</p>
</div>


#### 💬 문제 파악

- 처음 구독자 관리를 **Redis**로 했을 때는 싱글 스레드로 동작하는 Redis 특성상, 동시성 이슈가 발생하지 않았음
- PostgreSQL, 즉 **RDBMS**에서 트래픽이 몰릴 경우 복수의 트랜잭션이 경합 발생, **커밋되지 않은 값을 기반으로 업데이트 로직 수행**

```sql
# A 트랜잭션이 조회 SQL문을 수행해서 제한인원의 여유를 확인
SELECT personnel FROM openchat WHERE room_id = X;

# A 트랜잭션이 업데이트 과정을 수행하기 바로 직전 B 트랜잭션이 조회 SQL문을 수행해서 제한인원의 여유를 확인
SELECT personnel FROM openchat WHERE room_id = X;

# A, B 트랜잭션 둘 다 업데이트 처리, 동시성 이슈 발생
UPDATE openchat SET personnel = personnel + 1 WHERE room_id = X;
```
- Redis에서 동시성 이슈가 발생하지 않았던 이유는, Redis는 **싱글 스레드** 기반 동작 및 원자적 연산을 지원

<p align="center">
  <img width="60%" alt="원자적 연산" src="https://github.com/user-attachments/assets/af987755-3a74-4367-aaad-e83564d904db">
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">Redis의 원자적 연산 중 하나인 INCR</p>
</div>

- 그렇지만 Redis로 회귀하는 것은 **데이터베이스의 사용 목적 및 역할별 분류라는 MSA의 취지**를 지키지 못하는 것
- 리팩토링을 수행한 RDBMS 내에서 락을 걸어 동시성 제어를 수행하기로 결정

#### 💡 문제 해결

- 락을 구현할 수 있는 방법으로, **데이터베이스 레벨의 락**과 **외부 툴을 활용한 락** 구현 방법이 있음
- PostgreSQL 레벨의 락과 Redis를 활용한 락에 대해 고민

| **특징**                | **데이터베이스 레벨 락**                      | **외부 툴 락 (예: Redis)**               |
|-----------------------|------------------------------------------|---------------------------------------|
| **속도**               | 상대적으로 느릴 수 있음 (디스크 I/O 필요) | 매우 빠름 (메모리 기반)               |
| **원자성**             | 트랜잭션을 통해 보장됨                     | 명령어 단위로 원자적 처리             |
| **확장성**             | 수직적 확장 필요                          | 수평적 확장이 가능                    |
| **복잡성**             | 데이터베이스 내에서 간단하게 관리 가능      | 별도의 로직 필요 (락 획득 및 해제)     |
| **재사용성**           | 특정 데이터베이스에 종속됨                  | 다양한 시스템에서 재사용 가능          |
| **지속성**             | 데이터베이스 트랜잭션과 함께 지속됨         | 데이터의 지속성은 설정에 따라 달라짐   |
| **경합 조건**          | 다양한 격리 수준에서 동작                   | 원자적 명령으로 경합 조건 감소         |
| **락 경량성**          | 보통 무겁고, 성능 저하 우려 있음             | 경량 락으로 빠른 경합 처리 가능         |
| **다중 노드 지원**      | 복잡한 설정 필요                           | 기본적으로 다중 노드 지원               |
| **유지 관리**           | 데이터베이스 내에서 관리                    | 별도의 툴과 인프라 관리 필요            |

- 채팅 애플리케이션처럼 실시간 처리 속도를 우선순위로 봐야 하고 수평적 확장이 중요함
- 인스턴스의 스케일링이 있을 때, **락의 공유**를 통한 경합 처리를 수행해야 함
- 위의 사유로, **Redis를 활용한 분산 락 구현**을 통한 동시성 제어 결정
- **Redisson 클라이언트 or Lettuce 클라이언트**에 대한 고민

| **특징**            | **Redisson**                               | **Lettuce**                                |
|-------------------|------------------------------------------|-------------------------------------------|
| **사용 편의성**     | 고수준 API 제공, 쉽게 구현 가능            | 사용자가 원하는 대로 커스터마이징 필요       |
| **기능**           | 분산 락, 큐, 캐시 등 다양한 데이터 구조 지원 | 비동기 및 반응형 API, 모듈형 설계          |
| **자동 해제**       | 락 타임아웃 자동 관리                     | 명시적 해제를 위한 코드 필요                |
| **비동기 처리**     | 비동기 지원 없음                          | 비동기 및 반응형 프로그래밍 지원            |
| **성능**           | 성능이 우수하지만 비동기 처리에 비해 약간 느림 | 높은 성능과 낮은 지연 시간 제공             |
| **유연성**         | 다양한 기능을 한 곳에서 지원              | 다양한 프로그래밍 패러다임 지원             |
| **추천 사용 경우**  | 소규모 팀, 빠른 개발, 다양한 기능 필요시    | 고성능, 대규모 채팅 애플리케이션에 적합      |

- 락의 자동 해제에 있어 기능 구현이 상대적으로 간편한 Redisson을 1차적으로 채택 후, 성능 한계가 다가올 때 Lettuce로 전환 결정
- 락 기능을 제공하는 별도의 컴포넌트에, 현재 인원 증가 업데이트 메소드를 보유한 서비스를 의존성 주입

```java
@Slf4j
@Component
@RequiredArgsConstructor
public class DistributedLockFacade {

    private final RedissonClient redissonClient;
    private final ChatGraphqlService chatGraphqlService;

    public GraphqlDTO incrementPersonnel(String id) {

        RLock lock = redissonClient.getLock(id);

        try {
            boolean available = lock.tryLock(10, 1, TimeUnit.SECONDS);

            if (!available) {
                log.error("락 획득 실패");
                return null;
            }

            log.info("락 획득 성공");
            return chatGraphqlService.incrementPersonnel(id);
        } catch (InterruptedException e) {
            log.error("락 획득 예외 발생: {}", e.getMessage());
            throw new RuntimeException(e);
        } finally {
            log.info("락 잠금 해제");
            lock.unlock();
        }
    }
}
```

- 해당 코드로 GraphQL 호출 컨트롤러에 주입 후, 다시 JUnit 기반으로 테스트 수행 결과 동시성 제어 확인
- 문제 해결

<p align="center">
  <img width="60%" alt="동시성 제어" src="https://github.com/user-attachments/assets/da5a2bce-dacc-43b4-88f1-5f535f394bff">
</p>
<div align="center"> 
  <p style="font-size:12px; color:#808080;">Redisson 기반 분산 락 구현으로 동시성 제어</p>
</div>

### 3. 클라이언트 레벨 구독 종료 & 서버 레벨 구독 유지 상황에서의 채팅 메세지 보존

#### ❓ 문제 상황
#### ❗ 문제 발생
#### 💬 문제 파악
#### 💡 문제 해결

### 4. 웹소켓 구독 이벤트와 레디스 메세지브로커 이벤트 순서 정립을 통한 데이터 소실 방지

#### ❓ 문제 상황
#### ❗ 문제 발생
#### 💬 문제 파악
#### 💡 문제 해결
