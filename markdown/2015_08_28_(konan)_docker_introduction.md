footer:  Docker Introduction © Daekwon Kim 2015 -
slidenumbers: true

# [fit] Container
# [fit] 가상화 입문

^
오늘의 주제 : 컨테이너 가상화
왜 Docker가 아니라 Contaienr인가
Docker는 컨테이너 가상화 기술의 하나
중점 : 도구적인 면뿐만이 아니라 이게 왜 필요한가

---

# ![inline 350%](http://www.smartstudy.co.kr/static/image/icon/company.png)

## 김대권 (nacyot)
### Software & System Engineer

^
스마트스터디 프로그래머
부족하지만 인프라 환경 개선을 위해 노력중

---

# TOC

* Docker 입문
* Immutable Infrasture

---

# [fit] 시대는 바야흐로 가상화

![fit](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/Weather-overcast.svg/2000px-Weather-overcast.svg.png)

^
다들 아시겠지만,

---

# 하드웨어 가상화

## [fit] 소프트웨어로 구현된 가상의 하드웨어

^
일반적으로 가상화를 이야기할 때 가상화의 정의

---

# [fit] 물리적 하드웨어 위의
# [fit] 소프트웨어로 구현된 하드웨어

^
물리적 하드웨어 위에 소프트웨어로 하드웨어를 구현하고 그 위에 운영체제를 올리고...

---

# VirtualBox [^1]

# Parallels [^2] 

# VMWare [^3] 

