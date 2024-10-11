<p align="center">
  <a href="https://github.com/orgs/ChatTalk/repositories">
    <img width="70%" src="https://github.com/user-attachments/assets/bdcd934e-848a-4b8c-93ad-70dc44c9f225" alt="ChatTalk">
  </a>
</p>

<h3 align="center">
  실시간 통신 트래픽 제어 & MSA 마이그레이션 스터디 프로젝트
</h4>

---


## 📝 Introduction

HTTP, WebSocket 프로토콜에서의 로직 구현 및 MSA 기반 인프라 구축, 트래픽 제어를 목표로 하는 스터디 프로젝트입니다. <br />
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
