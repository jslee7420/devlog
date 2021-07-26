---
title: "this와 super"
excerpt: "Java의 this와 super 예약어"

categories:
  - Java
tags:
  - [Java, this, super]

toc: true
toc_sticky: true

date: 2021-07-23
last_modified_at: 2021-07-23
---

## this

- non-static 영역에서만 사용(instance method, constructor, instance initializer)
- 현재 생성중인, 실행중인 그 객체 자기 자신을 일컫음

### 사용법

1. 지역변수와 인스턴스 변수를 구분할때 사용
   ```java
   void setName(String name){
       this.name=name;
   }
   ```
2. 생성자가 오버로딩된 경우. 자신의 또다른 생성자 호출시 사용
   ```java
   this()
   ```
3. 자기자신의 객체를 메소드의 매개변수로 전달하거나 리턴하기 위해 사용

   ```java
   method(){
       return this; // 자신을 리턴
   }

   method(){
       obj.zzz(this); // 자신을 매개변수로 전달
   }
   ```

### 메모리에 this가 생성되는 과정

인스턴스 메소드가 불리면 스택영역에 인스턴스 메소드 관련 프레임이 생성된다. 해당 프레임 안에 객체를 가르키는 this 변수 생성됨.

## super

- non-static 영역에서 사용
- 현재 생성, 실행중인 객체의 부모를 의미하도록 사용하는 논리적인 개념

### 사용법

1. 자신의 메소드와 부모의 메소드를 구분하기 위해 사용(메소드 재정의 상황)
   ```java
   this.xxx();
   super.xxx();
   ```
2. 자식의 생성자에서 부모 생성자를 명시적으로 호출하기 위해
   ```java
   super();
   ```
