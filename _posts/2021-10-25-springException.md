---
title: "ExceptionHandler와 ControllerAdvice를 이용한 예외처리"
excerpt: "Spring에서 예외처리 쉽게 하기"

categories:
  - Spring
tags:
  - [spring]

toc: true
toc_sticky: true

date: 2021-10-25
last_modified_at: 2021-10-25
---

보통 예외처리는 try catch 문을 이용합니다. 고려해야할 예외가 많을 경우 모든 컨트롤러 혹은 서비스에 try catch구문을 작성해야해서 컨트롤러와 서비스의 본래 기능 구현에 집중하기가 어렵습니다. 이럴때 스프링의 @ExceptionHandler, @ControllerAdvice 어노테이션을 사용하면 보다 쉽게 예외처리를 할 수 있습니다.

## @ExceptionHandler

@ExceptionHandler는 @Controller, @RestController가 적용된 Bean내의 모든 메소드에서 발생하는 예외를 잡아와서 하나의 메서드에서 처리해주는 기능을 합니다.

```java
@Controller
public class Controller {
    ...
    ...
    @ExceptionHandler(NullPointerException.class)
    public String handleException(Exception e) {
        e.printStackTrace();
        return "test";
    }
}
```

예외를 처리하는 코드가 포함된 메소드(메소드명은 자유) 위에 @ExceptionHandler라는 어노테이션을 쓰고 인자로 캐치하고 싶은 예외클래스를 등록해주면 됩니다.

Controller Bean에서 NullPointerException이
발생하면, @ExceptionHandler(NullPointerException.class)가 적용된 메서드가 호출됩니다.

만약 하나로 더 많은 예외 처리를 하길 원한다면 모든 예외의 부모클래스인
Exception.class를 핸들링하여 최종적으로 이 handler를 거쳐 처리되도록 하면 됩니다. (@ExceptionHandler(Exception.class))

## @ControllerAdvice

@ControllerAdvice는 모든 @Controller 즉, 전역에서 발생할 수 있는 예외를 잡아 처리해주는 annotation입니다.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(NullPointerException.class)
    public String handleException() {
        e.printStackTrace();
        return "test";
    }

}
```

새로운 controllerAdvice 클래스를 만들어, @ControllerAdvice와 @ExceptionHandler annotation을 붙여 처리하고 싶은 예외를 잡아 처리하면 됩니다.

만약 ControllerAdvice와 함께 각각의 컨트롤러에 ExceptionHandler가 존재한다면 컨트롤러에 있는 ExceptionHandler가 더 높은 우선순위를 갖습니다.
