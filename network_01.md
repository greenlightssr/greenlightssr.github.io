### 날짜: 2025/01/23
### 주제: 네트워크
### 키워드: (유니,브로드,멀티)캐스트, (허브,스위치,라우터), (플러딩,포워딩)

<br>

---
### 수업 내용:

- 논리적 주소: 
  + Appletalk
  + IPX
  + IP (내 컴퓨터가 사용하는 주소)

- LAN card:
  + Token ring
  + FDDI
  + Ethernet ==> MAC address

- server : 서비스 제공자
- client : 서비스를 받는자

- DNS: 문자주소 -> ip 주소  *lookp(조회)
- ARP : ip주소 -> MAC주소
- RARP :  MAC -> ip주회

- 서버용 프로그램 설치 > 환경설정 > 포트설정(웰노운)

- C:\Windows\System32\drivers\etc
- <service name>  <port number>/<protocol>  [aliases...]   [#<comment>]

- 브로드캐스트 주소
  + 가상주소
  + 시스템/애플리케이션 운영 시 사용하는 주소

- 시스템:운영체제
  + BIP : 255.255.255.255
  + BMAC : FF.FF.FF.FF.FF.FF
  + 운영제체가 설치 시 할당 됨


- 멀티캐스트 주소
  + 가상주소
  + 시스템/애플리케이션 운영 시 사용하는 주소
  + 시스템:운영체제
  + MIP : 224~239

- MMAC: 0100.5E
  + 운영체제가 설치 시 할당 됨
  + 애플리케이션 설치 시 할당 됨

- arp -a 
- arp 캐시 테이블 = IP address : MAC address

- 게이트웨이 기능
  + 망과 망을 연결 시켜주는 것
  + 라우터, 멀티레이어 스위치, 게이트웨이(방화벽)

- ping
  + echo-request
  + echo-reply

- 데이터를 전달하는 방법
  + 포워딩 방식
  + 플러딩 방식

- 허브
  + 1계층
  + 경로데이타베이스 : 없음
  + 전송방식 : 모든 데이터 (유/멀/브)를 플러딩 방식

- 스위치
  + 2계층
  + 경로데이타 베이스 : MAC Address table
  + 전송방식
  + 포워딩 : 목적지 정보가 경로데이타베이스에 있는 경우
  + 플러딩 : 목적지 정보가 경로데이타베이스에 없을 경우
  + 브로드캐스트/멀티캐스트 패킷: 플러딩 방식으로 전송

- 라우터
  + 3계층 장비
  + 경로데이타베이스 : routing table
  + 전송방식
  + 포워딩 : 목적지 정보가 경로데이터베이스에 있는 경우
  + 목적지 정보가 경로데이타베이스에 없는 경우 폐기

-경로데이타베이스에는 브로드캐스트/멀티캐스트 주소는 등록되지 않음

-허브    : 플러딩
-스위치 : 플러딩/포워딩
-라우터 : 포워딩

-플러딩: 스위치가 목적지 주소를 모를 때, 데이터를 모든 포트로 전달
-포워딩: 목적지 주소를 알고 데이터를 정확한 경로로 전달



---

<br>

## !! 문제 3개 !!

### Q1. DNS 기능



### Q2. 게이트웨이 기능



### Q3. Multicast IP/MAC 주소 범위    

---

<br>

### A1. (문자 주소를 MAC 주소로 변환)

### A2. (망 간 연결에 사용된다)

### A3. (224~239)
