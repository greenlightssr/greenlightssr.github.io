---
layout: single
title: "하드디스크 개념 정리"
date: 2025-02-09
last_modified_at: 2025-02-09
categories:
  - sys/net security
tags:
  - sys/net security
author: hyuna
sidebar:
  nav: "categories"
---

# 하드디스크 개념 정리

## **1. 하드 디스크 구조** 
- **트랙** : 섹터 단위의 모음.
- **섹터** : 하드디스크의 물리적인 최소 단위 (512byte)
- **트랙 섹터** : 같은 구역에 있는 섹터의 집합.
- **클러스터** : 섹터 단위를 묶어놓은 데이터의 입출력 단위. 기본 4096byte.


## **2 Disk Partition** 
- 파티션 : 하드디스크 하나를 논리적으로 나눈 단위
- **MBR** : 하드디스크 파티션 개수, 각 파티션의 시작 주소 등을 가지고 있다. Sector 0번.
- **Primary Partition** : 운영체제가 설치될 수 있으며, 최대 4개 설치 가능하다.
- **Extended Partition** : 확장 파티션. 확장 파티션 안에 논리 파티션을 나눠 쓸 수 있다.
- **Logical Partition** : 논리 파티션. 운영체제 설치 불가하나 데이터 저장용도로 씀. 개수제한 없음


## **3. 하드디스크 추가**
- **1단계 : 하드디스크 추가 (SCSI)**
- **2단계 : 파티션 분할**
  + #ls /dev/sd* : 모든 디스크, 파티션 나열
  + #fdisk -l : 파티션 테이블, 정보 확인
  + #fdisk /dev/sdb -> fdisk 도구로 파티션 생성 가능. (파티션 넘버, 용량, 타입 등) -> 83은 리눅스
  + #ls /dev/sd* : 변경 후 디스크 상태 확인
  + #fdisk -l : 모든 디스크, 파티션 상태 확인. 
- **3단계 : 포맷(파일시스템)**
  + #mkfs.ext4 -v /dev/sdb1 : sdb 파티션 파일 시스템 ext4로 설정
  + 아직 파일 저장은 되지 않는 상태
- **4단계 : 마운트**
  + 하드웨어의 디렉터리화
  + #mkdir /sdb : /sdb 만듦
  + #mount /dev/sdb1 /sdb : sdb1을 sdb로 지정
  + #umount /dev/sdb1 : 마운트 해지 -> 일반 디렉터리 됨.

## **4. 확장 파티션 만들기**
-  fdisk 도구에서 partition type 'e' 선택 : 확장 파티션 선택
- 이후부터는 파티션 분할과 동일하게 진행
