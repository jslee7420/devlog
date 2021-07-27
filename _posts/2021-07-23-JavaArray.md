---
title: "Java 배열"
excerpt: "Java 1차원배열과 다차원 배열"

categories:
  - TIL
tags:
  - [Java, Array]

toc: true
toc_sticky: true

date: 2021-07-23
last_modified_at: 2021-07-23
---

배열은 같은 타입의 자료형이 연속적으로 존재하는 자료구조이다. 자바에서 배열은 객체이다. reference type 데이터이고 반복문과 결합하여 일괄처리가 가능하다. 리턴값, 매개변수 전달시 활용 가능하고 처음생성시 기본값으로 초기화가 자동진행된다.

장점:

1. 데이터 관리의 용이함: 반복문과 결합하여 일괄처리가 가능
2. 리턴값, 매개변수 전달시 활용 가능

단점: 크기가 고정 -> 배열 새로 생성, 기존 내용 복사

### 1차원 배열 생성

```java
데이터 타입[] 참조변수 = new 데이터타입[size];
```

### 1차원 배열 사용

참조변수[] <- 인덱스: 첫원소 기준 offset, 유효 인덱스: 0~배열 길이 -1(벗어나면 ArrayIndexOutofBoundsException 발생)

### 1차원 배열 초기화

데이터 타입[] 참초변수 = new 데이터타입[]{val1, val2,…}

배열은 그 형태가 크게 달라질 수 있기 때문에 생성자가 필요한 클래스가 아닌 형태로 제작됨

값을 넣어서 초기화하는 경우 “new 데이터타입[]” 생략가능

선언후 초기화 시에는 new 사용해야함

```java
int[] points;
points={1,3,5,7,6}; //불가능

points = new int[]{1,3,5,7,6} //가능
```

- 최초 메모리 할당 이후 , 배열은 변경 불가능
- 개별 요소는 다른 값으로 변경이 가능하지만 삭제는 불가능, 크기를 늘리거나 줄일 수 없다.
- 따라서 배열의 크기를 늘리려면 더큰 배열을 생성해서 기존의 값을 복사해야함
- 자바에서 배열의 크기는 런타임에 결정됨(객체의 동적 생성) 따라서 변수로 배열의 크기를 지정할 수 있다. 이와 다르게 C에서는 컴파일 타임에 배열의 크기가 결정되므로 변수를 사용할 수 없다.
- Array.toString: 일차원배열 출력
- Array.deepToString: 이차원이상의 배열 출력

### 다차원 배열

array of array: 배열 여러개를 모아 다시 배열로 관리하는 것이 다차원 배열

1차원 객체 배열 생성시 배열 생성 후 객체를 생성해서 넣어주어야함

```java
Order orders[] = new Order[100];
orders[0] = new Order();
```

1차원 객체 배열을 다차원 배열과 같은 효과를 낸다.