---
title: "에러와 예외"
excerpt: "Java Error and Exception"

categories:
  - TIL
tags:
  - [Java, Error, Exception]

toc: true
toc_sticky: true

date: 2021-07-27
last_modified_at: 2021-07-28
---

어떤 원인에 의해 오동작 또는 비정상적으로 종료되는 경우를 에러 혹은 예외라고 합니다.

## 심각도에 따른 분류

- Error
  - 메모리 부족, stack overflow와 같이 일단 발생하면 복구 불가능한 상황
  - 프로그램의 비정상 종료를 막을 수 없음 -> 디버깅 필요
- Exception
  - 읽으려는 파일이 없거나 네트워크 연결이 안 되는 등 수습될 수 있는 비교적 상태가 약한 것들
  - 프로그램 코드에 의해 수습될 수 있는 상황

# 예외처리(Exception handling)

예외 발생 시 프로그램의 비 정상 종료를 막고 정상 적인 실행 상태를 유지하는 것
예외의 감지 및 예외 발생 시 동작할 코드작성이 필요합니다.

## 예외클래스 계층

ㅇㅣ미지 필요

- checked exception
  - 예외 대처 코드가 없으면 컴파일 X
  - ex) IOException, FileNotFoundException 등등
- unchecked exception(Runtime exception)
  - 예외 대처 코드가 없어도 컴파일은 진행
  - ex) ArithmeticException

## Exception handling

### try~catch구문

```java
try{
    // 예외가 발생할 수 있는 코드
}catch(XXException e){ // 던진 예외를 받음
    // 예외 발생시 처리 코드
}
```

### Exception 객체의 정보 활용

**Throwable의 주요 메서드**
|메서드|설명|
|------|---|
|public String getMessage()|발생된 예외에 대한 구체적인 메세지를 반환|
|public Throwable getCause()||
|public void printStackTrace()||

계층적 예외
트리를 알아야 계층적 예외를 처리할 수 있다.

try catch finally

자식의 재정의된 메소드는 부모 클래스 혹은 인터페이스의 메소드보다 더 상위 타입 Exception을 던질 수 없다. 호출자는 상위 클래스에 맞게 컴파일되기 때문.
