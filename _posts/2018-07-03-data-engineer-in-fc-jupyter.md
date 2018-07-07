---
layout: post
title:  "jupyter 로 머신러닝 맛보기"
subtitle:   "jupyter 로 머신러닝 맛보기"
categories: data
tags: jupyter
comments: true
---
>7.7 일... 전 수업 내용을 정리도 못하고 냅따 올림

### jupyter notebook

fifa wolrd cup data engineer


jupyter 실행

anaconda 를 날리고 다시 깔았지만 허허허허

jupyter notebook 에서 matplotlib 을 호출 못한다

결국 설치함

```
sudo pip3 insatll matplotlib
```

-------------------------------

## 추가로 des 수업 jupyter 로 수업 이어하기

namuwiki_20180326.json 파일을 **8기가** 다!

jupyter 에서 ijson 라이브러리를 설치하고 사용하자

8기가의 json을 통으로 읽어 들이기엔 메모리 터질지도

나무위키의 내용을 word2vac으로 학습시키기에는 문서의 내용이 깔끔해야하기에 적당히 코드정규식 같은 놈으로 편집을 해주자

구글링 하면 코드가 많이 있으니 적당히 찾아서 쓰자

```
# We want only plain texts, so strip wiki grammer.
# Refer this link to know more about grammar. https://namu.wiki/w/%EB%82%98%EB%AC%B4%EC%9C%84%ED%82%A4:%EB%AC%B8%EB%B2%95%20%EB%8F%84%EC%9B%80%EB%A7%90

# Use regular expression to capture some pattern

# see http://stackoverflow.com/questions/2718196/find-all-chinese-text-in-a-string-using-python-and-regex
chinese = re.compile(u'[⺀-⺙⺛-⻳⼀-⿕々〇〡-〩〸-〺〻㐀-䶵一-鿃豈-鶴侮-頻並-龎]', re.UNICODE)
japanese = re.compile(u'[\u3000-\u303f\u3040-\u309f\u30a0-\u30ff\uff00-\uff9f\u4e00-\u9faf\u3400-\u4dbf]', re.UNICODE)

# hangul = re.compile('[^ ㄱ-ㅣ가-힣]+') # 한글과 띄어쓰기를 제외한 모든 글자
# hangul = re.compile('[^ \u3131-\u3163\uac00-\ud7a3]+')  # 위와 동일
# result = hangul.sub('', s) # 한글과 띄어쓰기를 제외한 모든 부분을 제거


def strip_wiki_literal(text):               
    text = re.sub(r"\{\{\{#\!html[^\}]*\}\}\}", '', text, flags=re.IGNORECASE|re.MULTILINE|re.DOTALL) # remove html
    text = re.sub(r"#redirect .*", '', text, flags=re.IGNORECASE) # remove redirect
    text = re.sub(r"\[\[분류:.*", '', text) # remove 분류
    text = re.sub(r"\[\[파일:.*", '', text) # remove 파일
    text = re.sub(r"\* 상위 문서 ?:.*", '', text) # remove 상위문서        
    text = re.sub(r"\[youtube\(\w+\)\]", '', text, flags=re.IGNORECASE) # remove youtube
    text = re.sub(r"\[include\(([^\]|]*)(\|[^]]*)?\]", r'\1', text, flags=re.IGNORECASE) # remove include
    text = re.sub(r"\[\[(?:[^\]|]*\|)?([^\]|]+)\]\]", r'\1', text) # remove link
    text = re.sub(r"\[\*([^\]]*)\]", '', text) # remove 각주
    text = re.sub(r"\{\{\{([^\ }|]*) ([^\}|]*)\}\}\}", r'\2', text) # remove text color/size
    text = re.sub(r"'''([^']*)'''", r'\1', text) # remove text bold
    text = re.sub(r"(~~|--)([^']*)(~~|--)", '', text) # remove strike-through
    text = re.sub(r"\|\|(.*)\|\|", '', text) # remove table
    text = re.sub(r"\n\s*\n*", '\n', text) # remove empty line                       
    text = chinese.sub('', text) # remove chinese
    text = japanese.sub('', text) # remove japanese
    return text
```


konlpy install 하고 테스트 하는 과정에서 jupyter 가 죽는다!!!

***왜 난?!!?!?!?***

예측컨데 아마도 tensorflow 설치할때 anaconda 를 지웠고 다시 설치 해놓으면서 환경이 꼬인듯 하다

<img src='https://bluehyun.github.io/assets/img/jupyter/jupyterdead.png'>

추가정보를 눌러보니 java 6 se 를 설치하라는 사이트로 넘어가고 설치 했더니 된다

<img src='https://bluehyun.github.io/assets/img/jupyter/javaseinstall.png'>


> konlpy 라이브러리는 twitter 에서 만든 형태소 분석기 라이브러리


나무위키를 트위터 라이브러리로 형태소 분석 돌려놓고

word2vec-gensim 을 알아보자

word2vec 은 사전을 만들고 학습을 한다.


으아아아..빡세다

따라가기 바쁨.ㅠㅠ


이론!!!

컴퓨터에서의 단어 표현

##Word Embedding

####one hot encoding

* 10차원 - 10 가지를 표현 할 수 있음
* 일상 단어를 표현하려면 2~5만 차원, 큰 단어목록은 50만차원 정도 가 필요함


####vector Representation

* 비슷한 단어끼리 비슷한 곳에 위치 하도록


####확률적 언어 모델
* 중심 단어가 주어졌을때 주변 단어들이 나올 확률을 구하고, 이 확률을 높이는 방향으로 벡터를 조정함
* 확률 언어 모델로 구글 번역기, 음성인식을 만든다


###Word2vec
> 확률적 언어 모델을 만들다가 뽀록으로 발견됨

* 기존의 Neural Net Language Model
	- 주변의 단어갯수 N , 사전의 크기 V, Projection Layer 크기 P

####종류
* CBOW
* Skip-Gram


####word2vec 원리

중심단어를 c(center word), 주변단어를 o(outer word) 가 등장할 확률을 softmax를 사용하여 다음과 같이 정의한다..

공식이다.

>softmax란?<br>
>임의의 값을 0,1 로 맵핑시키는 logistic function 의 하나

u,v 벡터가 어쩌다 보니 나오는가보다...로 공식을 이해하려면 직접 구현해보거나, 찬찬히 뜯어보거라.......

cost function : log-likelihood 를 사용

####negative sampling
중심단어 하나에 대해 모든 단어의 확률을 계산해야 하므로 계산량이 많음
이를 단순화 하여 일부 5-20개의 단어만 뽑아서 계산을 수행해도 유사한 효과를 얻을수있다
이러한것을 ***negative sampling*** 이라 한다

비슷한걸로는
seq2vec , doc2vec 이 있다.


이 수업을 어느정도 이해하고 있나
점수 준 이유
강사님은 수업 준비를 잘 하나
점수 이유
이 수업을 친구에게 추천하고 싶은가
점수 이유
피드백으로 앞으로 진행될 강의 , 패캠에 바라는 점 작성
