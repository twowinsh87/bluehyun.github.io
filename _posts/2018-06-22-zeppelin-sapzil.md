---
layout: post
title:  "zeppelin 빌드하기"
subtitle:   "zeppelin 빌드하기"
categories: data
tags: zeppelin
comments: true
---

최신 zeppelin 빌드하기 
## mac 기준으로 작성합니다.

github 가서 [zepplin githup](https://github.com/apache/zeppelin/) 또는 terminal 에서

>다운로드 받을때는 최신 버전을 받도록 하자. <br>개발중이므로 rc version을 사용하길 권장함<br>[마스터버전다운링크](https://github.com/apache/zeppelin/archive/master.zip)

```
git clone https://github.com/apache/zeppelin.git
git checkout v0.8.0-rc5
```
하단의 [Build from source](https://zeppelin.apache.org/docs/latest/install/build.html) 를 보면 받은 소스를 빌드 하는 방법에 대해 나와있다.

```
mvn clean package -DskipTests
```
**하.지.만**
<h2>작동하지 않는다!!!</h2>

**mvn** 작동하지 않는다 **maven** 이 설치 되지 않았기 때문이다.

maven 을 설치하자

```
brew install maven
```

maven 을 설치하고 빌드 한 뒤 실행하면 된다.
에러가 나는 경우가 있다.
<br>

* 프로세스가 실행중인지 확인하자
* zeppelin 에서 스파크 버전을 보자 2.2.0 이면<br> zeppelin/conf/ zeppelin.env.sh 에서 export SHARK_HOME 지정 하거나<br> zeppelin inter 에서 설치된 spark 경로를 기입하면 된다.

> SPARK_HOME	/Users/hyeonju/des/spark


## 아래는 삽질의 역사를 기록 한것

maven 설치 후 빌드 명령어를 입력 하니 에러가 난다....

```
[ERROR] The goal you specified requires a project to execute but there is no POM in this directory (.../zeppelin_old). Please verify you invoked Maven from the correct directory. -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MissingProjectException
```

> 에러 해결...기존 zeppelin 설치 폴더를 old 로 바꾸고 다운로드한 폴더를 zeppelin 으로 변경 후 터미널에서는 기존 old 폴더로 인식해서 **pom.xml** 파일을 찾지 못하는 오류였음. </br>terminal 에서 상위 폴더로 갔다 오니 ............!@#@##$%$%^%

한 20분 걸린다..는건 뻥임

```
[INFO] Total time: 01:03 h
[INFO] Finished at: 2018-06-20T23:34:31+09:00
[INFO] Final Memory: 305M/1917M
```
......

책보다가 라그 하다가 시간 좀 때우다가 다 되서 실행시키니 또 에러난다.
...

***모르겠다 다시 빌드해보자***

```
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 06:04 min
[INFO] Finished at: 2018-06-21T00:14:37+09:00
[INFO] Final Memory: 305M/2065M
[INFO] ------------------------------------------------------------------------
```

개 짧음..ㄷㄷㄷ

역시 에러.ㅠㅠ...


```
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/Users/hyeonju/des/zeppelin/zeppelin-server/target/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/Users/hyeonju/des/zeppelin/zeppelin-zengine/target/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/Users/hyeonju/des/zeppelin/zeppelin-interpreter/target/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
Exception in thread "main" java.lang.ExceptionInInitializerError
    at org.apache.zeppelin.conf.ZeppelinConfiguration.create(ZeppelinConfiguration.java:136)
    at org.apache.zeppelin.server.ZeppelinServer.main(ZeppelinServer.java:193)
```

프로세스 가 실행중임. 기존에 실행중인 zeppelin 다 죽이고 하면 됨
>ps -ef | grep zeppelin 으로 찾아서<br>
>kill -9 ***프로세스번호***
