---
layout: single
title: "네트워크(4)"
date: 2025-02-04
last_modified_at: 2025-01-30
categories:
  - sys/net security
tags:
  - network
author: jieon
sidebar:
  nav: "categories"
---

### 날짜: 2025/02/04

### 주제: 네트워크

### 키워드: MTU, Fragmentation, TCP/UDP, ICMP, ARP

---

## IP 프로토콜

### IP 필드

- Ip 프로토콜의 패킷은 Ip Header + Data 로 구성
- IP 프로토콜 사용시 Data 는 필수

### MTU

- 네트워크 각각각 전송할 수 있는 최대 전송 단위
- 현재 대부분 네트워크 환경이기에 MTU는 **1500byte**가 통용
- 전송할 byte가 크다면 단편화 필요

### Fragmentation (단편화)

- 3,4 계층에서 작업해야 하나 4계층은 패스 가능
- 송신자는 단편화
- 수신자는 재조립

### 단편화와 관련된 필드

- ip 에서 flag가 1이면 뒤에 더 있음
- fragmention offset에서 패킷 위치를 나타냄
- 단편화가 진행된 경우 identification 값이 같음

### MTU 설정 변경 코드

```
C:\> netsh interface ipv4 set subinterface “6" mtu=9000 store=persistent
C:\>netsh interface ipv4 show global
```

### TTL (time to live)

- 패킷 수명을 제한하기 위해 데이터그램이 통과하는 최대 **홉(hop)**수

### TTL 설정변경

```
C:\> netsh interface ipv4 set global defaultcurhoplimit=64
C:\>netsh interface ipv4 show global
```

### Header checksum

- **ip 는 ip header 부분만 오류 검출**
  - 이유 : IP 패킷은 경로를 따라 라우터에서 TTL(Time To Live) 등이 변경될 수 있는데, 전체 데이터까지 포함하면 체크섬을 계속 다시 계산해야 함 → 비효율적
- **tcp 는 전체 오류 검출**

  - 이유 : TCP는 신뢰성 보장이 중요한 프로토콜이라서 데이터까지 포함해 오류를 검출해야 함

- 송신자 : 헤더 체크썸 필드를 제외한 모든 필드를 더한다(16진수 덧샘), 그리고 체크썸 필드기록 후 전송한다.
- 수신자 : 수신한 데이터의 헤더 체크썸 필드를 제외한 모든 필드를 더하고, 해당 값이 체크썸 필드와 같는지 확인해 무결성을 검사한다.
- header checksum 계산방법 : 송신자 측에서는 IP header에서 Header checksum 제외 값을 모두 더한 후 Header checksum 에 넣는다.

## TCP / UDP

### TCP

- 연결지향, 스트림 (stream)기반
- 데이터를 세그먼트(segment) 단위로 처리
- **네트워크 단편화 가능**
  - tcp는 연속적인 데이터 흐름을 다루기에 전송할 데이터를 분활하여 전송
  - 만약 MTU 를 초과하면 IP 계층에서 단편화 하여 전송
- TCP 단편화 과정
  - 애플리케이션에서 큰 데이터를 보냄
  - TCP가 데이터를 세그먼트(Segment) 단위로 나눔
  - 각 TCP 세그먼트가 IP 패킷으로 캡슐화됨
  - IP 계층에서 MTU보다 크면 단편화(Fragmentation) 진행
  - 수신 측에서 TCP가 세그먼트를 재조립하여 원래 데이터 복원

### UDP

- 비연결지향, 메시지 기반
- 데이터를 데이터그램 단위로 처리
- **네트워크 단편화 없음**

### MSS (Maximum Segment Size)

- TCP에서 한 번에 전송할 수 있는 최대 데이터 크기
- TCP가 IP 패킷의 크기를 고려하여 세그먼트(Segment) 크기를 결정할 때 사용되는 값
  - **MSS = MTU - (IP 헤더 + TCP 헤더) ex\_ MSS = 1500 - 20 + 20 = 1460**
  - MSS는 TCP 세그먼트에서 "데이터(payload)"의 최대 크기

## ICMP (Ineternet Control Message Protocol)

**오류 메시지를 보고하고, 네트워크 상태를 진단하는 프로토콜**

### ICMP Header

| 필드               | 크기 (비트) | 설명                    |
| ------------------ | ----------- | ----------------------- |
| **Type**           | 8           | ICMP 메시지의 유형      |
| **Code**           | 8           | Type에 대한 세부 코드   |
| **Checksum**       | 16          | 오류 검출을 위한 체크섬 |
| **Rest of Header** | 32          | 메시지 유형에 따라 다름 |

