footer:  Docker로 보는 서버 운영의 미래 © Daekwon Kim 2015 -
slidenumbers: true

# [fit] Docker로 보는
# [fit] 서버 운영의 미래
### The Future of System Engineering

---

## [2014 Deview](http://deview.kr/2014/session?seq=20)

### 2014. 9. 29.
### 2015. 8. 29. update

---

# ![inline 350%](http://www.smartstudy.co.kr/static/image/icon/company.png)

## Daekwon Kim
### SMARTSTUDY Software & System Engineer

---

![fit](http://i.imgur.com/BVz3cIx.png)

---

# [fit] Deployment
## [fit] 그리고 Docker

^
Docker은 애플리케이션 배포를 어떻게 바꿀 것인가

---

# TOC

1. 배포와 서버운영
1. Infrastructure as a Service (IaaS)
1. Platform as a Service (PaaS)
1. 컨테이너형 어플리케이션 가상화
1. Docker로 다시 정의하는 배포

^
배포의 정의, 클라우드, 그리고 컨테이너

---

# State (상태)

## [fit] 사물ㆍ현상이 놓여 있는 모양이나 형편

^
이야기에 들어가기에 앞서, 뒤에서 이어질 모든 이야기의 핵심

---

# 1. 배포와 서버운영

---

# 배포의 요소

![inline 200%](https://www.lucidchart.com/publicSegments/view/542438f7-a7b8-4f68-851f-44710a005489/image.png)

^
먼저 물리적인 서버에서의 애플리케이션 배포에 대해서 이야기해보죠

---

# 배포란?

## [fit] 대상 서버를 어플리케이션이 실행 가능한 상태로 만드는 일

---

# 예제

## Ruby on Rails 어플리케이션

---

# 하나의 서버

![inline 150%](https://www.lucidchart.com/publicSegments/view/54243b36-def8-4ead-a08a-471a0a009686/image.png)

---

# 배포 과정

![inline 150%](https://www.lucidchart.com/publicSegments/view/54243a6d-ed1c-422f-8a2a-476f0a005489/image.png)

---

# 배포 과정에 따른 상태 변화

![inline 150%](https://www.lucidchart.com/publicSegments/view/54243a8e-bd5c-4463-9c53-0d8b0a0099df/image.png)

---

# 더 복잡한 상황

---

# 다수의 어플리케이션

![inline 150%](https://www.lucidchart.com/publicSegments/view/54243b67-ac78-45c9-9c82-6dda0a00c16d/image.png)

---

# 새로운 어플리케이션

![inline 100%](https://www.lucidchart.com/publicSegments/view/54243baa-9f84-45a6-86a7-775c0a00c16d/image.png)

---

# 배포 과정 (정상화)

![inline 100%](https://www.lucidchart.com/publicSegments/view/54243c2d-2ab0-4b73-89dd-6aea0a008ac6/image.png)

---

# 배포

어플리케이션들이 모두 실행 가능한 상태로 만드는 일

![inline 100%](https://www.lucidchart.com/publicSegments/view/54243e15-c020-4145-bce3-68430a00c285/image.png)

---

# 서버 운영

모든 어플리케이션이 동작하는 *상태*를 유지하는 일

![inline 100%](https://www.lucidchart.com/publicSegments/view/54243c5e-b324-49a4-b122-425c0a004825/image.png)

^
하지만 실제로 서버를 운영하시는 분들은 너무나 잘 아시겠지만 이게 정말 어렵습니다.

---

# [fit]서버 운영이 어려운 이유

^
그렇다면 서버 운영은 왜 어려운가

---

# [fit] 서버 운영 = 전역적 상태 관리

^
서버 운영은 서버라는 하나의 작은 생태계가 기적적으로 균형을 갖추도록하는 일이기 때문

---

![fit](http://upload.wikimedia.org/wikipedia/commons/0/01/Card_castle6.JPG)

---

# 카드로 만든 집
   
> The system becomes a house of cards. You fear any change and you fear replacing it since you don’t know everything about how it works.
-- [Chad Fowler](http://chadfowler.com/blog/2013/06/23/immutable-deployments/)

^
시스템은 카드로 만든 집이 되어간다. 우리는 시스템 전체가 어떻게 작동하는 지 전체를 파악하지 못 하기 때문에 어떤 변화나 무언가를 교체하는 것에 대한 공포를 느끼게 될 것이다. 실제로 오랜 레거시 서버들이 이런 이유로 방치되곤 하죠

---

# 클라우드

^
그렇다면 이제 물리적인 서버를 떠나서 클라우드의 세계로 넘어가고자 합니다.

---

# [fit] 2. Infrastructure as a Service

---

# 같은 환경을 가지는 가상화된 환경

![inline 150%](https://www.lucidchart.com/publicSegments/view/54248a1c-1080-4a40-9256-115d0a00c60b/image.png)

^
가상화를 통한 스펙 통일

---

# [fit] 원하는 만큼 사용 가능한 컴퓨팅 자원

![inline 150%](https://www.lucidchart.com/publicSegments/view/54248a25-5a60-47ab-abf7-3d960a00c16d/image.png)

^
클라우드가 허용하는 한 얼마든지 서버를 띄울 수 있음. 또한 시간당 과금

---

# Disposable Component

* 서버는 물리적으로 고정된 자원
* 인스턴스는 쓰고 버리는 자원

---

# 인터넷의 발전소

> "Amazon Web Service는 인터넷의 발전소다
-- 타마카와 켄

^
발전소의 비유. 필요한 만큼 생산한다

---

# 이미지

---

# 이미지화 & 스케일 인/아웃

![inline 150%](https://www.lucidchart.com/publicSegments/view/54248b8f-0448-4450-9e1c-6a480a00c60b/image.png)

^
애플리케이션이 돌아가는 특정 상황을 이미지로 만듬. 그리고 서버를 만들고 죽이고 하는 과정을 반복적으로 적용. Disposable Component가 만들어낸 개념

---

# 오토 스케일링

![inline  150%](https://www.lucidchart.com/publicSegments/view/54248bea-f1e8-4d46-884c-5e3a0a005489/image.png)

^
서버의 스케일링을 다양한 메트릭스를 통해 자동적으로 수행

---

# 이미지 관리

---

# 이미지 수의 증가

이미지 수에 비례해서 관리가 어려워짐
(어플리케이션 수 * 시간)

![inline 150%](https://www.lucidchart.com/publicSegments/view/54248fd5-29e0-4b8f-af40-2e170a004825/image.png)

---

# 상태에 기반한 이미지

이미지는 어떤 특정 시점의 *상태*를 저장한 것 뿐

![inline 150%](https://www.lucidchart.com/publicSegments/view/54248fde-d984-4444-813c-5a6c0a008ac6/image.png)

---

# 최종적으로 남은 이미지

어떻게 만들었는지 아무도 모름 (복원 불가능)

![inline 150%](https://www.lucidchart.com/publicSegments/view/54249043-9e28-4681-9dd8-40180a00c60b/image.png)

---

# 이미지 관리

* 다양한 시점의 상태 관리
* 어떻게 하면 상태를 더 잘 관리할 수 있을까?
* 이미지 / 인스턴스 활용의 극대화

---

# [fit] Configuration Management

![inline 150%](https://www.lucidchart.com/publicSegments/view/54249182-1adc-41ab-989e-4c500a005489/image.png)

---

# 명령어를 통한 상태 변화(과거)

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424946c-2574-4877-a47c-1deb0a00c285/image.png)

---

# [fit] Cookbook을 통한 상태 변화(Chef)

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424947b-5eb8-4690-a447-5a400a008ac6/image.png)

---

# 멱등

같은 과정을 거치면 서버는 똑같은 상태가 된다

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424956d-2470-4d73-9185-3f700a00c60b/image.png)

---

# Infrastructure의 코드화

![inline 150%](https://www.lucidchart.com/publicSegments/view/54249474-467c-44c4-865f-656a0a0099df/image.png)

---

# Apache Cookbook 예제

**CMD**

```
$ apt-get install apache2
```

**Chef Cookbook**

```
package 'httpd'

service 'httpd' do
  action [:start, :enable]
end
```

---

# [fit] Configuration Management 효과 (1)

* 초기 적용이 어려움
  * 학습 비용
  * 많은 시행착오가 필요
  * 작업 속도가 느림

---

# [fit] Configuration Management 효과 (2)

* 서버 운영를 단순화
  * 서버의 상태를 코드로 관리
  * 어떤 상태를 재현 가능하게 만들어줌
  * 다수의 서버를 운용중에 특정 상태로 변화시킬 수 있음

---

# [fit] Configuration Management

## <br><br>상태를 관리하는 도구

---

# [fit] 3. Platform as a Service

---

# PaaS

자유도는 낮지만, 좀 더 편리한?

![inline 100%](https://www.lucidchart.com/publicSegments/view/542497f9-f0c0-4b65-b4e0-4ce50a005489/image.png)

---

![inline 100%](http://i.imgur.com/LoETW9Bl.jpg)

---

# 배포의 요소(과거)

![inline 150%](https://www.lucidchart.com/publicSegments/view/542438f7-a7b8-4f68-851f-44710a005489/image.png)

---

# 배포의 요소(PaaS)

![inline 150%](http://i.imgur.com/AZDqy43.png)

---

# 어플리케이션 배포 단위

배포 환경은 Heroku가 제공

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424a466-25b4-47ea-a28c-6a250a0099df/image.png)

---

# [fit] 어플리케이션과 배포 단위의 1:1 매치

어플리케이션 별 독립된 배포 환경 제공

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424a4f8-1ee0-4e57-8fcd-1e490a00c285/image.png)

---

# Scale In / Out 기본 지원

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424a587-b92c-4ce0-9b0c-32bf0a004825/image.png)

---

# 어플리케이션 업데이트

---

# 기존의 어플리케이션 업데이트

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424a761-4218-4697-b575-474f0a004d3d/image.png)

---

# 기존의 어플리케이션 롤백

![inline 150%](https://www.lucidchart.com/publicSegments/view/54275c07-0b20-4901-ad46-58f40a008ac6/image.png)

---

# [fit] Heroku에서의 어플리케이션 업데이트

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424a76a-1e78-4fbe-b008-3cd70a005489/image.png)

---

# Heroku에서의 롤백

```
$ heroku releases
Rel   Change                          By                    When
----  ----------------------          ----------            ----------
v52   Config add AWS_S3_KEY           jim@example.com       5 minutes ago
v51   Deploy de63889                  stephan@example.com   7 minutes ago
v50   Deploy 7c35f77                  stephan@example.com   3 hours ago
v49   Rollback to v46                 joe@example.com       2010-09-12 15:32:17 -0700
...

$ heroku rollback v40
```

---

# 배포의 단순화

![inline 150%](https://www.lucidchart.com/publicSegments/view/542761a7-b914-4aa6-9d6e-34f60a00c0e0/image.png)

---

# 확장의 단순화

![inline 110%](https://www.lucidchart.com/publicSegments/view/542761b1-d760-477d-a098-251f0a008ac6/image.png)

---

# [fit] PaaS를 사용하지 않는 이유

---

# 비용

![](http://i.imgur.com/RQdJBow.jpg)

---

# PaaS스럽지 않은 어플리케이션

![inline 150%](https://www.lucidchart.com/publicSegments/view/5424a9f7-9344-493f-85b6-1da10a00c285/image.png)

---

# PaaS != IaaS

* IaaS에 비해서 큰 학습 비용
* 원격 접속 시스템이 없거나 제한
* 파일 시스템 이용에 제한
* Site 패키지 설치 제한
* 로그 수집 제한적 허용 (STDOUT)

---

# [fit] 문제를 해결하는 법이 다름

---

# 파일 시스템
    
* 외부 Storage 서비스를 사용

---

# 애드온 (외부 서비스)

![inline fit](http://i.imgur.com/mRZkKYC.png)

---

# [fit] 4. 컨테이너형 어플리케이션 가상화

---

# PaaS의 단점?

* 원격 접속 시스템이 없거나 제한
* 파일 시스템 이용에 제한
* Site 패키지 설치 제한
* 로그 수집 제한적 허용 (STDOUT)

---

# 상태 변화에 의존한 작업

![inline 150%](https://www.lucidchart.com/publicSegments/view/54250096-9de8-4f49-8fe9-4f5f0a004d3d/image.png)

---

# Immutable(Stateless)

![inline 150%](https://www.lucidchart.com/publicSegments/view/54250072-877c-4e50-a113-05780a00c285/image.png)

---

# [fit] 뒤집어보면 컨테이너형 가상화의 특징

---

# Heroku Dyno
   
## LinuX Container (LXC)
## Chroot on steroid

---

# Chroot (Change Root)

* pivot root 기능
* 파일, 라이브러리는 직접 준비
* 사용이 까다로움
* 프로세스 격리의 초기 버전?

---

# LinuX Container

* Kernel Namespaces
* Apparmor and SELinux profiles
* Seccomp policies
* *Chroots (using `pivot_root`)*
* Kernel capabilities
* Control groups (cgroups)

---

# 예제 1) 가상 머신?

![inline](http://i.imgur.com/3WEL6pD.png)

---

# 호스트 커널 공유

![inline 120%](https://www.lucidchart.com/publicSegments/view/542625e3-5d14-4b45-8622-17210a00c285/image.png)

---

# 프로세스 실행 환경 분리

![inline 150%](https://www.lucidchart.com/publicSegments/view/5427569d-bfd0-45e9-844c-5a050a0090b1/image.png)

---

# 예제 2) 프로세스 격리

격리된 환경에서 특정 프로세스만 실행

```
$ cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=14.04

$ lxc-create -t centos -n centos
$ lxc-start -n centos -- cat /etc/redhat-release
CentOS release 6.5 (Final)
```

---

# Linux Container

격리된 환경, 즉 내부적인 의미의 컨테이너에 집중

![inline fit](http://i.imgur.com/2UJce1Il.jpg)

---

![inline 100%](http://i.imgur.com/wSwaXbE.png)

---

# Docker

![inline 100%](http://i.imgur.com/QIo2ZI8.png)

---

# [fit] Linux Container의 확장 도구

---

# [fit] Docker Container ≈ Heroku Dyno

---

# [fit] Docker는 LXC의 Wrapper?

---

# Docker 구조

![inline 120%](https://www.lucidchart.com/publicSegments/view/53db7b95-4114-4fc0-ae13-6d9f0a00d812/image.png)

---

# Docker의 발전

* 0.7.0 (2013-11-25)
  * Device Mapper 지원
* 0.8.0 (2014-02-04)
  * BTRFS 지원
  * MacOSX 공식 지원(boot2docker)
* 0.9.0 (2014-03-10)
  * LibContainer 도입(기본 드라이버)
* 1.0.0 (2014-06-09)
  * Docker Hub
  * 안정화(문서에서 경고 문구 사라짐)

---

# 현재의 Docker

![inline fit](http://i.imgur.com/O3hOnB9.png)

---

# Docker 지원 시스템 (범용성)

Ubuntu, Red Hat Enterprise Linux, Oracle Linux, CentOS, Debian, Gentoo, Google Cloud Platform, Rackspace Cloud, Amazon EC2, IBM Softlayer, Arch Linux, Fedora, openSUSE, CRUX Linux, Microsoft Windows, Mac OS X

---

# 도커의 차별성

## 이미지(Image)

---

# [fit]이미지 기반의 어플리케이션 가상화

![inline 150%](https://www.lucidchart.com/publicSegments/view/5427b371-9fdc-400e-943a-2c1b0a0048fd/image.png)

---

# [fit] 이미지 만들기 (Build)

---

# [fit] Read Only & Writable layer

![inline 150%](https://www.lucidchart.com/publicSegments/view/5425532a-e154-4c09-a2d6-3cfd0a008ac6/image.png)

---

# rootfs / Base Image

![inline 150%](https://www.lucidchart.com/publicSegments/view/54255311-7998-4017-aa92-591d0a0099df/image.png)

---

# 상태 변화

![inline 150%](https://www.lucidchart.com/publicSegments/view/54255322-d974-45e8-979e-6ee80a004d3d/image.png)

---

# Git 설치하기

```
$ docker run -it ubuntu:latest --name git /bin/bash

root@2f8bfff679f9:/# git
bash: git: command not found
root@2f8bfff679f9:/# apt-get update &> /dev/null
root@2f8bfff679f9:/# apt-get install -y git &> /deev/null

root@2f8bfff679f9:/# git --version
git version 1.9.1
```

---

# Git 설치 후 상태 변화

Diff를 통해서 Base Image와 컨테이너의 차이를 파악

```
$ docker diff git | grep git | head -n 10
(standard input):56:A /var/lib/dpkg/info/git.list
(standard input):78:A /var/lib/dpkg/info/git.conffiles
(standard input):98:A /var/lib/dpkg/info/git.postrm
(standard input):109:A /var/lib/dpkg/info/git.prerm
(standard input):116:A /var/lib/dpkg/info/git.postinst
(standard input):125:A /var/lib/dpkg/info/git-man.list
(standard input):184:A /var/lib/dpkg/info/git-man.md5sums
(standard input):200:A /var/lib/dpkg/info/git.preinst
(standard input):202:A /var/lib/dpkg/info/git.md5sums
(standard input):257:A /var/lib/git
```

---

# Commit으로 새로운 이미지 생성

```
$ docker images | grep ubuntu
ubuntu  |  14.04   |  826544226fdc  |  3 weeks ago  |  194.2 MB
ubuntu  |  latest  |  826544226fdc  |  3 weeks ago  |  194.2 MB

$ docker commit git ubuntu:git
f98472c1d8aa3329d354c642b19ee45468297faa08487b3cd950d34247b5f211

$ docker images | grep ubuntu
ubuntu  |  git     |  f98472c1d8aa  |  6 seconds ago  |  252.2 MB
ubuntu  |  14.04   |  826544226fdc  |  3 weeks ago    |  194.2 MB
ubuntu  |  latest  |  826544226fdc  |  3 weeks ago    |  194.2 MB
```

---

# 새로운 상태를 이미지로 저장

![inline 150%](https://www.lucidchart.com/publicSegments/view/54255a4d-88f4-4b12-902a-201c0a004d3d/image.png)

---

# Dockerfile

## [fit] 이미지 생성 과정을 기술한 Docker 전용 DSL

---

# Dockerfile 예제

```
FROM nacyot/ruby-ruby:latest

RUN apt-get update
RUN apt-get install -qq -y libsqlite3-dev nodejs
RUN gem install foreman compass

WORKDIR /app
RUN git clone https://github.com/nacyot/docker-sample-project.git /app
RUN git checkout v0.1
RUN bundle install --without development test

ENV SECRET_KEY_BASE hellodocker
ENV RAILS_ENV production
EXPOSE 3000
CMD foreman start -f Procfile
```

---

# [fit] Dockerfile을 통한 이미지 빌드 (1)

![inline fit](https://www.lucidchart.com/publicSegments/view/542561e1-6418-42e7-a233-55a20a004d3d/image.png)

---

# [fit] Dockerfile을 통한 이미지 빌드 (2)

![inline fit](https://www.lucidchart.com/publicSegments/view/542561ef-5530-420b-aa8f-3cba0a008ac6/image.png)

---

# 빌드된 이미지

호스트의 환경과 무관하게 실행 가능

![inline 150%](https://www.lucidchart.com/publicSegments/view/5427b724-a4e0-45e0-9406-131b0a004d3d/image.png)

---

# [fit] 이미 어플리케이션이 실행 가능한 상태?

# [fit] <br>배포 완료?!

---

# [fit] Docker를 활용한
# [fit] 오픈소스 배포 문화

---

# StriderCD

Node.js 웹 어플리케이션

```
$ docker run -it -p 3000:3000 niallo/strider
```

---

# IHaskell

파이썬, Haskell, Zeromq 기반 유틸리티 / 웹UI

```
$ docker run -it gregweber/ihaskell console
```

---

# Docker Hub

```
$ docker info
Containers: 30
Images: 342
...
Username: nacyot
Registry: [https://index.docker.io/v1/]
```

---

# Docker Private Registry

파이썬 웹 어플리케이션

```
$ docker run -it -p 5000:5000 registry
```

---

# Build once, Run anywhere

![inline fit](http://i.imgur.com/vtn8aRE.png)

---

# 표준화된 이미지

* 이미지 생성 / 공유 기능
* 공식 Registry 서비스 지원
* Private Registry 어플리케이션

---

# 컨테이너와 Docker 

## [fit] 표준화된 컨테이너의 이동성에 집중

![](http://i.imgur.com/B9jKH7y.jpg)

---

# LXC vs Docker

## [fit] LXC == 프로세스 격리를 위한 도구
## [fit] Docker == 컨테이너 수송을 위한 도구

---

# Docker의 핵심

## IaaS의 자유
## PaaS의 단순함

---

# [fit] 5. Docker로 다시 정의하는 배포

---

# 배포 단위

![inline 150%](https://www.lucidchart.com/publicSegments/view/5427bd60-d024-4160-a907-0cb10a0048fd/image.png)

---

# Docker 이미지
   
![inline 150%](https://www.lucidchart.com/publicSegments/view/5427be44-e9d8-4a1c-8a7c-2d590a005489/image.png)

---

# 배포 대상

![inline 150%](https://www.lucidchart.com/publicSegments/view/5427be4c-3fb8-401d-b806-39ca0a00c60b/image.png)

---

# 기존 배포와 서버운영

![inline fit](https://www.lucidchart.com/publicSegments/view/54243c5e-b324-49a4-b122-425c0a004825/image.png)
   
---

# 배포와 서버 운영의 새로운 정의

![inline fit](https://www.lucidchart.com/publicSegments/view/5427c43e-056c-4303-a308-6f280a00c60b/image.png)

---

# 어플리케이션 업데이트

![inline fit](https://www.lucidchart.com/publicSegments/view/5427c7d1-ead4-475a-a355-73710a005489/image.png)

---

# 롤백

![inline fit](https://www.lucidchart.com/publicSegments/view/5427c7d8-11e0-4d8b-907b-57db0a008ac6/image.png)

---

# 역할의 변화

---

# 프로그래머의 역할

![inline fit](https://www.lucidchart.com/publicSegments/view/5427c447-50f4-4be6-ab0a-01f60a004d3d/image.png)

---

# 서버관리자의 역할

![inline fit](https://www.lucidchart.com/publicSegments/view/5427c134-02e8-473d-92aa-12840a005489/image.png)

---

# [fit] Immutable
# [fit] Infrastructure

---

# 미래

---

# CoreOS

클러스터링 가능한 도커 전용 OS

![inline fit](http://i.imgur.com/jYiSO3l.png)

---

# 물류 시스템

![inline 150%](https://www.lucidchart.com/publicSegments/view/54259720-b944-4776-a5d5-28330a00c60b/image.png)
     
---

# 서버의 정의

> Docker로 모든 어플리케이션을 컨테이너로 만든다면 서버는 Docker를 돌리기 위해 존재할 뿐.
-- subicura

---

# 클라우드스러움

## Disposable Component
## Immutable Infrastructure

---


# [fit] The Future is Immutable.
### <br> [Mitchell Hashimoto](http://www.slideshare.net/profyclub_ru/8-mitchell-hashimoto-hashicorp)

---

# Thank you!

## [@nacyo_t](https://twitter.com/nacyo_t)
