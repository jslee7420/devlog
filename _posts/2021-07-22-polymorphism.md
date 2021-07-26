---
title: "다형성"
excerpt: "객체 지향의 꽃 다형성에 대해 알아보자"

categories:
  - Java
tags:
  - [Java, Polymorphism]

toc: true
toc_sticky: true

date: 2021-07-22
last_modified_at: 2021-07-23
---

하나의 객체가 많은 형(타입)을 가질 수 있는 성질  
정의: 상속관계에 있을때 조상 클래스의 타입으로 자식 클래스 객체를 레퍼런스 할 수 있다.  
다형성의 전제 조건은 상속이다.

## 다형성의 대분류

- 객체 다형성: Type 다형성
- 메소드 다형성: 다중정의(overloading), 재정의(overriding)

## 다형성과 참조형 객체의 형 변환

메모리에 있더라도 참조하는 변수의 타입에 따라 접근할 수 있는 내용이 제한된다. 참조하는 변수가 포함하는 내용까지만 접근 가능하다.

```java
class Person{
    public void sayHi{
        System.out.println("hi");
    }
}

Obejct obj = new Person();
obj.sayHi();// 불가능
```

### 참조형 객체의 형변환

- child -> super: 묵시적 형변환
- super -> child: 명시적 형변환 필요(생략 불가능)
  ```java
  Phone phone = new SmartPhone();
  Smartphone sPhone = (SmartPhone)phone;
  ```
- 조상을 무작정 자손으로 바꿀 수는 없다.(메모리에 자손의 영역에 해당하는 내용이 없는 객체인 경우), 형변환은 일어나지만 메서드 호출시 오류가 발생할 수 있다.
  - instance of 연산자: 실제 메모리에 있는 객체가 특정 클래스 타입인지 boolean으로 리턴
    ```java
    Person person = new Person();
    if(person instanceof SpiderMan){
        SpiderMan sman = (SpiderMan) person;
    }
    ```

## 참조변수의 레벨에 따른 객체의 멤버 연결

- 상속 관계에서 객체의 멤버 변수가 중복될때 참조 변수의 타입에 따라 참조되는 멤버 변수가 달라진다.
- 상속 관계에서 객체의 메서드가 중복될 때(pverride되었을때), 무조건 자식 클래스의 메서드가 호출됨(**최대한 메모리에 생성된 실제 객체에 최적화 된 메서드가 동작**)

## 다형성의 활용

### 활용1. 이형집합 배열

- 배열은 같은 타입의 데이터를 묶음으로 다룬다. 다형성을 이용하면 공통 부모 조상을 이용하여 서로 다른 타입의 객체를 하나의 배열로 다룰 수 있다.
- Object의 배열은 어떤 타입의 객체도 저장 가능

### 활용2. 매개변수의 다형성

- 조상을 파라미터로 처리하여 객체의 타입에 따라 메서를 만들 필요가 없어짐.
- Java API 처럼 공통기능인 경우 Object를 파라미터로 사용하지만 많은 경우 비즈니스 로직상 최상위 객체 사용 권장

### 활용3. 리턴 타입 다형성

- 리턴 타입을 조상 클래스로 사용하여 다형성 구현

## 동적 바인딩

runtime에 객체를 따라가서 실제 그 객체에 재정의된 메소드를 확인 후 호출하는 것.(<-> 정적 바인딩:compile time)

```java
Employee e = new Engineer();
e.getInfo();
```

위 코드에서 compile time에서는 Employee의 getInfo()메서드로 인식, 런타임에서는 Engineer 객체의 getInfo 메서드로 인식(동적 바인딩)하여 그것을 호출
