footer: Ruby 기반 원격 코드 실행기 © nacyot 2014 -
slidenumbers: true

# [fit] Docker 기반
# [fit] 원격 코드 실행기

---

# [fit] Docker Casual Talk #2
### 2015. 01. 26.
### 2015. 09. 09. update

---

![fit](http://i.imgur.com/BVz3cIx.png)

---

# Codewars

![fit](http://i.imgur.com/Y9Qh4yE.png)

---

# Slack

![fit](http://i.imgur.com/q6HN9l9.png)

---

# 시각화 스터디

![fit](http://i.imgur.com/tkO1Ph6.png)

---

# [fit] 프로그래머라면 코드로 이야기....

---

# [fit]봇이 있었으면 좋겠다

---

# 냐옹이봇

![fit](http://i.imgur.com/7iUwylC.png)

---

# 냐옹냐옹

![fit](http://i.imgur.com/lMbXEaH.png)

---

# Codewars 평가기

![fit](http://i.imgur.com/EH0w4FW.png)

---

# 없어짐...

![fit](http://i.imgur.com/Z3hVAsf.png)

---

# 찾아냄!

![fit](http://i.imgur.com/BpMbqhb.png)

---

# Deprecated?

## org repo는 없어지고, README도 없고...

---

# 코드를 뜯어보니...

## cli에서 특정 언어에 해당하는
## docker image에 run을 실행

---

# [fit] 이미지만 있으면 됨 'ㅇ'

![fit](http://i.imgur.com/wO1OeFS.png)

---

## 사용법도 알아냄

![fit](http://i.imgur.com/adzJiUX.png)

---

# 이제 서버만 있으면 되겠다

* 상상의 나래를 펼쳐보자
* express로 대충 api 2~3개 만들면 되겠지...
* 고정 `api_key` 같은 것도 있음 좋겠고...

---

# express 이미 있네!

![fit](http://i.imgur.com/GUZ3y0T.png)

---

# 사용법도 알아냄

![fit](http://i.imgur.com/vxWCfFh.png)

---

# apiKey도 이미 있네!

![fit](http://i.imgur.com/eQp7I3c.png)

---

# Hubot이 등장할 차례

![fit](http://i.imgur.com/9KcSxjD.png)

---

# [fit] http 요청하고, 포맷팅

---

# [fit] 서버는 호스트에서 동작...

---

# Dockerize!

![fit](http://i.imgur.com/G7G9LV6.png)

---

# 시연

## Languages
## Sample

---

# 보안

---

# `system('rm -rf /')`

* 도커 위에서 도니까 어떻게든 되겠지...
* 호스트와 분리되어 있음

---

# `while True`

* 실제로는 명령어가 wrapping 돼있음
* 컨테이너는 6초 후에 알아서 사망

---

# `:(){ :|:& };:`

limit nproc 20 100
limit nofile 50 100
limit fsize 102400000 204800000

---

# 그리고 어차피...

* 메인 서버도 DO에서 단독으로 돌아감
* 털어봤자.... 먼지 안 나옴

---

# Thank you!

## [@nacyo_t](https://twitter.com/nacyo_t)
