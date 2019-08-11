---
layout: post
title:  "[Java]Reflection"
subtitle:   "[Java]Reflection"
description : "Java Reflection 정리"
keywords : "Java, Reflection, 리플렉션, 자바 리플렉션"
categories: language
tags: java
comments: true
---

> ## Reflection  
> Java 리플렉션 정리  

## Java 

## 리플렉션
- class 객체를 이용해서 클래스의 정보를 얻음(생성자, 필드, 메소드)
- 아래는 주요 메소드 정리

`Field[] getFields()`: public 필드 값을 Field 클래스 배열 타입으로 리턴

`Field[] getDeclaredFields()`: 해당 클래스의 변수 목록을 field 클래스 배열 타입으로 리턴.

`Field getDeclaredField(String name)`: name과 동일한 이름으로 정의된 변수를 Field 클래스 타입으로 리턴한다.

`Method[] getMethods()`: public으로 선언된 모든 메소드 목록을 Method 클래스 배열 타입으로 리턴한다. 해당 클래스에서 사용 가능한 상속받은 메소드도 포함된다.

`Method getMethod(String name, Class... parameterTypes)`: 지정된 이름과 매개변수 타입을 갖는 메소드를 Method 클래스 타입으로 리턴한다.

`Method[] getDeclaredMethods()`: 해당 클래스에서 선언된 모든 메소드 정보를 리턴한다.

`Method getDeclaredMethod(String name, Class... parameterTypes)`: 지정된 이름과 매개변수 타입을 갖는 해당 클래스에서 선언된 메소드를 Method 클래스 타입으로 리턴한다.

`Constructor[] getConstructors()`: 해당 클래스에 선언된 모든 public 생성자의 정보를 Constructor 배열 타입으로 리턴한다.

`Constructor[] getDeclaredConstructors()`: 해당 클래스에서 선언된 모든 생성자의 정보를 Constructor 배열 타입으로 리턴한다.

`int getModifiers()`: 해당 클래스의 접근자(modifier) 정보를 int 타입으로 리턴한다.

`String toString(): 해당 클래스 객체를 문자열로 리턴한다.


출처: https://12bme.tistory.com/129 [길은 가면, 뒤에 있다.]
- 참고: (책)이것이 자바다, [https://12bme.tistory.com/129](https://12bme.tistory.com/129)
