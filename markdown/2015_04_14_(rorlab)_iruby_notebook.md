footer: RORLAB / 주피터(Jupyter) 프로젝트 - IRuby Notebook © [nacyot](https://twitter.com/nacyo_t) 2015 -
slidenumbers: true

# [fit] Jupyter
## [fit] IRuby Notebook

---

## RORLAB 84번째 모임

### 2015. 4. 14.

---

![fit](http://i.imgur.com/BVz3cIx.png)

---

# REPL of Ruby

## irb(루비 내장 REPL)
## [PRY](http://pryrepl.org/) (확장 REPL)

---

# PRY

## [fit] an IRB alternative and runtime developer console

![](http://i.imgur.com/qMuvBjd.png)

---

# IRuby Notebook
## [sciruby/iruby](https://github.com/SciRuby/iruby)

![fit](http://i.imgur.com/XdRZBBQ.png)

---

# Demo #1

* Executing IRuby Notebook server
* [IRuby Notebook interface](https://github.com/SciRuby/iruby)
* Evaluating simple Ruby expressions

---

# What is REPL?

## Read–eval–print loop

---

# from Lisp

---

# IRuby Notebook

## 2012. 3. 25. ~

---

# IPython

## [fit] <br/>2001년부터 만들어진 Python REPL의 확장

---

# IPython 0.0.1

https://gist.github.com/fperez/1579699

![fit inline](http://i.imgur.com/XDYv7v7.png)

---

# Python의 REPL 구현

* 기본 REPL
  * python
* 확장 REPL
  * ipython
  * bpython

---

# [fit] 왜 Python REPL의 확장을 만들었을까?

---

# [fit] 왜 Python REPL의 확장을 만들었을까?

> I started using Python in 2001 and liked the language, but its interactive prompt felt like a crippled toy compared to the systems mentioned(maple, mathematica, etc) above or to a Unix shell.
-- [Fernando Perez](http://blog.fperez.org/2012/01/ipython-notebook-historical.html)

---

# 루비에서의 pry

![fit](http://i.imgur.com/fuyEC08.png)

---

![fit](http://i.imgur.com/fuyEC08.png)

---

# IPython 0.12

---

# IPython 0.12

> The major new feature with this release is the IPython Notebook, an interactive Python interface running in the browser. Download it now, or read more about what’s new.
-- [IPython 0.12 Release Note](http://ipython.org/ipython-doc/rel-0.12/whatsnew/version0.12.html)

---

# [fit] IPython Notebook

## 2011~

![](http://ipython.org/ipython-doc/rel-0.12/_images/notebook_specgram.png)

---

# IPython 0.11

---

# [fit] IPython 0.11 - qtconsole

## Rich GUI IPython client

![fit](http://i.imgur.com/msxxc1P.png)

---

# IPython 0.11 - ZeroMQ

* ZeroMQ 기반 메시지 시스템 도입
* 성능 문제 해결 및 qtconsole 백엔드
* ipython notebook

---

# 기존의 REPL

* 해당하는 실행기 언어로 구현
  * lisp -> lisp, irb -> ruby
  * python -> python
* 클라이언트(셸)와 백엔드(실행기)의 강한 결합
  * 분리하기 어려움
  * REPL이 가지는 근본적인 제약

---

## ZeroMQ가 도입된 이유
# 성능

---

# ZeroMQ가 도입된 이유

> ZeroMQ provides us with much tighter control over memory, higher performance, and its communications are impervious to the Python Global Interpreter Lock because they take place in a system-level C++ thread."
-- [IPython 0.11 Release Note](http://ipython.org/ipython-doc/rel-0.11/whatsnew/version0.11.html#high-level-parallel-computing-with-zeromq)

---

# [fit] ZeroMQ 도입에 주목해야 하는 이유

![fit](http://i.imgur.com/a23rZms.png)

---

# ZeroMQ 이전

단일 프로그램

![inline](http://i.imgur.com/jaCwVre.png)

---

# ZeroMQ 이후

클라이언트와 백엔드의 약한 결합

![inline](http://i.imgur.com/6HV1Vq4.png)

---

# 다양한 클라이언트 지원

* Notebook(client) - IPython Server
  * qtconsole
  * IPython Notebook
  * IPython
  * BIPython

---

# [fit] 다양한 클라이언트 지원(2)

![fit](http://i.imgur.com/hOluhlk.png)

---

![fit](http://i.imgur.com/hOluhlk.png)

---

# Message Protocol

* [Messaging in IPython](https://ipython.org/ipython-doc/dev/development/messaging.html)
* 0.11에서 공개
* 자체 버전을 가지고 있으며 현재 5.0
* ZeroMQ 기반

---

# 실행기(커널)의 분리

* Message Protocol에 따르는 Kernel 개념 도입
* Python 실행기가 Python Kernel로 분리됨

---

# IRuby의 정의

---

# [fit] IRuby = Interactive Ruby?

---

# [fit] IRuby = IPython Kernel for Ruby

![inline](http://i.imgur.com/x794HK9.png)

---

# [fit] IPython은 언어에 비종속적인 REPL

* 커널이 분리되면서 다양한 커널이 개발됨
* 기존의 도구/생태계를 그대로 이용 가능

---

# IPython Kernels

* [IPython kernels for other languages](https://github.com/ipython/ipython/wiki/IPython-kernels-for-other-languages)
  * Julia, Haskell, FSharp, Ruby, Go
  * Scala, Mathics, Aldor, Calico, Erlang
  * Lua, R, OCaml, Forth, Perl, Perl6
  * Octave, Scilab, MathLab, Bash, CSahrp
  * Clojure, Hy, Redis, Javascript, Calysto, ...

---

# IPython 3.0 = Jupyter

* [Project Jupyter](https://jupyter.org/)
  * 더 이상 Python만을 위한 도구가 아님을 인정
  * 파이썬에 관련된 프로젝트 -> IPython
  * 다언어 지원을 위한 프로젝트 -> Jupyter
* Jupyter Protocol
* Jupyter Notebook(HTML+Javascript 분리)

---

# Jupiter

갈릴레오 갈릴레이 - 오래된 훌륭한 시각화 사례
[link](http://www4.ncsu.edu/~kimler/hi322/galmoons.html)

![](http://www4.ncsu.edu/~kimler/hi322/galileo_notebook.gif)

---

# [fit] Jupyter = Julia + Python + R

---

# [fit] Jupyter = Julia + Python + R

![inline](http://curezone.com/upload/Members/new03/omg_wtf_cat.jpg)

---

# [fit] Jupyter 이전 - 타언어 커널 사용법

IPython은 커널에 의존적으로 실행

```
$ ipython notebook --kernel <language>
```

---

# Jupyter 이후 - Kernelspec

특정 커널에 비의존적으로 실행

---

# 설정 디렉터리 구조

```
$ tree -d -L 1 ~/.ipython
~/.ipython
├── db
├── extensions
├── kernels         # <- 여기
├── log
├── nbextensions
├── pid
├── profile_default
├── security
├── startup
└── static
```

---

# [fit] 타언어 커널 사용 -> 다언어 커널 사용

IRuby, IBash 설치 이후

```
$ tree -d -L 1 ~/.ipython/kernels
~/.ipython/kernels
├── ruby
└── bash
```

---

# Jupyter Interface

하나의 Jupyter Instance에서 다언어 커널 실행가능

![inline](http://i.imgur.com/9Av7MxP.png)

---

# Demo 2
   
* Ruby
* Haskell
* Bash

---

# [fit] IPython Notebook

## IPython 0.11~ (2011년~)

---

# [fit] [What is the big deal about IPython Notebooks?](http://www.reddit.com/r/Python/comments/1q9tq7/what_is_the_big_deal_about_ipython_notebooks/)

---

# 웹 애플리케이션

* 범용적인 유저 인터페이스
* 비선형적 코드 실행
* CodeMirror 에디터
* Javascript 환경

---

# 범용적인 유저 인터페이스

* 웹에서 가능한 모든 것
* HTML, CSS, Image, Canvas, SVG, ...

![inline](http://i.imgur.com/DsFq0kl.png)

---

# 비선형적 코드 실행 (1)

선형적인 실행 - REPL의 본질적인 한계

![inline](http://i.imgur.com/7XwpCau.png)

---

# 비선형적 코드 실행 (2)

코드는 셀 단위로 편집하고, 실행되고, 재실행

![inline](http://i.imgur.com/wlT9IjM.png)

---

# CodeMirror 에디터

![inline](http://i.imgur.com/P4q3j5H.png)

---

# Javascript 환경

---

# Demo 3

* [Javascript Magic](http://nbviewer.ipython.org/github/payne92/notebooks/blob/master/00%20Javascript%20In%20Notebooks.ipynb)
* [D3 Notebook 예제(시각화 스터디)](http://nbviewer.ipython.org/gist/nacyot/c0190709f56024eb516e)
* [Interactive Widget](http://nbviewer.ipython.org/github/melund/ipython/blob/3.x/examples/Interactive%20Widgets/Index.ipynb)
* [InlineAttachment 예제](https://github.com/nacyot/jupyter-inline-attachment-sample)

---

# [fit] 여기까지는 프로그래밍 이야기

---

# [fit] 여기부터는 Notebook 이야기

---

# [fit] 왜 Jupyter에 주목해야 하는가?

---

# REPL

* 소모성 프로그래밍 환경
* 보통 짧은 코드 테스트용

---

# REPL의 한계를 넘어서

* 기록을 위한 프로그래밍 환경
* 다양한 표현 지원
* 셀 단위의 코드 편집 지원

---

# 연습과 기록

> Examples are reusable ideas in the form of customizable code snippets; examples can serve as an alternative to fixed, monolithic typologies; examples are a shared extension of memory.
-- [Eyeo 2013 - For example by Mike Bostock](https://vimeo.com/69448223)

---

# Demo 4

* [`naycot/euler_project`](https://github.com/nacyot/euler-project)

---

# [fit] 코드와 글 사이의 본질적인 문제

---

# 코드

IPython code 중 일부 - BSD License

![](http://i.imgur.com/82CI9An.png)

---

# 글

Discourse on Floating Bodies, by Galileo Galilei

![](http://i.imgur.com/l93fvIP.png)

---

# 코드와 글 ≒ 물과 기름

* 각자 고유한 맥락을 가짐
  * 전혀 다른 방식으로 쓰여짐
  * 도구로 처리할 수 있는 부분이 다름
* 문법 분석과 맞춤법/오타
  * Syntax 하이라이팅
  * 80자 제한과 문단 개념

---

# 글 안에 포함된 "죽어있는" 코드

책에 실린 코드

![inline](http://i.imgur.com/SCue2pU.png)

---

# [fit] 코드와 글의 고유한 맥락에 대한 고민들

* Donal E. Knuth - Literate Programming
* Alan Kay - Active Essays
* Fernando Perez - Data-driven Journalism

---

# [fit] Literate Programming(문학적 프로그래밍)

> Let us change our traditional attitude to the construction of programs: Instead of imagining that our main task is to instruct a computer what to do, let us concentrate rather on explaining to human beings what we want a computer to do.
-- [Donald E. Knuth](http://www.literateprogramming.com/knuthweb.pdf)

---

# [fit] 같은 평면 위에 올려진 코드와 문서

---

# CWeb (1)

![](http://i.imgur.com/vBG44d1.png)

---

# CWeb (2)

[구조적 문서화를 위한 CWEB 시스템](http://faq.ktug.org/wiki/pds/SampleDocument/cwebman.pdf)

![](http://i.imgur.com/ngMttQq.png)

---

# [fit] "살아있는" 코드 안에 포함된 글

---

# Sphinx (1)

[ansible-modules-core/cloud/docker/docker.py](https://github.com/ansible/ansible-modules-core/blob/16ece8f87c9d1ad3a2a32f4d0b8c9a674eac05d9/cloud/docker/docker.py)

![inline](http://i.imgur.com/c4HXJvh.png)

---

# Sphinx (2)

[Ansible Documentation - docker](http://docs.ansible.com/docker_module.html)

![inline](http://i.imgur.com/9qA4AgH.png)

---

# [fit] 글 안에 포함된 "살아있는" 코드

---

# knitr (1)

[from __future__ import dream
knitr를 이용한 워드프레스 포스팅하기](http://freesearch.pe.kr/archives/3265)

![inline](http://i.imgur.com/bKtUjkQ.png)

---

# knitr (2)

[from __future__ import dream
knitr를 이용한 워드프레스 포스팅하기](http://freesearch.pe.kr/archives/3265)

![inline](http://i.imgur.com/UQxQvZn.png)

---

# d3 도서(o'reilly)

[O'Reilly Atlas + jsbin](http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#_the_new_chart)

![inline](http://i.imgur.com/TaVzgub.png)

---

# Active Essays

> An “Active Essay” is a new kind of literacy, combining a written essay, live simulations, and the programs that make them work in order to provide a deep explanation of a dynamic system. The reader works directly with multiple ways of representing the concepts under discussion. By “playing with” the simulations and code, the reader gets some hands-on experience with the topic.
-- [Alan Kay](http://web.archive.org/web/20060710213801/http://www.squeakland.org/whatis/a_essays.html)

---

# [fit] Steven Wittens' Presentation

* [Making WebGL Dance](http://acko.net/files/fullfrontal/fullfrontal/webglmath/online.html)
* [Source Code](https://github.com/unconed/fullfrontal)

---

# Setosa blog

* [Markov Chains](http://setosa.io/blog/2014/07/26/markov-chains/)

---

# Jiongster

* [..., Why React is Awesome](http://jlongster.com/Removing-User-Interface-Complexity,-or-Why-React-is-Awesome)
* [Presenting The Most Over-Engineered Blog Ever](http://jlongster.com/Presenting-The-Most-Over-Engineered-Blog-Ever)

---

# Awesome!

* 표현 도구로서의 자바스크립트
* 하지만, 하나의 웹사이트라고 봐야...
* 저작 환경 = 그냥 프로그래밍

---

# 그리고, Jupyter

---

# "코드"와 "연구"의 만남

현존하는 가장 범용적인 *Scientific Research 환경*.

---

# "글"과 "코드"의 고유한 맥락

현존하는 가장 범용적인 *Active Essays 저작 환경*.

---

# Scientific Research

![inline](http://i.imgur.com/d0o5qcp.png)

---

# Data-driven Journalism

> Our job with IPython is to think deeply about questions regarding the intersection of computing, data and science, but it's clear to me at this point that we can contribute in contexts beyond pure scientific research. I hope we'll be able to provide folks who have a direct intersection with the public, such as journalists, with tools that help a more informed and productive debate.
-- [Fernando Perez](http://nbviewer.ipython.org/github/fperez/blog/blob/master/130418-Data-driven%20journalism.ipynb)

---

# Reproducible Notebook

* 코드를 실행해보는 것에 그치지 않음
  * 저장하고, 게시하고, 공유하도록 도와줌
  * ipython 환경이 있다면 실행해보는 것도 가능
* HTML 등 다른 포맷으로 출력 기능 제공
  * [nbviewer](http://nbviewer.ipython.org/)
  * ipynb 뷰어 서버

---

# [fit] IPython Notebook으로 블로그하기

* [Fernando Perez
Blogging with the IPython notebook](http://blog.fperez.org/2012/09/blogging-with-ipython-notebook.html)
* [Pythonic Perambulations](https://jakevdp.github.io/)
* [Box and Whisker
IPython Notebook으로 블로깅하기](http://www.boxnwhis.kr/2015/02/10/blogging_with_python.html)

---

# 사례

[루비의 꽃, 열거자 Enumerable 모듈](http://blog.nacyot.com/articles/2014-04-19-ruby-enumerable/)
[루비(Ruby) 테스트 프레임워크 RSpec 2.14 매쳐](http://blog.nacyot.com/articles/2014-04-07-rspec-matchers/)

![inline](http://i.imgur.com/mYNDVjT.png)

---

# `.ipynb` 빌드

[`helper/markdown_helper.rb`](https://github.com/nacyot/blog.nacyot.com-source/blob/54fc2aa73e37d1614023ede8f497ecda4bc895b8/helper/markdown_helper.rb#L85)

```
def render_ipynb(filename)
  source = "./source/iruby/#{filename}.ipynb"
  output = "./source/iruby/#{filename}"
  cmd = "ipython nbconvert --to html --template basic #{source} --output #{output}"
  system(cmd)
end
```

---

# Demo 5

* 루비의 꽃, 열거자 Enumerable 모듈 실행하기

---

# Thank you!

## [@nacyo_t](https://twitter.com/nacyo_t)
