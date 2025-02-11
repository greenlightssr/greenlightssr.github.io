---
layout: single
title: "네트워크(3)"
date: 2025-02-03
last_modified_at: 2025-01-30
categories:
  - sys/net security
tags:
  - network
author: jieon
sidebar:
  nav: "categories"
---

### 날짜: 2025/02/03

### 주제: 네트워크

### 키워드:

---

## 수업 내용:

### Sniffing(도청) 환경이해

- sniffing 환경구성을 위해 wireshark를 설치
  + wireshark 기능 : 패킷 수집 및 분석 , 낮은 수집률

- wireshark 는 무차별 모드를 설정해 패킷을 수신
  + 무차별모드란:
  + 데이터 링크 계층과 네트워크 계층의 주소 필터링을 해제한 모드
  + 주소 지정에 관계없이 호스트의 프로세서에 모든 패킷을 전달

### Packet Sniffing 환경
- 허브 환경에서의 스니핑
  + 허브를 통해 전송되는 트래픽은 해당 허브에 연결된 모드 포트 통과 (플러딩)

### 스위치 환경에서 스니핑 방법
- 포트 미러링 : 네트워크 스위치에서 특정 포트의 트래픽을 다른 포트로 복제하는 기능
- 허빙 아웃 : 스위치가 MAC 주소 테이블을 오버플로우하도록 공격하여 허브처럼 동작하게 만드는 기법
- 탭 사용 : 네트워크 장비 사이에 하드웨어 장비(TAP)를 설치하여 트래픽을 복사, 보안 장비(IDS, IPS)에서 주로 사용됨






## TCP/IP 프로토콜 분석

### TCP/IP Protocol Stack
TCP/IP 프로토콜 스택은 크게 4계층으로 구성되어 있음

- Application Layer (응용계층)
  + 사용자가 직접 사용하는 프로그램(예: 웹 브라우저, 메일 등)이 위치
  + 대표적인 프로토콜: FTP(파일 전송), SSH(원격 접속), Telnet(터미널 접속), HTTP/HTTPS(웹), DNS(도메인 변환), SNMP(네트워크 관리)
  + 각각의 서비스는 포트 번호(Port Number) 를 사용함
    예: HTTP(80번), HTTPS(443번), FTP(21번) 등

- Transport Layer (전송계층)
  + 데이터를 어떤 방식으로 전송할지 결정하는 계층 TCP/UDP

- Network Layer (네트워크 접근 계층)
  + 데이터가 어떤 경로(route)로 가야하는지 결정하는 계층
  + ipv4, icmp, igmp, ARP/RARP

- Network Access Layer (네트워크 접근 계층)
  + 실제 물리적인 네트워크에서 데이터를 전달하는 계층
  + LAN


### Payload & Encapsulation
- 응용 계층 (L7~L5, Application Layer)

  + 사용자가 보낸 원본 데이터 (예: HTTP 요청)
  + 데이터를 그냥 Data 라고 부름
- 전송 계층 (L4, Transport Layer)
  + TCP 또는 UDP 헤더가 추가됨
  + TCP는 포트 번호를 포함 (예: 80번 포트 = 웹)
  + 이 단계에서는 Segment 라고 부름
- 네트워크 계층 (L3, Network Layer)
  + IP 주소를 추가하는 IP 헤더 가 붙음
  + 목적지 IP 주소를 포함하여 어디로 보낼지 결정
  + 이 단계에서는 Packet 이라고 부름
- 데이터 링크 계층 (L2, Data Link Layer)
  + 이더넷 헤더(MAC 주소)와 CRC (오류검출 코드) 추가
  + 오류 검출을 위한 FCS (Frame Check Sequence) 포함
  + 이 단계에서는 Frame 이라고 부름


### TCP Header

- 1.출발지 포트(Source Port) - 16bit
  + 패킷을 보내는 장치의 포트 번호 (예: 12345)

 - 2.목적지 포트(Destination Port) - 16bit
   + 패킷을 받는 장치의 포트 번호 (예: 80 = HTTP)

- 3.순서 번호(Sequence Number) - 32bit
   + 패킷이 전송될 때 데이터의 순서를 추적하는 번호

- 4.응답 번호(Acknowledgment Number) - 32bit
   + 받은 데이터에 대한 확인 응답 번호 (ACK)

 - 5.HLEN (Header Length) - 4bit
   + TCP 헤더의 길이를 나타냄 (기본 20바이트, 옵션 포함 시 최대 60바이트)

 - 6.플래그(Flags) - 6bit
   + TCP 연결 상태를 나타내는 중요한 필드

