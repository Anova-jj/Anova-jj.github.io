---
title: metasploit을 공부하며 기억해야할 사항
categories: [03_정보보안]
---




## 섹션 1. 사용해보기 #

### modules

- exploit
- auxiliary
- post

- payload
- encoder
- nop


### 둘러보기 
lib 폴더 - msf/, rex/

> msf/core/
> msf/base/sessions

> /rec/post/meterpreter



## 섹션 2. MSF 모듈 #

### msfconsole 가장 기본적인 공식
search - use - info - show - set - (check) - explot(run)

> search keyword -> 모듈 검색

> use 모듈이름 -> 모듈 사용 선언

> info  -> 모듈 세부정보 확인

> show options -> 설정해야하는 옵션들 확인

> set -> 설정

> exploit -> 실제 공격

### msfconsole 명령어
- search
- use
- info 
- set 
- show
- exploit(run) 모듈 실행
- sessions
- jobs

> show 항목
show options
show payload
show targets


### payload 바꾸기
set payload <페이로드 경로>


### 세션 바로 안뜨게 하기

```bash 
exploit -j -z  

sessions #sessions로 떠 있는 명령 확인
sessions -i 1 #1번 세션 접근
```


### 스크립트로 exploit 실행

```bash 

vi 파일명.rc # 스크립트 작성
msfconsole -r 파일명.rc #실행

```



## meterpreter 

메터프리터 기능 사용
1. 내장기능
2. 스크립트(기존)
3. 스크립트 (새)

### extension 사용 #

```bash
use -l  #extension 확인
load <extension> #모듈 로드 -> extension 이 메터프리터에 붙음

```


> 참고- 시작프로그램 등록
reg setval -k HKLM\\software\\microsoft\\windows\\currentversion\\run -v normal -d '올릴 파일 경로'



### 계정 변경하기-incognito 확장 모듈 ##

```bash
list_tokens -u # 계정 목록 보기
impersonate_token user <  > #변경
```



### meterscript 커스텀 스크립트 실행 ##
```bash
use -l  #extension 확인
load <extension> #모듈 로드 -> extension 이 메터프리터에 붙음

``````



### meterpreter 스크립트 사용 ##

```bash
run 스크립트.rb
```


## 모의해킹과 MSF #

### 데이터베이스 핵심 명령어##
1. 데이터베이스 구동
```bash
service postgresql start
msfdb init
```

2. 연결 상태 확인 
```msfconsole
db_status
```

3. 데이터 가져오기/ 내보내기

```msfconsole
db_import
db_export
```

4. 스캐닝


```msfconsole
db_nmap
```


5. db내 정보 확인

```msfconsole
hosts -c address, os_flavor

services -c name,info -S http

creds -a ip -p port -u user -P password

loot
```


