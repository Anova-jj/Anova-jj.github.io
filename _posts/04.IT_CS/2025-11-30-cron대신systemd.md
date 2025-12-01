---
title: crontab 대신 systemd로 스케쥴링하자!
categories: [04_IT_CS]
---


## 개요#

배치 프로그램과 같은 주기적인 쉘스크립트를 실행하기 위해서
리눅스에서는 cron 데몬을 사용한다.



cron 시스템을 사용하면 다양한 장점이 있겠지만 무엇보다 쉽고 간단하게
스케쥴링 작업을 할 수 있다는게 가장 큰 장점이다.



그럼에도 불구하고 cron 프로그램 대신에 systemd로 조금씩 전환하려는 이유는 이벤트기반의 스케쥴링도 가능하고, 로그도 유연하게 사용 가능하기 때문이다!!

~~사실 cron이 나중에 안쓰이게 될 것 같아서 얼른 systemd으로 하는 연습을 해놔야할 것 같다.~~


아치 리눅스에서는 cron을 기본적으로 지원하지 않기도하고, systemd도 익숙해 지면 좋으니 자주 쓰면서 연습좀 해놔야겠다.




## 동작순서#

1. Timer
2. Service
3. 쉘스크립트




## Timer 주요 시간 방식#

> Monotonic timer , Realtime Timer

- Monotonic timer (상대 시간)


특정 이벤트(부팅, 서비스 시작 등) 기준으로 시간이 흐른 뒤 실행


ex) OnBootSec=15min: 부팅 후 15분 뒤 실행


- Realtime Timer (달력 시간)

ex) OnCalendar = \[요일] 년-월-일 시:분:초





## Timer 섹션의 주요 속성#

- OnBootSec
- OnCalendar
- Unit


## Timer 파일 작성#

```vim
nvim /etc/systemd/systemd/타이머.timer


[Unit]
Description= 


[Timer]
OnBootSec=1min
OnCalendar=*-*-* *:0/10:00
Unit=서비스.service


[Install]
# 보통 timer유닛은 timers.target을 설정하고, 일반 서비스는 muti-user.target을 설정한다.
WantedBy=timers.target 
```




## 파일 작성 후 사용

```bash
# 1. 변경된 설정 파일 로드 (필수)
sudo systemctl daemon-reload
```

```bash
# 2. 타이머 활성화 (부팅 시 자동 시작) 및 즉시 시작
sudo systemctl enable --now 타이머.timer
```

```bash
# 3. 타이머 상태 확인
systemctl status 타이머.timer
```