(밑의 6개를 flag 라고 함)
- URG (긴급 데이터)
- ACK (응답 확인)
- PSH (즉시 전송)
- RST (연결 초기화)
- SYN (연결 요청)
- FIN (연결 종료)

-  7.윈도우 크기(Window Size) - 16bit
   + 한 번에 받을 수 있는 데이터 크기 (흐름 제어)

- 8.체크섬(Checksum) - 16bit
  + 데이터 오류 검출을 위한 값

- 9.긴급 포인터(Urgent Pointer) - 16bit
   + URG 플래그가 설정되었을 때 사용하는 값

- 10.옵션 & 패딩(Options & Padding)
  + 선택적으로 추가 가능한 필드 (예: 타임스탬프, MSS)

---
### TCP 연결관리

### 3-way-handshaking

- SYN       : 클라이언트 -> 서버
- SYN + ACK : 서버 -> 클라이언트
- ACK       : 클라이언트 -> 서버


---
### IP Header

- 1.VER (Version) - 4bit
  + IP 프로토콜 버전 (IPv4: 4, IPv6: 6)

- 2.HLEN (Header Length) - 4bit
  + IP 헤더의 길이 (기본 20바이트, 옵션 포함 시 증가)

- 3.서비스 유형(Service Type) - 8bit
  +  패킷의 우선순위 (QoS, TOS 필드)

- 4.총 길이(Total Length) - 16bit
  + 헤더 + 데이터 포함한 전체 패킷 크기 (최대 65,536바이트)

- 5.식별자(Identification) - 16bit
  + 패킷을 구분하는 고유 ID (단편화된 패킷 재조립에 사용)

- 6.플래그(Flags) - 3bit
  + 패킷 단편화 여부 설정 (예: 더 단편화 가능 여부)

- 7.단편화 오프셋(Fragmentation Offset) - 13bit
  + 단편화된 패킷의 위치를 나타냄

- 8.TTL (Time To Live) - 8bit
   + 패킷이 네트워크에서 살아남을 수 있는 시간 (라우터 지날 때마다 감소, 0이면 폐기)

- 9.프로토콜(Protocol) - 8bit
  + 상위 계층에서 사용하는 프로토콜 정보 (예: TCP=6, UDP=17, ICMP=1)

- 10.헤더 체크섬(Header Checksum) - 16bit
  + 헤더의 오류 검출을 위한 값

- 11.출발지 IP 주소(Source IP Address) - 32bit
  + 패킷을 보내는 장치의 IP 주소

- 12.목적지 IP 주소(Destination IP Address) - 32bit
  + 패킷을 받는 장치의 IP 주소

- 13.옵션(Option) & 패딩(Padding)
  + 선택적으로 추가할 수 있는 필드 (보안, 경로 지정 등)


### 이더넷 프레임 구조

###  1. Ethernet Frame (DIX 2.0) 구조
이더넷 프레임은 기본적으로 **최소 64바이트에서 최대 1518바이트** 까지 사용할 수 있다.

###  Ethernet Frame 필드 설명

| 필드명                 | 크기(바이트) | 설명 |
|----------------------|------------|----------------|
| **Preamble**        | 8  | 수신 장치가 데이터를 준비할 수 있도록 동기화 (전송 시작 표시) |
| **Destination Address** | 6  | 목적지 MAC 주소 |
| **Source Address**      | 6  | 출발지 MAC 주소 |
| **Type**                | 2  | 상위 프로토콜 식별 (예: IPv4 = 0x0800, ARP = 0x0806) |
| **DATA**                | 46~1500 | 전송할 실제 데이터 (페이로드) |
| **FCS (Frame Check Sequence)** | 4  | 오류 검출을 위한 CRC 값 |



###  2. IEEE 802.3 & IEEE 802.2 구조
IEEE 802.3 표준에서는 **Type 필드 대신 Length 필드** 를 사용하고,
상위 계층을 구분하기 위해 **IEEE 802.2 헤더** 를 추가했다.

###  IEEE 802.3 필드

| 필드명                  | 크기(바이트) | 설명 |
|----------------------|------------|----------------|
| **Preamble**        | 7  | 동기화 신호 |
| **SFD (Start Frame Delimiter)** | 1  | 프레임의 시작을 알림 |
| **Destination Address** | 6  | 목적지 MAC 주소 |
| **Source Address**      | 6  | 출발지 MAC 주소 |
| **Length**              | 2  | 데이터의 길이 (최대 1500바이트) |
| **802.2 Header**        | 3+ | 상위 프로토콜 식별 |
| **DATA**                | 42~1497 | 전송할 데이터 |
| **FCS**                 | 4  | 오류 검출 |

---






<br>

## !! 문제 3개 !!

### Q1.

### Q2.

### Q3.

---

<br>

### A1.

### A2.

### A3.
