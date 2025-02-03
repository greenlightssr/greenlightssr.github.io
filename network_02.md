### 날짜: 2025/01/24

### 주제: 네트워크

### 키워드:  Mdia Translation, 트래픽 흐름, OSI 7 참조모델, TCP/IP 프로토콜

---

### 수업 내용:

### 트래픽 흐름

#### - 내부망 : 스위치 사용( 게이트웨이 사용 안함)

#### - 외부망 : 라우터 사용 (게이트웨이 사용, 망분리)

---



#### 내부망 트래픽 흐름 

- 1단계 : DNS를 이용하여 수진지 IP주소 조회  (서버 ip를 안다면 생략 가능)
  + DNS 캐쉬 조회: ipconfig / displaydns
  + Host.txt 파일 조회 : \windows\system32\drivers\etc\hosts
  + DNS 서버 : DNS Request / Response
- 2단계 : 서브넷 마스크를 이용하여 수신자 내부망/외부망 확인
- 3단계 : ARP를 이용하여 수신자 MAC주소 조회
  + ARP 캐쉬 조회
  + ARP Request / Reply 이용
- 4단계 : 수신지로 트래픽 전송


#### 외부망 트래픽 흐름

- 1단계 : DNS를 이용하여 수신 IP 주소 조회
- 2단계 : 서브넷마스크를 이용하여 수신자 내부망/외부망 확인
- 3단계 : ARP를 이용하여 수신자 MAC 주소 조회
- 4단계 : Media Translation 방법으로 수신지로 트래픽 전송

---

![1737880390285](image/network_01(1)/1737880390285.png)

- 7계층 (Application Layer)
  + UI를 통해 데이터 생성
  + 대다수 사용자 인지하는 게층은 7계층
  + HTTP UI 폼 결정으로 인해 대부분의 웹 브라우저 형식이 비슷하다
- 6계층 (Presentation Layer)
  + code 변환 (encoding(아스키, 유니코드))
  + 압축 (bmp, png, zip)
  + 암호화 (DES, RSA)
- 5계층 (Session Layer)
  + 서비스 개시 (인증, 인증 값 할당)
  + 서비스 유지 (지속적 인증)
  + 서비스 해지 (인증 값 완료)
- 4계층 (Transport Layer)
  + End to End 호스트 간 가상회선 설정
  + 상태확인
- 3계층 (Network Layer)
  + Router (기기)
  + Routing (최적 경로를 선정하는 작업)
  + Route (최적경로)
- 2계층 (Data Link Layer)
  + 데이터 전달
  + 오류 제어
  + LAN : 장비를 공유 => 충돌 => 재전송 => 전송지연 문제 발생 => 매체접근제어로 문제 해결(media access control)
- 1단계 (Physical Layer)
  + 전기적, 기계적, 기능적, 정차적인 수단 제공


#### OSI 7 계층 PDU (protocol data unit)

- L7 ~ 5 : Message, Data
- L4 : segment == datastream ==> port
- L3 : packet == datagram ==> IP address
- L2 : frame
- L1 : bit

---

![1737881259580](image/network_01(1)/1737881259580.png)

---

<br>

## !! 문제 3개 !!

### Q1. 내부망 트래픽 흐름에서 DNS를 이용하여 수신지 IP 주소를 조회하는 단계에서 참조할 수 있는 정보가 아닌 것은 무엇인가?

1. DNS 캐쉬
2. Host.txt 파일
3. DNS 서버
4. 서브넷 마스크

### Q2. OSI 7 계층에서 데이터의 압축 및 암호화와 관련된 계층은 무엇인가?

1. 5계층
2. 6계층
3. 4계층
4. 3계층

### Q3. 외부망 트래픽 흐름에서 라우터를 통해 최적 경로를 설정하고 데이터 전송을 관리하는 OSI 계층은 무엇인가?

1. 4계층
2. 3계층
3. 2계층
4. 1계층

---

<br>

### A1. 4

### A2. 2

### A3. 2
