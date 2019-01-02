---
layout: post
title:  "[Spring boot] Springboot 02_설정, Annotation"
subtitle:   "[Spring boot] Springboot 02_설정, Annotation"
description : "[Spring boot] Springboot 02_설정, Annotation"
keywords : "springboot, annotation, Rest Api, 어노테이션, spring, 자동설정"
categories: etc
tags: springboot
comments: true
---


> # Spring boot 02
> Spring boot Annotation  
> 자동설정, Rest Api  

## - 자동설정
- 스프링 부트는 두 단계로 나눠서 읽어(등록)들인다.
	- (1) componentScan을 사용
	- (2) EnableAutoConfiguration

## - Spring boot 자동설정 Annotation
- @SpringBootApplication
	- @ComponentScan + @EnableAutoConfiguration


### (1) @ComponentScan

> @ComponentScan은 ComponentScan 어노테이션이 달린 class의 package 부터  
> 하위 패키지 까지 훑고, 	아래의 어노테이션을 전부 bean으로 등록한다.  
> @Component (@Congiguration @Repository @Service @Contontroller @RestController)  


### (2) @EnableAutoCongiguration
> Spring.factories를 찾고  
> org.springframework.book.autoconfigure.EnableAutoConfiguration의  
> 모든 key값을 보고, 그 것에 해당하는 class를 보고(configuration)  
> 해당하는 class가 엄청많은데 ConditionalOn~~~ 조건에 맞는 것만 bean으로 등록  


### (3) @SpringBootApplication
> 위의 두가지(1),(2) 스캔과정을 @SpringBootApplication 선언 하나로 모든 작업을 함.

<br>

## - Rest Api

### 스프링 REST 지원
- http Method(= 데이터 처리방식, SQL)
	- Post(= Create,Insert), Get(= Read,Select), Put(= Update, Update), Delete(= Delete,Delete)
	- @GetMapping, @PostMapping @PutMapping, @PatchMapping, @DeleteMapping (스프링 4.3)


### Restful Api
- Get : /users/12 : 식별자가 12인 유저를 반환(select)
- Post: /users : 유저를 생성
- Put : /users/12 : 12번 사용자의 {"name":aaa} name을 aaa로 수정
	- /users : {"name":aaa} 유저 모두의 이름을 aaa로 수정
- Delete: /users/12 : 12번 사용자의 데이터를 삭제
	-  /users : 사용자의 데이터 모두를 삭제

### 스프링 Rest Api 처리 방식

- **@Controller (웹 MVC 처리)**
	- @GetMapping("/경로"), @PostMapping("/경로"): 일반적인 웹 처리에서는 @Controller 레벨에서 경로에 따른 요청을 처리하고, 알맞은 view를 return한다. post의 경우에는 body에 값을 포함하고 있다.

- **@Controller + @ResponseBody**
	- 메소드에 @ResponseBody를 사용해서 객체를 Json 형태로 응답할 수 있음. (Json 형태로 변환하는 viewresolver가 처리)

- **@RestController(@Controller + @ResponseBody)**  
	- @RestController는 @ResponseBody를 사용하지 않고, 객체를 Json 형태로 응답할 수 있음. (Json 형태로 변환하는 viewresolver가 처리)

- **RequestParam**
	- 쿼리 스트링으로 처리
	- (도메인/selectByAddress?address=gangnam)로 전달에서 address=gangnam 값을 받을 수 있음.

```
@GetMapping("/selectByAddress")
	public ResponseEntity<List> getSelectByAddress(@RequestParam("address") String address) {

	...생략...
}
```

- **Pathvariable**

```
@GetMapping("/selectByIdx/{key}")
	public ResponseEntity<T> getByKey(@PathVariable Integer key) {

	...생략...
}
```

- **RequestBody**
	- 아래 예시의 경우 body 값으로 Test 객체를 받음

```
// test 객체 -> Json 형태로 return
@PostMapping("/test")
public Test testJson1(@RequestBody Test test){

	....생략...
}
```
