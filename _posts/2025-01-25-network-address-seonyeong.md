---
layout: single
title: "네트워크 주소"
date: 2025-01-26
last_modified_at: 2025-01-26
categories:
  - sys/net security
author: seonyeong
sidebar:
  nav: "categories"
---

## ※ 네트워크 주소

• MAC Address(2계층 주소)

• IP Address(3계층 주소)

• Port number(4계층 주소)

• FQDN(7계층 주소)

### 1. 논리적 주소 (3계층 주소)

존재하고 있는 논리적 주소 종류

Appletalk

IPX

IP - 바로 우리가 사용하고 있는 컴퓨터 주소

IP address 구성

- Network ID + Host ID

Subnet Mask 기능

- IP address의 Network ID와 Host ID 구분

IP 주소에 서브넷 마스크를 씌우면 네트워크 ID가 나온다.

![](https://blog.kakaocdn.net/dn/ZTjgq/btsLXXI4Yuk/Toq4X2YBF7E9n9qLtKSFkk/img.png)

&연산을 하면 이 컴퓨터는 192.168.1.0 망의 10번째라는 것을 알 수 있다.

(네트워크 ID : 192.168.1 호스트 ID : 10)

네트워크 ID가 동일하다면

송신자는 수신자가 내부망에 있다고 생각

다르다면 외부망

### 2. 물리적 주소 (2계층 주소)

LAN card 종류

- Token ring
- FDDI
- Ethernet -> MAC address 이더넷 랜카드의 물리적 주소

MAC 주소(16진수)

ex) 00-40-D0-15-81-C5

앞의 6자리는 제조회사 식별번호(OUI) 뒤의 6자리는 카드 일련번호(UAA)

○  IP address 충돌

- 수정하면 됨

○  MAC address 충돌

- 두 컴퓨터의 MAC address가 같을 때 발생

원래는 충돌이 일어날 수가 없다 만들 때부터 빌트인 된 번호이기 때문에...

하지만 랜카드를 복제했을 때 충돌!

IP address 못지않게 MAC address도 중요해용

### 3. Fully Qualified Domain Name (FQDN, 7계층 주소)

server : 서비스 제공자

client : 서비스를 받는 자

Host Name + Domain Name

ex) www.test.com

일반적으로 public 한 사이트들은 호스트명을 프로토콜명으로 두는 경우가 많다. www

인간이 이해 가능하도록 숫자 진화

3333.4444.5555 인간을 주민등록번호로 이름 부르는 것과 같음

↓

192.168.1.20 10진수로 변화

↓

www.test.com 와 이해하기 쉽다(근데 돈내야됨)

#### ▷ DNS & ARP

네트워크 주소 관련 프로토콜

DNS : 문자주소를 IP주소로 알 수 있게 해주는 것. lookup(조회). 그 반대도 DNS, 2가지 기능을 함

ARP : IP주소를 통해서 MAC주소를 알 수 있게 해주는 것. 그 반대는 RARP MAC주소로 IP주소 암

문자주소에서 바로 MAC주소 알아내는 통신규약은 없다.

### 4. Port number (4계층 주소)

- 프로그램에 부여되는 번호

아파트로 생각하면 몇 번지인지

ex) 아파트 1동 65535 가 있다.

192.168.1.10 아파트 정문에 도착

192.168.1.10:3 아파트 3호에 도착

![](https://blog.kakaocdn.net/dn/mJZBy/btsLVxZGRcb/EugULl853RiGgVQ14TQCjK/img.png)

2의 16제곱 = 65535(외워두자) 0~65536

서버용 프로그램에 부착되는 번호 Well-Known Port (정적)

클라이언트용 프로그램에 부착되는 번호 Dynamic Port (동적)

서버용 프로그램 설치

환경설정

- 포트설정

web server : 80, 443

ftb server : 20, 21

telnet server : 23

모두 다 Well-Known Port~

○ 포트 번호 충돌

- 하나의 컴퓨터의 여러 프로그램에 동일한 포트 번호가 부여됐을 때
- 실제로 충돌은 일어나지 않음. 회피 정책을 쓰고 있다.

<C:\Windows\System32\drivers\etc services 파일 열면 port number랑 protocol 나오니까 확인>

만약에 http://naver.com에 접속을 한다고 가정하자

http는 80번이라서 뒤에 포트번호를 입력하지 않아도 자동으로 접속이 된다

근데 server가 8000번으로 포트번호 바꿨어요 여기로 들어오세요 한다면?

http://naver.com:8000 이렇게 쳐도 됨

뒤에 포트번호가 우선시 되기 때문!!!
