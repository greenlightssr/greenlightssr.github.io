---
layout: single
title: "OSI 7 참조모델"
date: 2025-02-18
last_modified_at: 2025-02-18
categories:
  - sys/net security
author: seonyeong
sidebar:
  nav: "categories"
---
## ※ OSI 7 참조모델

* ISO가 서로 다른 시스템간의 통신을 허용하기 위해 만든 모델
* 네트워크가 제공하는 여러 가지 기능을 7개 계층으로 나눔

![](https://blog.kakaocdn.net/dn/cBdg7u/btsLYLo8G8L/kExaLeLqwPQkOktYEVtFok/img.webp)

상위 3계층(Software 기능)

중계 계층(Middleware 기능)

하위 3계층(Hardware 기능)

#### 7) 응용 계층 (Application Layer)

* UI 제공
* UI를 통해 데이터 생성
* HTTP, FTP, Telnet, SMTP, SNMP, Telnet, NFS...

#### 6) 표현 계층 (Presentation Layer)

* 인코딩(encoding, 부호화) : 2진화, ASCII, UNICODE (무조건 필수 기능)
* 압축화 : bmp, png, zip 등(압축할 필요 없으면 진행이 안 될 수도 있다.)
* 암호화 : DES, RSA 등(보안이 중요하지 않다면 진행이 안 될 수도 있다.)

#### 5) 세션 계층 (Session Layer)

* 양단간에(End-to-End) 서비스를 개시(인증, 인증값 할당), 유지(지속적 인증), 해지(인증 만료)
* 구체적인 서비스 확인
* SSL

#### 4) 전송 계층 (Transport Layer)

* 양단간에 가상회선(virtual Circuit) 설정(서버 활성화, 서비스 제공 가능 상태), 유지(서비스 제공 유지 중), 해지(서비스 중지)
* 3-way handshake로 가상회선 설정
* end-point = host (양단간)
* 가상회선 수립 = 세션 수립 = 채널이 열렸다
* 서로간의 활성화 여부 확인, 상태 확인

#### 3) 네트워크 계층 (Network Layer)

* 최적 경로 결정(Routing)

Router : 기기

Routing : 최적 경로를 선정하는 작업

Route : 최적 경로

#### 2) 데이터 링크 계층 (Data Link Layer)

* 데이터 전달(forwarding)
* 오류제어(error control)
* 매체접근제어(media access control)

LAN 2계층 구간 (switch)

→ 장비를 공유

→ 충돌

→ 재전송

→ 전송 지연

= (공유) 매체 접근 제어 기술(충돌 방지 기술)

통신제어에서 오류제어란 수신된 데이터에서 오염이 있는지 없는지 점검하는 것

오류점검코드를 별도로 추가해서 보낸다.

<잠깐 상식!> CSMA/CD 방식. 충돌 안일어나게...유랜카드에 들어있음 그 기술 들어간 랜카드가 이더넷카드

#### 1) 물리 계층 (Physical Layer)

* 기계적 특성 : 커넥터의 크기, 핀의 개수 및 위치 등의 규격
* 전기적 특성 : 전송매체 전류 및 전압 특성, 전송속도, 최대 전송 거리 등을 규정
* 기능적 특성 : 커넥터의 각 핀의 기능을 규정
* 절차적 특성 : 각 핀의 신호화 주고 받는 순서에 대한 규정
