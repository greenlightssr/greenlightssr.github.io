---
layout: single
title: "system_security"
date: 2025-02-16
last_modified_at: 2025-02-16
categories:
  - sys/net security
author: doyoon
sidebar:
nav: "categories"

---

# 시스템 보안

## [마운트(Mount)](pplx://action/followup)

하드웨어 디바이스나 파티션을 특정 디렉터리에 연결하여 파일 시스템으로 접근할 수 있게 하는 과정

---

## [하드 링크(Hard Link)](pplx://action/followup)

- **[생성 방법](pplx://action/followup)**: `ln test test_ln`
- 동일한 inode 번호를 공유하여 하나의 파일을 여러 이름으로 접근할 수 있다.
- 원본 파일을 삭제해도 링크된 파일은 그대로 유지된다.

---

## [소프트 링크(Soft Link, 심볼릭 링크)](pplx://action/followup)

- **[생성 방법](pplx://action/followup)**: `ln -s test test_sl`
- 별도의 inode를 가지며, 원본 파일의 경로를 참조하는 방식
- 원본 파일이 삭제되면 링크도 유효하지 않게 된다.

---

## [inode 정보 확인](pplx://action/followup)

`stat` 명령어를 사용하여 파일의 inode 번호 및 메타데이터를 확인할 수 있다.
예시: `stat test`

---

# 파일 시간 정보

- **[Access Time(액세스 시간)](pplx://action/followup)**: 파일이 마지막으로 읽힌 시간.
- **[Modify Time(수정 시간)](pplx://action/followup)**: 파일의 내용이 마지막으로 변경된 시간.
- **[Change Time(상태 변경 시간)](pplx://action/followup)**: 파일의 메타데이터(권한, 소유자 등)가 변경된 시간.

---

# 파일 및 디렉터리 검색

- **[find 명령어](pplx://action/followup)**: 특정 조건에 맞는 파일이나 디렉터리를 검색
  - **[형식](pplx://action/followup)**: `find [경로] [조건] [액션]`
  - **[예시](pplx://action/followup)**: `find ./ -perm -4000` (SET_UID가 설정된 파일 찾기)

---

# 권한 관리와 특수 권한

## [기본 권한 설정](pplx://action/followup)

- **[umask](pplx://action/followup)**: 새로 생성되는 파일이나 디렉터리의 기본 권한을 결정

## [특수 권한](pplx://action/followup)

1. **[SetUID (s)](pplx://action/followup)**:
   - 실행 파일에 설정되며, 실행 시 해당 파일의 소유자 권한으로 동작
2. **[SetGID (s)](pplx://action/followup)**:
   - 실행 파일이나 디렉터리에 설정되며, 생성되는 파일이 해당 그룹을 상속
3. **[Sticky Bit (t)](pplx://action/followup)**:
   - 디렉터리에 설정되며, 파일 삭제 권한을 해당 파일의 소유자나 디렉터리 소유자만 가지게 한다.
   - **[설정 방법](pplx://action/followup)**: `chmod +t [디렉터리명]` 또는 `chmod 1XXX [디렉터리명]`

---

# 루트킷(Rootkit)

## [정의](pplx://action/followup)

시스템에 대한 무단 접근 권한을 얻기 위해 사용되는 악성 코드 또는 도구 모음.

## [특징](pplx://action/followup)

- 탐지와 제거가 매우 어렵다
- 주요 기능:
  1. 권한 상승
  2. 은닉성

---

# 사용자 및 그룹 관리

## [사용자 관리](pplx://action/followup)

1. **[사용자 생성](pplx://action/followup)**: `adduser [사용자명]`
2. **[사용자 정보 확인](pplx://action/followup)**:

   - `/etc/passwd` 파일:
     - 모든 사용자 정보 포함.
     - 형식: `로그인ID:패스워드자리:UID:GID:사용자 정보:홈 디렉터리:로그인 셸`
     - 실제 암호는 `/etc/shadow`에 저장됨.
3. **[패스워드 저장 구조 (/etc/shadow)](pplx://action/followup)**:

   - 형식: `$id$salt$hashed_password`
     - `id`: 해시 알고리즘 식별자.
     - `salt`: 해시에 사용된 솔트 값.
     - `hashed_password`: 솔트와 함께 해시된 비밀번호.
4. **[사용자 관리 명령어](pplx://action/followup)**:

   - 비밀번호 설정/변경:
     - `passwd [사용자명]`: 비밀번호 설정 또는 변경.
     - `passwd -l [사용자명]`: 계정 잠금.
     - `passwd -u [사용자명]`: 계정 잠금 해제.
   - 사용자 수정:
     - `usermod`: 사용자 계정 정보 수정.
   - 사용자 삭제:
     - `userdel [사용자명]`: 계정 삭제.
     - `userdel -r [사용자명]`: 계정과 홈 디렉터리 삭제.

---

# PAM(Pluggable Authentication Modules)

## [정의](pplx://action/followup)

다양한 인증 방식을 플러그인 형태로 제공하여 유연한 인증 체계를 구축할 수 있게 하는 시스템.

## [특징](pplx://action/followup)

1. 유연성: 다양한 모듈 조합으로 원하는 인증 방식 구현 가능.
2. 확장성: 새로운 인증 모듈 추가 가능.
3. 일관성: 중앙에서 인증 정책 관리 가능.

## [구성 요소](pplx://action/followup)

1. **[auth](pplx://action/followup)**: 사용자 신원 확인 및 인증.
2. **[account](pplx://action/followup)**: 계정 상태 확인 및 접근 권한 제어.
3. **[password](pplx://action/followup)**: 비밀번호 변경 처리.
4. **[session](pplx://action/followup)**: 세션 시작 및 종료 시 필요한 작업 수행.

## [제어 플래그](pplx://action/followup)

- `required`: 실패 시 전체 인증 실패, 모든 모듈 실행 후 결과 반환.
- `requisite`: 실패 시 즉시 인증 실패, 이후 모듈 실행 중단.
- `sufficient`: 성공 시 즉시 인증 성공, 이후 동일 유형 모듈 실행 중단.
- `optional`: 성공 여부가 전체 인증 결과에 큰 영향 없음.
