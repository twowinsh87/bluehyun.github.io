---
layout: post
title:  "데이터 엔지니어 수업 정리 180622"
subtitle:   "패캠 데이터엔지니어 수업"
categories: data
tags: tensorflow
comments: true
---
## tensorflow 설치하기
>mac 용 기준으로 설명합니다.
>

```
윈도우 사용시 anaconda 로 설치하는 방법도 있는데
The Anaconda installation is community supported, not officially supported.
아나콘다 커뮤니티에서 지원 하는거고 공식지원은 아니다 라고 적혀있다.
실무에서 사용시 어떤 문제가 생길지 모르니 native-pip로 설치하자
```
[native-pip install link](https://www.tensorflow.org/install/install_windows#installing_with_native_pip)

gpu 가 없는 mac 이니 좀 수월하게 설치됨

### Prerequisite

* Python
	* Python 2.7
	* Python 3.3+
* pip
	* pip, for Python 2.7
	* pip3, for Python 3.n. 	

	> **pip** 는 파이썬으로 작성된 패키지 소프트웨어를 설치 · 관리하는 패키지 관리 시스템 이다. Python Package Index (PyPI)에서 많은 파이썬 패키지를 찾을 수 있다. 파이썬 2.7.9 이후 버전과 파이썬 3.4 이후 버전은 pip를 기본적으로 포함한다.
[위키백과 pip 설명](https://ko.wikipedia.org/wiki/Pip_(패키지_관리자))


설치 되어 있는지 확인하고 실행하는데 에러난다

<span style="color:red"> distributed 1.21.8 requires msgpack, which is not installed.</span>

기존에 데엔스 수업에서 아나콘다를 깔았기에 기존 아나콘다를 지우고 다시 깔도록 하자


지우고 python 3.6.6 ver 다시 설치

pip 가 bash_profile 에 minconda & anaconda 에 있기에 지우고 다시시작

pip3 설치 확인함


[python link](https://www.python.org/downloads/mac-osx/)

```
hyeonjuui-MacBook-Pro:~ hyeonju$ pip3 -V
pip 10.0.1 from /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages/pip (python 3.6)
```

```
pip3 install tensorflow
```
로 설치함
