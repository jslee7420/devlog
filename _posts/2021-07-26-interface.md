---
title: "인터페이스"
excerpt: "Java 다형성 인터페이스"

categories:
  - TIL
tags:
  - [Java, interface]

toc: true
toc_sticky: true

date: 2021-07-26
last_modified_at: 2021-07-27
---

인터페이스 정의: 서로다른 두 장치, 소프트웨어를 이어주는 부분

최고 수준의 추상화 단계: 모든 메서드가 abstract 형태
jdk8에서 default method와 static method 추가(body를 가짐)

- 사용자 관점:"What", 사용방법
- 구현자 관점:"How", 동작의 책임(구현)

인터페이스의 핵심: 사용과 구현의 분리!
구현이 변경되어도 사용법은 변화가 없다.

## 형태

클새스와 유사하게 interface 선언
멤버구성
모든 멤버변수는 public static final이며 생략가능
모든 메서드는 public abstract이며 생략 가능(오버라이드 시 접근 제한자는 항상 public)

```java
public interface MyInterface{
public static final int MEMBER1 = 10;
int MEMBER2 =10;

        public abstract void mehtod1(int param);
        void method2(int param);
    }
```

## 인터페이스 상속

클래스와 마찬가지로 extends를 이용해 상속이 가능
클래스와 다른 점은 인터페이스는 다중상속이 가능(헤깔릴 메서드 구현자체가 없다.)

## 인터페이스 구현과 객체 참조

클래스에서 implements 키워드를 사용해서 interface 구현
implements한 클래스는
모든 abstract 메서드를 overrid해서 구현하거나
구현하지 않을 경우 abstract 클래스로 표시해야함
여러개의 interface implements 가능

## 인터페이스 구현과 객체 참조

다형성은 조상 클래스 뿐 아니라 조상 인터페이스에도 적용될 수 있다.

## 인터페이스의 필요성

구현의 강제로 표준화 처리
abstract 메서드 사용
인터페이스를 통한 간접적인 클래스 사용으로 손쉬운 모듈 교체 지원
인터페이스만 바라보기 때문에 구현에 변경이 있어도 사용자 코드는 변경이 없다.
서로 상속의 관계가 없는 클래스들에게 인터페이스를 통한 관계부여로 다형성 확장
이미 상속이 된 클래스에 추가적으로 인터페이스 implements해서 다형성 확장
모듈간 독립적 프로그래밍 가능 -> 개발 기간 단축
UI 작업 팀과 로직 구현팀이 나뉘어진 경우 구현할 내용에 대한 협의를 인터페이스로 표현하고 UI팀에서는 대략적인 구현(호출과 리턴 타입)을 사용해서 UI개발을, 구현팀은 정확한 로직으로 구현을 동시에 할 수 있다.

## default 메서드

인터페이스에 선언된 구현부가 있는 일반 메서드
메서드 ㅇ선언부에 modifier 추가 후 메서드 구현부 작성
접근 제한자는 public 으로 한정됨(생략 가능)

```java
interface DefaultMethodInterface{
void abstractMethod();

        default void defaultMethod(){
            System.out.println("기본 메서드");
        }
    }
```

### 필요성

기존에 interface 기반으로 동작하는 라이브러리의 interface에 추가해야하는 기능이 발생
기존 방식으로라면 모든 구현체들이 추가되는 메서드를 overrice 해야함
default 메서드는 abstract가 아니므로 반드시 구현 필요 없음

default 메서드 충돌
우선순위
super class의 method우선: super class가 구체적인 메서드를 갖는 경우 default method는 무시됨
interface간의 충돌: 하나의 interface에서 default method를 제공하고 다른 interface에서도 같은 이름의 메서드가 있을 때 sub class는 반드시 override해서 충돌 해결

## static method

interface에 선언된 static method
일반 static 메서드와 마찬가지로 별도의 객체 없이 바로 인터페이스 이름으로 접근해서 사용
