---
layout: post
title:  "[Spring boot] Test 환경 구성 및 설정"
subtitle:   "[Spring boot] Test 환경 구성 및 설정"
description : "[Spring boot] Test 환경 구성 및 설정"
keywords : "springboot, Spring Boot Test, h2, jpa, msa, queryDSL, 스프링테스트"
categories: etc
tags: springboot
comments: true
---


> ## Spring boot Test 환경 구성 및 설정
> h2
> jpa
> query DSL  

### Pom.xml

```
<!-- Test -->
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
	<scope>test</scope>
	<version>1.4.197</version>
</dependency>
```

### class Test

```
@Slf4j
@ActiveProfiles("test") // application-test.yml을 사용
@Transactional
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.NONE) //컨트롤러는 제외
```

### application-test.yml

- application-test.yml 생성 및 작성

```
spring:
  jpa:
    show-sql: true
    open-in-view: true
    hibernate:
      ddl-auto: create
    properties:
      hibernate:
        format_sql: true
        dialect: org.hibernate.dialect.H2Dialect
  datasource:
    url: jdbc:h2:mem:test
  flyway:
    enabled: false

  # test에 console을 사용 할 일은 없지만 혹시나...  
  h2:
    console:
      enabled: true
```

### Runtime시에 data를 h2에 insert
- h2는 메모리 디비이므로 미리 넣어주고 select 관련 테스트가 수월하다.

```
//resources/data.sql

....Entity에 맞게 insert문을 작성...
```

**h2를 활용한 테스트 환경 구성 완료**
