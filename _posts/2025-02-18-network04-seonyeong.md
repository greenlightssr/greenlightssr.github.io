---
layout: single
title: "TCP/IP 프로토콜 분석01"
date: 2025-02-18
last_modified_at: 2025-02-18
categories:
  - sys/net security
author: seonyeong
sidebar:
  nav: "categories"
---

### ● TCP/IP Protocol Stack

![](https://blog.kakaocdn.net/dn/byE359/btsLZWktDwh/Oza94nKi7k3I3DOaQJtKr0/img.png)

#### Application Layer (7)

* TCP 계열의 서비스와 UDP 계열의 서비스로 나뉜다
* DNS는 두 계열 다 됨

#### Transport Layer (4)

* ex) http 데이터가 payload 됐을 때 앞에 TCP 헤더가 부착된다
* ex) tftp 데이터가 payload 됐을 때 앞에 UDP 헤더가 부착된다

#### Network Layer (3)

ARP RARP(3계층임 2계층 아님)

ICMP 인터넷 제어 메세지 프로토콜

IGMP 멀티캐스트 작업할 때 쓰는 프로토콜

위 3개는 유틸리티 프로토콜임 작업할 때 편하게

IPv4 필수 프로토콜! 무조건 이 헤더 부착

#### Network Access Layer (2)

이더넷 랜 부착

수직적 관계 까먹지 말고 생각하기

---

(ex) 수업 방식으로 이해해 보기

<TCP 수업 방식>

like 3WHS 클라이언트가 서버에게 질문 시 꼭 대답을 해줘야 함 양방향

올바른 대답이 올 때까지 무한 반복 항상 클라이언트가 먼저 요청

마지막에 서버가 요청하고 클라이언트가 대답하고 서버 로그아웃 그다음 클라이언트 로그아웃

장점 : 클라이언트와 서버 입장에서는 상호 간 신뢰성 확보

단점 : 시간이 오래 걸림 너무 느리다

<UDP 수업 방식>

서버가 준비돼서 단방향으로 데이터, 수업 내용 다 보내버리고 혼자 로그아웃

클라이언트 상태 확인 안 해도 되고 대답도 필요 없다

장점 : 매우 빠르다

단점 : 상호 간 신뢰성 떨어진다

느리더라도 안정성을 확보하고 싶다면 TCP, 패킷이 버려져도 상관없다 빠르기만 하면 돼 이렇다면 UDP

---

FTP(S) -----> FTP(C)

100MB -----> 99MB(O), 1MB(X)

실패, TCP이기 때문에 완전하게 보내야 한다

ex) 영화 파일 다운로드할 때

TFTP(S) -----> TFTP(C)

100MB -----> 99MB(X), 1MB(O)

성공, UDP이기 때문에 전송은 다 했으니까 상관없다

---

HTTP : 웹클라이언트(WC)와 웹서버(WS) 사이에서 평문의 웹문서(HTML)를 송수신해 주는 통신규약

    Apache

HTTPS : 웹클라이언트(WC)와 웹서버(WS) 사이에서 암호화된 웹문서(HTML)를 송수신해 주는 통신규약

    Apache + 인증서 → HTTP + SSL

SHTTP : 웹클라이언트(WC)와 웹서버(WS) 사이에서 암호화된 웹문서(HTML)를 송수신해 주는 통신규약

    Apache + 공개키 → HTTP + SSH

FTP : 평문의 파일을 송수신해 주는 통신규약

FTPS : 암호화시킨 파일을 송수신해 주는 통신규약

    FTP + SSL

SFTP : 암호화시킨 파일을 송수신해 주는 통신규약

    FTP + SSH
