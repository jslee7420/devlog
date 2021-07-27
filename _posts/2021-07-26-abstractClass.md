---
title: "추상 클래스"
excerpt: "Java 다형성 추상클래스"

categories:
  - TIL
tags:
  - [Java, 추상클래스]

toc: true
toc_sticky: true

date: 2021-07-26
last_modified_at: 2021-07-26
---

추상 클래스는 상속 전용 클래스입니다. 클래스에 구현부가 없는 메서드가 있어 객체 생성이 불가능합니다.

```java
abstract public class ClassName{
  abstract void methodName();
  public void methodName2(){
    System.out.println("mehtod2");
  }
}
```

- 메서드 선언부만 남기고 구현부는 세미콜론으로 대체
- 구현부가 없다는 의미로 abstract키워드를 메서드 선언부에 추가
- 객체를 생성할 수 없는 클래스라는 의미로 클래스 선언부에 abstract를 추가

## 추상클래스의 필요성

상위 클래스 타입으로써 자식을 참조할 수 있다.
조상 클래스에서 상속받은 abstract 메서드를 재정의 하지 않으면 자식 클래스도 abstract로 선언해야한다.(재정의 하지 않으면 컴파일 에러 발생)

abstract 클래스는 구현의 강제를 통해 프로그램의 안정성 향상
abstract는 UML상에서 이탤릭으로 표현합니다.

서로 다른 클래스에서 비슷한 메소드를 제공하고 여러 클래스 객체를 활용하여 해당 기능을 사용하는 경우 Object 객체로 만들게 되면 매우 번거롭다. 이럴때 추상 클래스를 선언하면 해당 클래스의 추상 메소드로 훨씬 쉽게 사용 가능하다.