[^1]: [https://www.virtualbox.org/](https://www.virtualbox.org/)

[^2]: [http://www.parallels.com/products/desktop/](http://www.parallels.com/products/desktop/)

[^3]: [http://www.vmware.com/](http://www.vmware.com/)

---

# 이미 일상적인 기술

^
굳이 기업용 가상화 기술을 이야기하지 않더라도 개인에게도 이미 친숙한 기술

---

# 인프라스트럭처

## 하드웨어 파편화 최소화
## 서버 없는 사무실
## 거의 무한한 확장성

^
가상화(클라우드)를 통해서 변화고 있는 부분들. 가상화된 하드웨어이기 때문에 파편화가 거의 없고, 서버를 사무실에 둘 필요가 없으며, AWS를 사용한다면 아마존이 감당할 수 있는 만큼은 확장 가능

---

# [fit] 그리고 새로이 ~~등장한~~ 재발견된

^
이러한 가상화를 전제로 다시 주목받는 기술

---

# [fit] Container?

---

# [fit] Container 가상화의 대표주자
# [fit] <br/><br/>Docker[^4]

![](http://i.imgur.com/GEcrPFc.jpg)

^ Container 가상화를 구현하는 대표적인 도구

[^4]: [https://www.docker.com/](https://www.docker.com/)

---

# [fit] Hello, Docker
## 간단한 예제로 시작하기

---

# Ghost 블로그[^5]

## ex) [리모티 블로그](http://blog.remotty.com/blog/)

[^5]: [http://ghost.org/](http://ghost.org/)

^
새로운 오픈소스 블로그 플랫폼. 고스트로 만든 리모티 블로그 소개하기. 서비스도 있지만 오픈소스로 공개되어 있으며 직접 설치해서 사용하는 것도 가능

---

# 고스트 설치하기

1. node 설치하기
1. ghost 소스코드 다운로드
1. 데이터베이스 셋업
1. 관련 환경설정
1. 서버 설정하기
1. 프로덕션 서버에 배포

^
간략히 적은 프로세스. 얼핏 간단해보이지만, 프로그래밍 / 인프라에 대한 상당한 지식 요구할 뿐만 아니라, 고스트 버전이나 의존성 문제로 생각처럼 설치가 되지 않을 수도 있음

---

# Docker로 실행하기

```
$ docker pull ghost

$ docker images | grep ghost
ghost latest 85c3e5ecdf68 2 days ago 231.3 MB

$ docker run --name ghost -p 8080:2368 -d ghost
b81b2a20c09f0e973e6
```

^
그럼 Docker를 사용하면 어떻게 될까요. Docker에서는 Ghost를 미리 설치해둔 이미지를 준비해서 그 이미지를 실행하면 바로 고스트가 실행됩니다.

---

# [fit] DEMO
# [fit] Ghost Blog

![](http://i.imgur.com/JPTARDS.png)

^
앞의 예제를 실제로 실행해서 보여드리도록 하겠습니다. CMD 이동 명령이 실행

---

# [fit] 프로세스가 실행되는 두 가지 환경

1. Docker Server가 실행되는 컴퓨터의 환경
2. ghost가 설치된 Docker 이미지의 환경

^
여기서 중요한 점을 하나 짚고 넘어갈 필요가 있습니다. 어떻게 설치하지도 않은 프로그램이 내 컴퓨터에서 구동이 될 수 있는 걸까요? 저는 지금 Docker Daemon을 boot2docker를 이용해서 Virtual Machine 상에서 실행하고 있습니다. 여기에는 Ghost가 설치되어있지 않습니다. 즉, Docker를 사용할 때는 Ghost를 설치한 게 아니라, Ghost가 설치된 환경을 가진 이미지를 준비했다는 게 중요합니다. 좀 더 자세히 살펴보겠습니다.

---

# [fit] Docker가 실행되는 환경

```
$ docker version
Client version: 1.7.1
Client API version: 1.19
Go version (client): go1.4.2
Git commit (client): 786b29d
OS/Arch (client): linux/amd64
...

$ which node
-sh: node: not found
```

^
도커가 설치되어있는 환경에서 node를 찾아보면, not found 즉 설치되어있지 않다는 것을 확인할 수 있스니다.

---

# [fit] xaos가 설치된 Docker 이미지의 환경

```
$ # docker server 환경
$ docker run --rm -it ghost bash

ShellInDockerContainer$ # 컨테이너 환경
ShellInDockerContainer$ which node
/usr/local/bin/node

ShellInDockerContainer$ npm list | grep ghost
ghost@0.6.4 /usr/src/ghost
```

^
그렇다면 도커 이미지 안에 들어가보도록 하겠습니다. 앞서 Ghost를 실행한 이미지 환경 안에서 직접 bash를 실행시켜서 그 안에 무엇이 있는지 확인해볼 수 있습니다. 이 안으로 들어와서 which 명령어를 실행해보면, /usr/local/bin/ 아래에 node가 설치된 것을 알 수 있습니다. 그리고 npm list를 통해서 ghost가 설치되어있는 것도 확인할 수 있습니다.

---

# [fit] 소프트웨어 패키지가 아니라
# [fit] 설치된 환경 자체

^
여기서 알 수 있는 점은 Docker의 이미지는 소프트웨어 패키지가 아니라는 점입니다. 소프트웨어 패키지를 포함한 모든 환경이 같이 저장되어있습니다. 이는 일견 하드웨어 가상화와 비슷해보이기도 합니다.

---

# [fit] 하드웨어 가상화 없는
# [fit] 격리된 환경의 프로세스

^
하지만 컨테이너 가상화 기술의 핵심은 하드웨어 가상화 없이 "고유한 환경"을 가진 이미지들을 만들고 언제든지 재실행할 수 있다는 점입니다. 그래서 컨테이너에서 실행하는 것은 운영체제가 아니라, 하나의 프로세스가 되는 것입니다.

---

# [fit] Container!

^
이게 바로 컨테이너입니다.

---

# 그래서 대단한 거야?

^
컨테이너 가상화 기술을 모르던 사람이 이걸 보고 느끼는 감정은 두 가지 중 하나라고 생각합니다. 하나는 굉장히 충격을 받거나, 그래서 대단한 건지 잘 와닿지 않는 경우죠.

---

# The
# Future
# of
# Everything

![right](http://i.imgur.com/qcNrkiA.png)

[Link](http://www.slideshare.net/MichaelDucy/the-future-of-everything-37344357)

---

### docker

---

## docker

---

# docker

---

# [fit] docker

---

# 

![140%](https://upload.namu.wiki/upload/%EA%B7%B8%EB%9F%B0%EB%8D%B0%20%EA%B7%B8%EA%B2%83%EC%9D%B4%20%EC%8B%A4%EC%A0%9C%EB%A1%9C%20%EC%9D%BC%EC%96%B4%EB%82%AC%EC%8A%B5%EB%8B%88%EB%8B%A4%2FitDidHappen.png)

^
저는 이제 이런 상황을 Docker를 사용하는 입장에서 굉장히 흥미롭게 바라보고있습니다. Docker가 처음 나왔던 게 2013년 중반, 제가 처음 사용해본 게 2013년 말이었는데, 그 때랑은 비교할 수 없을 만큼 많이 사용되고 있고, 컨테이너 가상화 기술의 표준처럼 자리잡았죠.

---

# [fit] 실전으로 배우는
# [fit] Dokcer 

^
앞에서는 이미지를 실행하는 법을 간단히 살펴보았다면, 여기서보터는 실제로 Docker 이미지를 만드는 법에 대해서 알아보겠습니다.

---

# 이미지

## 프로세스를 실행하기 위해
## 미리 준비된 환경

^
사실은 굉장히 번거로운 개념입니다. 왜냐하면 하나의 프로세스를 실행하기 위해서 하나의 환경을 만든다? 사실 이러한 방식의 접근을 사용해보지 않은 사람들에게는 굉장히 거추장스럽고, 중복이 많은 방식으로 보일 수도 있어요. 근데 어쨌건 컨테이너 가상화에서는 하나의 프로세스만을 위해서, 하나의 환경을 준비합니다.

---

# 컨테이너

## 이미지 환경에서
## 실행된 프로세스

^
프로세스, 프로세스, 프로세스. 도커는 컨테이너를 실행시키기 위한 도구이며, 컨테이너 = 프로세스

---

# 원시적인 컨테이너

---

# chroot

## 프로세스의 root를 속이자

^
원래 프로세스는 모든 파일과 의존성(라이브러리)를 루트를 기준으로 찾음. 그런데 chroot 특정 디렉터리를 루트라고 인식하도록 변경시켜줌. 이를 통해서 실행된 프로세스는 모든 파일과 의존성을 지정된 디렉터리로부터 찾게됨.

---

# [fit] Container = chroot + @

^
이 알파에는 네트워크 가상화 계층화된 파일 시스템 자원 관리 

---

# Docker

## 이미지 관리 인터페이스
## 컨테이너 관리 인터페이스
## 계층화된 파일 시스템

^
Docker는 새로운 컨테이너 가상화를 제안한 도구라기보다, 이러한 것들을 잘 정리해서 만든 도구. 인터페이스의 승리. 계층화된 파일 시스템의 효율성.

---

# [fit] Docker 설치

---

# Docker 설치

* 리눅스

```
$ curl -sSL https://get.docker.com/ | sh
```

* 윈도/OSX : [boot2docker](http://boot2docker.io/)로 설치

---

# boot2docker

## [http://boot2docker.io/](http://boot2docker.io/)

---

# boot2docker (1)

* Docker는 리눅스 커널만 지원
* 윈도/OSX에서는 Docker를 지원하지 않음
* 따라서 리눅스 가상 머신이 필요
* boot2dokcer = CoreLinux on VirtualBox

---

# boot2docker (2)

* 가상머신을 쓰면서까지 Docker를 써야하나?
  * 성능 면에서는 분명히 불리함
  * 이미지/컨테이너 개념은 여전히 강력함
  * 실배포에서는 클라우드에서 리눅스 머신을 사용

---

# [fit] Docker 원리 이해하기

![inline](http://i.imgur.com/TMjnMyU.png)

[from](https://docs.docker.com/installation/mac/)

^
Docker의 Daemon과 Client 구조

---

# [fit] boot2dokcer 원리 이해하기

![inline](http://i.imgur.com/VOMf8R0.png)

[from](https://docs.docker.com/installation/mac/)

^
Docker이 Daemon은 원격의 Client에서도 실행가능. 로컬의 가상 머신은 물론 외부의 서버에 대해서도 가능하다.

---

# boot2docker 설치

1. 먼저 [boot2docker](http://boot2docker.io/) 에서 OS별 인스톨러 다운로드
2. 인스톨러로 설치
  * docker와 boot2docker 명령어가 설치
3. 터미널에서 `boot2docker init` 실행
  * CoreLinux 가상머신 생성
4. `boot2docker up` 실행
5. `eval $(boot2docker shellinit)` 실행

---

# [fit] `eval $(boot2docker shellinit)`

* `docker` 명령어로 가상머신의 데몬을 사용하도록 지정
  * `docker` = Docker Client
  * `가상머신의 Docker 데몬` = Docker Server
  * 명령을 내리면 실제론 가상머신에서 실행
* 터미널을 새로 열 때마다 실행해야함
* `~/.bashrc` 파일을 열어 맨 뒤에 추가
  * `eval $(boot2docker shellinit)`

---

# [fit] Docker GUI 인터페이스
# [fit] [Kitematic](https://kitematic.com/)
#### 이런 것도 있어요

![](http://i.imgur.com/ihUMmmE.png)

^
CLI와는 도저히 친해질 수 없다면...

---

# [fit] 준비 완료!

---

# 이미지를 만들어보자!

## 새로운 환경 정의하기

---

# [fit] wget이 설치된 Ubuntu 이미지

---

# `docker pull`

이미지를 받아오는 명령어

```
$ docker pull <IMAGE_NAME>
```

```
$ docker pull ubuntu:14.04
```

---

# `docker images`

도커에서 사용가능한 이미지 목록

```
$ docker images
REPOSITORY   TAG     IMAGE ID       ...
ubuntu       14.04   d2a0ecffe6fa   ...
```

---

# `docker run`

이미지로부터 컨테이너 실행하기

```
$ docker run -it <IMAGE_NAME> <COMMAND>
```

```
# ubuntu:14.04 이미지에서 bash 명령어를 실행
$ # <- 여기는 호스트의 셸
$ docker run -it ubuntu:14.04 bash
root@8b7290edaa5c:/$ # <- 새로운 환경 안의 셸
```

---

# Conatiner ID

# 8b7290edaa5c

---

# `docker ps`

실행중인 컨테이너 목록

```
# 호스트의 다른 셸에서 실행
$ docker ps
CONTAINER ID   IMAGE          COMMAND   ...
8b7290edaa5c   ubuntu:14.04   "bash"    ...
```

---

# 컨테이너에서 wget 설치하기

```
root@8b7290edaa5c:/# wget
bash: wget: command not found

root@8b7290edaa5c:/# apt-get update
root@8b7290edaa5c:/# apt-get install -y wget

root@8b7290edaa5c:/# wget
wget: missing URL
Usage: wget [OPTION]... [URL]...

Try `wget --help' for more options.
```

---

# `docker diff`

실행한 이미지로부터 현재 컨테이너의 변경사항 출력

```
$ docker diff <CONTAINER_ID>

# 호스트의 다른 셸에서 실행
$ docker diff 8b7290edaa5c
A /.wh..wh.plnk/101.138481 # 파일 추가
A /.wh..wh.plnk/361.138462 # 파일 추가
C /etc                     # 변경 사항
A /etc/ca-certificates     # 파일 추가
...
```
---

# `docker commit`

실행한 이미지로부터 현재 컨테이너의 변경사항 저장

```
$ docker commit <CONTAINER_ID> <IMAGE_NAME>
```

```
$ docker commit 8b7290 nacyot/wget:latest
9ea5dab42924a2a7cbb4a...
# 새로 생성된 이미지 ID

$ docker images
REPOSITORY   TAG     IMAGE ID       ...
ubuntu       14.04   d2a0ecffe6fa   ...
nacyot/wget  latest  9ea5dab42924   ...
```

---

# nacyot/wget 실행해보기


```
$ docker run -it ubuntu:14.04 bash
root@c30e6fa29017:/# wget
bash: wget: command not found
```

```
$ docker run -it nacyot/wget bash
root@f87cd323f346:/# wget
wget: missing URL
Usage: wget [OPTION]... [URL]...

Try `wget --help' for more options.
```

---

# Dockerfile

이미지 빌드 과정을 파일로 기술

```
FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y wget
```

---

# `docker build`

Dockerfile로 이미지 빌드하기

```
$ docker build -t <IMAGE_NAME> <TARGET_DIR>
```

```
$ ls
Dockerfile

$ dokcer build -t nacyot/wget:latest .
```

---

# Demo

---

# 더 공부하기

## [fit] [도커(Docker) 튜토리얼 : 깐 김에 배포까지](http://blog.nacyot.com/articles/2014-01-27-easy-deploy-with-docker/)

^ 도구로서의 도커는 아주 작은 부분. 작년에 쓴 튜토리얼.

---

# [fit] 컨테이너가 필요한 이유

^ `apt-get wget` 대신 왜 이런 귀찮은 짓을 할까?

---

# [fit] 보편적 물리법칙

# <br/><br/>언제 어디서나

---

# [fit] 컴퓨터의 환경은
# [fit] 보편적이지 않다

---

# 특수한 환경

## 특정 하드웨어
## 특정 OS
## 특정 시점의 시스템 설정
## 설치된 소프트웨어들

^ 어떤 수준에서건 문제가 발생할 수 있음. 어제 되는 건 오늘 되지 않는다

---

# [fit] 컴퓨터를 수리하는
# [fit] 가장 일반적인 알고리즘

---

# 재부팅

## 그래도 안 되면...

---

# 재설치

## 그래도 안 되면...

---

# OS 재설치

## 윈도우 다시 깔아.

---

# [fit] 상태 관리는 원래 어렵다
# [fit] 서버도 어렵다
# [fit] 데스크탑도 똑같이 어렵다

---

# 깨끗한 환경

^ 왜 이런 짓을 하는 걸까. 모든 것은 환경을 초기화하기 위해서. 좀 더 깨끗한(?) 환경에서 실행할 때 프로세스가 정상적으로 실행될 확률(?)이 올라간다.

---

# Dockerfile이란

## <br/><br/>깨끗한 환경으로부터
## [fit] 애플리케이션 실행 환경까지 최단경로

---

# [fit] 이미지 = 작동되는 상태

---

# 10명의 맥북

## 10개의 서로 다른 환경

---

# 하나의 이미지

## 항상 같은 환경

---

# [fit] Docker is

---

### Docker is
# 뽕 맞은 chroot

---

### Docker is
# 초강력한 포터블 앱

---

# 재현성

## 이미지로 만들면 공유가능
## 여기서 되면, 저기서도 됨

---

# [Docker hub](http://hub.docker.com/)

* 도커 공식 이미지 공유를 위한 서비스
* 다양한 이미지가 미리 준비되어 있음
  * 기본 운영체제 : Ubuntu, CentOS, ...
  * CMS: Wordpress, Ghost, drupal, ...
  * Ipython, Jira, Gitlab, Deepdream, ...
* `docker run` 명령어 하나면 실행 가능

---

# Wordpress
### 난이도: 중

^ 너무나도 유명한 CMS.

---

# Wordpress on Docker

```
$ docker run --name wp-mysql -e MYSQL_ROOT_PASSWORD=password -d mysql
$ docker run --link wp-mysql:mysql -p 8000:80 -d wordpress
```

---

# [fit] http://192.168.59.103:8000

![fit](http://i.imgur.com/23tu7Vd.png)

---

# Deepdream

![](http://i.imgur.com/y6gXyPS.png)

### [from](http://googleresearch.blogspot.ch/2015/06/inceptionism-going-deeper-into-neural.html)
### <br><br><br>난이도: 상

---

# Deepdream

* Deep Learning을 통해 컴퓨터의 눈으로 보는 세계
* Deep Learning 프레임워크 caffe를 사용

---

# [fit] 나도 한 번 해보자
# [fit] Deepdream

---

# [fit] 그럼 먼저 caffe를 설치해ㅂ.....

---

# [OS X Installation](http://caffe.berkeleyvision.org/install_osx.html)

![](http://www.kernelops.com/wp-content/uploads/2014/05/Screen-Shot-2014-05-06-at-9.59.03-AM.png)

```
We highly recommend using the Homebrew package manager. Ideally you could start from a clean /usr/local to avoid conflicts. In the following, we assume that you’re using Anaconda Python and Homebrew.

CUDA: Install via the NVIDIA package that includes both CUDA and the bundled driver. CUDA 7 is strongly suggested. Older CUDA require libstdc++ while clang++ is the default compiler and libc++ the default standard library on OS X 10.9+. This disagreement makes it necessary to change the compilation settings for each of the dependencies. This is prone to error.

Library Path: We find that everything compiles successfully if $LD_LIBRARY_PATH is not set at all, and $DYLD_FALLBACK_LIBRARY_PATH is set to provide CUDA, Python, and other relevant libraries (e.g. /usr/local/cuda/lib:$HOME/anaconda/lib:/usr/local/lib:/usr/lib). In other ENV settings, things may not work as expected.

General dependencies

brew install -vd snappy leveldb gflags glog szip lmdb
# need the homebrew science source for OpenCV and hdf5
brew tap homebrew/science
brew install hdf5 opencv

If using Anaconda Python, a modification to the OpenCV formula might be needed Do brew edit opencv and change the lines that look like the two lines below to exactly the two lines below.

  -DPYTHON_LIBRARY=#{py_prefix}/lib/libpython2.7.dylib
  -DPYTHON_INCLUDE_DIR=#{py_prefix}/include/python2.7

If using Anaconda Python, HDF5 is bundled and the hdf5 formula can be skipped.

Remaining dependencies, with / without Python

# with Python pycaffe needs dependencies built from source
brew install --build-from-source --with-python -vd protobuf
brew install --build-from-source -vd boost boost-python
# without Python the usual installation suffices
brew install protobuf boost

BLAS: already installed as the Accelerate / vecLib Framework. OpenBLAS and MKL are alternatives for faster CPU computation.

Python (optional): Anaconda is the preferred Python. If you decide against it, please use Homebrew. Check that Caffe and dependencies are linking against the same, desired Python.

Continue with compilation.
libstdc++ installation

This route is not for the faint of heart. For OS X 10.10 and 10.9 you should install CUDA 7 and follow the instructions above. If that is not an option, take a deep breath and carry on.

In OS X 10.9+, clang++ is the default C++ compiler and uses libc++ as the standard library. However, NVIDIA CUDA (even version 6.0) currently links only with libstdc++. This makes it necessary to change the compilation settings for each of the dependencies.

We do this by modifying the Homebrew formulae before installing any packages. Make sure that Homebrew doesn’t install any software dependencies in the background; all packages must be linked to libstdc++.

The prerequisite Homebrew formulae are

boost snappy leveldb protobuf gflags glog szip lmdb homebrew/science/opencv

For each of these formulas, brew edit FORMULA, and add the ENV definitions as shown:

  def install
      # ADD THE FOLLOWING:
      ENV.append "CXXFLAGS", "-stdlib=libstdc++"
      ENV.append "CFLAGS", "-stdlib=libstdc++"
      ENV.append "LDFLAGS", "-stdlib=libstdc++ -lstdc++"
      # The following is necessary because libtool likes to strip LDFLAGS:
      ENV["CXX"] = "/usr/bin/clang++ -stdlib=libstdc++"
      ...

To edit the formulae in turn, run

for x in snappy leveldb protobuf gflags glog szip boost boost-python lmdb homebrew/science/opencv; do brew edit $x; done

After this, run

for x in snappy leveldb gflags glog szip lmdb homebrew/science/opencv; do brew uninstall $x; brew install --build-from-source -vd $x; done
brew uninstall protobuf; brew install --build-from-source --with-python -vd protobuf
brew install --build-from-source -vd boost boost-python

If this is not done exactly right then linking errors will trouble you.

Homebrew versioning that Homebrew maintains itself as a separate git repository and making the above brew edit FORMULA changes will change files in your local copy of homebrew’s master branch. By default, this will prevent you from updating Homebrew using brew update, as you will get an error message like the following:

$ brew update
error: Your local changes to the following files would be overwritten by merge:
  Library/Formula/lmdb.rb
Please, commit your changes or stash them before you can merge.
Aborting
Error: Failure while executing: git pull -q origin refs/heads/master:refs/remotes/origin/master

One solution is to commit your changes to a separate Homebrew branch, run brew update, and rebase your changes onto the updated master. You’ll have to do this both for the main Homebrew repository in /usr/local/ and the Homebrew science repository that contains OpenCV in /usr/local/Library/Taps/homebrew/homebrew-science, as follows:

cd /usr/local
git checkout -b caffe
git add .
git commit -m "Update Caffe dependencies to use libstdc++"
cd /usr/local/Library/Taps/homebrew/homebrew-science
git checkout -b caffe
git add .
git commit -m "Update Caffe dependencies"

Then, whenever you want to update homebrew, switch back to the master branches, do the update, rebase the caffe branches onto master and fix any conflicts:

# Switch batch to homebrew master branches
cd /usr/local
git checkout master
cd /usr/local/Library/Taps/homebrew/homebrew-science
git checkout master

# Update homebrew; hopefully this works without errors!
brew update

# Switch back to the caffe branches with the formulae that you modified earlier
cd /usr/local
git rebase master caffe
# Fix any merge conflicts and commit to caffe branch
cd /usr/local/Library/Taps/homebrew/homebrew-science
git rebase master caffe
# Fix any merge conflicts and commit to caffe branch

At this point, you should be running the latest Homebrew packages and your Caffe-related modifications will remain in place.
```

Done!

---

![inline 100%](http://i.imgur.com/Ac6zj1X.png)

---

# Docker 등판

[ryankennedyio/deepdream](https://hub.docker.com/r/ryankennedyio/deepdream/)

```
$ git clone https://github.com/ryankennedyio/deep-dream-generator.git
$ cd deep-dream-generator
$ docker run -d \
    -p 443:8888 \
    -e "PASSWORD=password" \
    -v $(pwd):/src \
    ryankennedyio/deepdream
...
a4ea7d082a79e6251a4
```

---

## [fit] https://192.168.59.103

![fit](http://i.imgur.com/eiHtA6y.png)

---

# 더 자세히 이해하기

[Running deep dream on Windows and OSX](http://ryankennedy.io/running-the-deep-dream/)

---

# Gitlab
### 난이도: 최상

---

# Gitlab?

* Github와 비슷한 설치형 오픈소스 Git 호스팅 서비스
* 서비스도 있고, 직접 설치해서 사용하는 것도 가능
* 개발자에게도 어려운 설치
  * 한때 설치하기 어렵기레 정평이 나있었음
* Git, ssh, Database, Redis, Ruby, Rails...

---

# [sameersbn/docker-gitlab](http://www.damagehead.com/docker-gitlab/)

```
# Run Postgres Container
$ docker run --name gitlab-postgresql -d \
    --env 'DB_NAME=gitlabhq_production' \
    --env 'DB_USER=gitlab' --env 'DB_PASS=password' \
    --volume /srv/docker/gitlab/postgresql:/var/lib/postgresql \
    sameersbn/postgresql:9.4-2

# Run Redis Container
$ docker run --name gitlab-redis -d \
    --volume /srv/docker/gitlab/redis:/var/lib/redis \
    sameersbn/redis:latest # Redis Container

# Run Gitlab Container
$ docker run --name gitlab -d \
    --link gitlab-postgresql:postgresql --link gitlab-redis:redisio \
    --publish 10022:22 --publish 10080:80 \
    --env 'GITLAB_PORT=10080' --env 'GITLAB_SSH_PORT=10022' \
    --volume /srv/docker/gitlab/gitlab:/home/git/data \
    sameersbn/gitlab:7.13.3
```

---

# Wait 5 minute

![](http://i.imgur.com/3lf8a9C.png)

---

# [fit] http://192.168.59.103:10080
### root / 5iveL!fe

![](http://i.imgur.com/COfYsUG.png)

---

# [fit] Build once, Run anywhere

---

# 감사합니다 :)

## [fit] <br><br><br>propellerheaven@gmail.com
