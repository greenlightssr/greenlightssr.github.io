---
layout: single
title: "계층별 장비와 트래픽 흐름"
date: 2025-02-18
last_modified_at: 2025-02-18
categories:
  - sys/net security
author: seonyeong
sidebar:
  nav: "categories"
---
게이트웨이 기능

- 망과 망을 연결시켜 주는 것
- 라우터, 멀티레이어 스위치, 게이트웨이(방화벽)

게이트웨이 원칙

내부망을 써야 한다.

192.168.1.254라면 무조건 1.254 써야 됨

1.3 쓰면 접속 못한다.

ping 192.168.1.10 보냈을 때 순서

1. arp request
2. arp reply
3. echo-request
4. echo-reply

## ※ 계층별 장비

### • Switch (2계층)

### • Router (3계층)

### • Hub (1계층) - 주소X

### ▷ Forwarding과 Flooding

• Forwarding : 하나의 송신지 포트에서 하나의 수신지 포트로 트래픽 전송(효율적)

• Flooding : 송신지 포트를 제외한 나머지 포트들로 트래픽 전송(비효율적)

### 1. Switch (2계층 장비)

- 경로데이터 베이스 : MAC Address Table
- 전송방식

  - 포워딩 : 목적지 정보가 경로데이터베이스에 있는 경우
  - 플러딩 : 목적지 정보가 경로데이터베이스에 없는 경우
- 브로드캐스트/멀티캐스트 패킷 : 플러딩 방식으로 전송

경로데이터베이스에는 브로드캐스트/멀티캐스트 주소는 등록되지 않음(FFFF. 0105E 이런거)

### 2. Router (3계층 장비)

- 경로데이터베이스 : Routing Table
- 전송방식

  - 포워딩 : 목적지 정보가 경로데이터베이스에 있는 경우
- 목적지 정보가 경로데이터베이스에 없는 경우 폐기(drop)
- 브로드캐스트/멀티캐스트 패킷 : 폐기(drop)

routing table은 IP가 정확하게 나오지 않음

1.0에서 4.0으로 가려는데 출구번호가 없다?

그렇다면 폐기

스위치는 모르는 경우에는 플러딩 방식을 하는데 라우터는 그냥 폐기해버린다는 점이 있다.

### 3. HUB (1계층 장비)

- 경로데이터베이스 : 없음
- 전송방식 : 모든 데이터(유/멀/브)를 플러딩 방식

<간단 요약>

허브 : 플러딩

스위치 : 플러딩/포워딩

라우터 : 포워딩



arp -a

-> ARP 캐시테이블

IP address : MAC address

MAC address table

MAC address : 출구번호

ipconfig /displaydns

-> DNS 캐시테이블

문자주소 : IP주소

nslookup www.naver.com

ping www.naver.com

ipconfig /flushdns

---

## ※ 트래픽 흐름

### 내부망

1 단계) DNS를 이용하여 수신지 IP 주소 조회

- DNS 캐시 조회 (c:\> ipconfig /displaydns)
- Hosts.txt 파일 조회 (\windows\system32\drivers\etc\hosts)
- DNS 서버 이용

2 단계) 송신자 서브넷 마스크를 이용하여 수신지가 (내부망/외부망)에 존재하는지 확인

3 단계) 수신지 MAC 주소 조회

- ARP 캐쉬 조회
- ARP Request/Reply 를 이용

4단계) 수신지로 트래픽 전송

서버의 IP를 안다면 1단계 생략 가능

수신지의 서브넷마스크를 모르기 때문에 송신지 수신지 IP주소에 송신지의 서브넷마스크를 이용하여 내부망인지 외부망인지 확인을 한다.

![](https://blog.kakaocdn.net/dn/Zn3xp/btsLX9RvXqn/N1glOQMjLkvBdUrAzigbA1/img.png)
송신지

![](https://blog.kakaocdn.net/dn/b6DinW/btsLYPSpwM0/7kgnkuCHNijELg2IlhWXx1/img.png)
수신지

네트워크 ID가 동일하니 내부망이다.

스위치는 플러딩써서 데이터를 전송하기 때문에 막혀있어도 어떻게든 전송은 한다.

### 외부망

1 단계) DNS를 이용하여 수신지 IP 주소 조회

- DNS 캐시 조회 (c:\> ipconfig /displaydns)
- Hosts.txt 파일 조회 (\windows\system32\drivers\etc\hosts)
- DNS 서버 이용

2 단계) 송신자 서브넷 마스크를 이용하여 수신지가 (내부망/외부망)에 존재하는지 확인

3 단계) GateWay의 MAC 주소 조회

- ARP 캐쉬 조회
- ARP Request/Reply 전송

4단계) Media Translation 방법으로 수신지로 트래픽 전송

broadcast domain

2개

1개

외부망일 때는 수신지 MAC address에 게이트웨이 MAC address가 온다.

ARP request, reply는 나갈 수 밖에 없다.