### ICMP 오류 메시지

| Type   | Code | 설명                        |
| ------ | ---- | --------------------------- |
| **3**  | 0    | 네트워크 도달 불가          |
| **3**  | 1    | 호스트 도달 불가            |
| **3**  | 2    | 프로토콜 도달 불가          |
| **3**  | 3    | 포트 도달 불가              |
| **3**  | 4    | 단편화 필요                 |
| **3**  | 13   | 통신 필터링됨               |
| **5**  | 0    | 네트워크 리디렉션           |
| **5**  | 1    | 호스트 리디렉션             |
| **11** | 0    | TTL 초과                    |
| **11** | 1    | 프래그먼트 재조립 시간 초과 |

### ICMP 정보 메시지

| Type   | Code | 설명                     |
| ------ | ---- | ------------------------ |
| **0**  | 0    | Echo Reply (ping 응답)   |
| **8**  | 0    | Echo Request (ping 요청) |
| **9**  | 0    | Router Advertisement     |
| **10** | 0    | Router Solicitation      |

### ICMP 예시 (Ping 메시지)

- ICMP Echo Request (ping 요청)

```
Type: 8
Code: 0
Checksum: 0x4d5a
Identifier: 0x1234
Sequence Number: 0x0001
Data: (패킷의 데이터 부분)
```

- ICMP Echo Reply (ping 응답)

```
Type: 0
Code: 0
Checksum: 0x5bcd
Identifier: 0x1234
Sequence Number: 0x0001
Data: (요청과 동일한 데이터)
```

## ARP (Address Resolution Protocol)

### ARP Request 패킷

- **브로드캐스트(FF:FF:FF:FF:FF:FF)로 전송**되며, 네트워크에 있는 모든 장비가 요청을 받음

```Opcode: 1 (Request)
Sender MAC: 11:11:11:11:11:11 (클라이언트)
Sender IP: 192.168.1.10
Target MAC: 00:00:00:00:00:00 (모름)
Target IP: 192.168.1.20 (서버)
```

### ARP Reply 패킷

- **유니캐스트(1:1 통신)**로 요청한 장비에게만 전송

```
Opcode: 2 (Reply)
Sender MAC: 22:22:22:22:22:22 (서버)
Sender IP: 192.168.1.20
Target MAC: 11:11:11:11:11:11 (클라이언트)
Target IP: 192.168.1.10
```

### ARP request, reply 과정

- 클라이언트가 ARP Request 전송
  - 목적지 IP의 MAC 주소를 모름 → Broadcast(FF:FF:FF:FF:FF:FF)로 요청
- 서버 응답
  - 자신의 MAC 주소(22:22:22:22:22:22)를 클라이언트 에게만 응답 (Unicast)
- 클라이언트는 ARP Cache Table에 서버 MAC 주소 저장
  - **잘못된 MAC 주소도 저장**하기에 악용 가능 (취약점)

---

<br>

## !! 문제 3개 !!

### Q1. 다음 중 IP 프로토콜의 특징으로 올바르지 않은 것은?

1. IP 프로토콜은 패킷을 전달하기 위한 헤더(Header)와 데이터(Data)로 구성된다.
2. MTU 는 일반적으로 1500바이트가 기본값이다.
3. TTL 은 패킷이 통과할 수 있는 최대 거리(거리 벡터)를 의미한다.
4. IP 헤더의 Checksum은 IP 헤더만을 대상으로 오류를 검출한다.

### Q2. TCP와 UDP에 대한 설명으로 옳지 않은 것은?

1. TCP는 연결 지향적이며 신뢰성이 높은 전송을 제공한다.
2. TCP는 데이터를 스트림(Stream) 단위로 처리하며, UDP는 데이터그램(Datagram) 단위로 처리한다.
3. TCP는 단편화를 수행할 수 없으며, UDP만 네트워크 단편화를 수행할 수 있다.
4. UDP는 헤더 크기가 작아 오버헤드가 적고, 빠른 전송이 가능하다.

### Q3. ARP에 대한 설명 중 틀린 것은?

1. ARP Request는 브로드캐스트 방식으로 네트워크에 있는 모든 장비에게 전송된다.
2. ARP Reply는 요청한 장비에게만 유니캐스트 방식으로 전송된다.
3. ARP는 IP 주소를 MAC 주소로 변환하는 역할을 한다.
4. ARP Reply는 반드시 브로드캐스트 방식으로 전송되어야 한다.

---

<br>

### A1. 3

### A2. 3

### A3. 4
