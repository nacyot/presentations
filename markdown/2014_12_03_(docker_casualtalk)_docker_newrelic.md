footer: Dokerizing newrelic-sysmond © nacyot 2014 -
slidenumbers: true

# [fit] Dockerizing
# [fit] newrelic-sysmond

---

# [fit] Docker Casual Talk #2
### 2014. 12. 03.
### 2015. 09. 09. update

---

![fit](http://i.imgur.com/BVz3cIx.png)

---

# ![inline 350%](http://www.smartstudy.co.kr/static/image/icon/company.png)

## Daekwon Kim
### SMARTSTUDY Software & System Engineer

---

# 예전 발표

## [fit] [도커(Docker) 메트릭스 & 로그 수집](http://www.slideshare.net/ext/docker-37592250)

---

# 모니터링(로그, 메트릭스)

* 2 (시스템, 어플리케이션) by 2 (로그, 메트릭스)
  * 1. 시스템 로그
  * 2. 시스템 메트릭스
  * 3. 어플리케이션 로그
  * 4. 어플리케이션 메트릭스
   
---

# Docker와 모니터링 전체 그림

![fit inline](http://i.imgur.com/PqPlIUf.png)

---

# Docker와 모니터링 세부 분류

![fit inline](http://i.imgur.com/GcuIoLo.png)

---

# Docker와 모니터링 세부 분류

1. 도커 호스트 시스템 로그
2. 도커 호스트 시스템 메트릭스
3. 컨테이너 어플리케이션 로그
4. 컨테이너 어플리케이션 메트릭스
5. 컨테이너 메트릭스(?)

---

# 오늘의 주제
## Docker 호스트 시스템 메트릭스

---

# Newrelic Server Monitor

* 외부 Service에 위임하기
* 쉬운 방법

---

# Agent 설치하기
  
* 패키지 관리자 지원
* 바이너리로 설치
  
---

# Agent 설치하기
  
* 패키지 관리자 지원
* 바이너리로 설치
* __Dockerize!__

---

# Why?

* 운영체제마다 설치 방법이 달라서 설치하기 귀찮음
* CoreOS 사용에 따라 호스트에서 뭔가 하기 싫음
* 모든 프로세스는 도커 위에서
* 심지어 시스템 관리도 도커 위에서 (toolbox...)
* 이미 대부분의 시스템에서 Docker 사용중

---

# 누가 이미 만들어놨음

* [johanneswuerbach/newrelic-sysmond-service](https://github.com/johanneswuerbach/newrelic-sysmond-service/blob/master/Dockerfile)
* 컨테이너 안에서
* 에이전트 다운 받고
* 에어전트 설정하고,
* 실행

---

# 잘 작동함 >_<

* CPU / Memory
* Disk
* Network
* Processes.....?

---

# Processes???

## 안 나와요

---

# 컨테이너 내부 감시

## sysmond 프로세스만 볼 수 있음

---

# 쓸모가 없다... oTL...

---

# [fit] 구세주

---

# [fit] chroot

---

# chroot!

* 컨테이너 안에 또 다른 격리 공간
* 바이너리가 있으므로 busybox를 사용
* 다행히 busybox에서도 chroot 사용 가능
* busybox 내의 주요 디렉터리 복사
* 호스트의 /proc 디렉터리를 마운트 시킴
* 이를 통해 sysmond가 processes 전체를 읽음!

---

# 아싸!

![fit](http://i.imgur.com/MWmJhHd.png?1)

---

# 아차...

![fit](http://i.imgur.com/oQsIlDc.png)

---

# CoreOS

* btrfs가 기본...(뭣이!)
* newrelic에서 지원 안 됨
* 안 나옴...

---

# [fit] [nacyot/newrelic-sysmond](https://github.com/nacyot/docker-logs/tree/master/newrelic-sysmond/busybox)

---

# docker run!

```
$ docker run -d \
    -v /proc:/chroot/proc:ro \
    -v /etc/resolv.conf:/chroot/etc/resolv.conf:ro \
    -e NEW_RELIC_LICENSE_KEY=<LICENSE_KEY> \
    -e NEW_RELIC_HOST_NAME=`hostname` \
    -e SERVICE_NAME=<SERVICENAME> \
    -h `hostname` \
    --name newrelic-sysmond \
    nacyot/newrelic-sysmond:busybox
```

---

# Thank you!

## [@nacyo_t](https://twitter.com/nacyo_t)
