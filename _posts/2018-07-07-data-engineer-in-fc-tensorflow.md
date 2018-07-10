---
layout: post
title:  "tensorflow tutorial"
subtitle:   "tensorflow 로 머신러닝 맛보기"
categories: data
tags: tensorflow
comments: true
---

### tensorflow tutorial 해보자


### tensorboard
시각화를 도와주는 툴

log 를 만들어서
로그 디렉토리로 이동
tensorboard -logdir=.

현재 디렉토리기에 . 으로 표현함

### Estimato
tf.estimator.LinearRegressor
아주 간편하게 모델을 생성하고 학습 가능


###RNN(머신러닝)

>머신러닝 태그 하나 만들어야겠다

RNN 은 스테이트를 가지고 있다
스테이트는 수많은 단어인데, 문맥 이라 보면 된다.

스테이트는 중간, 마지막 스테이트가 있다.

loss 를 정의 할 수 있다

* 언어모델(language model) 연속된 단어들의 등장화률을 예측 하는 모델
* 확률적 언어 모델을 만들려먼 이전에 나온 단어들을 많이 학습 할 수록 정확하다
	* 2-gram, 3-gram, 4-gram
* n-gram을 늘릴수록 메모리가 엄청 필요하다.
	* 이 문제를 해결하려고 나온게 **RNN**

RNN 을 확실히 이해하려면 로우하게 직접 구현해봐야;;

RNN 을 **잘** 학습시키기는 어렵다
layer 가 깊어질 수 록 점점 어려워짐

####Vanishing Gradient 문제
* 너무 오래된 정보까지 참조하려다 보니 어디서 부터 잘못됐는지 역추적이 힘듬


### LSTM(Long Short-Term Memory)

* RNN 과 유사한 구조
* RNN 은 반복구조로 기억력을 가지게 된다
* RNN 은 최근 몇개 단어 정도의 기억력만 가지게 된다
* LSTM 은 더욱 긴 기억력을 가지기 위한 구조
	* RNN 이 몇개의 단어라면, LSTM 은 수백단어

####LSTM 내부
* Forget gate
* Input gate
* cell state


### GRU(Gated Recurrent Unit)
* LSTM 을 약간 업글한 모델

### Attention Mechanism
이론이다!!!

인간의 인지과정에서 특정 순간/사물에 집중하는 모습에서 아이디어를 얻음

RNN 같은 모델의 경우 하나의 Hidden State에 모든 내용을 기억하기 어려워짐

Hidden State(기억,또는 메모리) 를 저장하고 있다가, 이전의 State 를 활용함



###CNN
다음 시간에 ...

RNN 과 근본적으로 비슷하지만 이미지 분석할때 사용함. RNN 처럼 단어분석에 사용가능함
