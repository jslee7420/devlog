---
title: "Java 반복문, 조건문, 연산자"
excerpt: "Java의 반복문, 조건문, 연산자에 관한 팁"

categories:
  - TIL
tags:
  - [Java, Datatypes]

toc: true
toc_sticky: true

date: 2021-07-23
last_modified_at: 2021-07-23
---

## 연산자

- 삼항 연산자

```java
조건문?true인경우 실행 내용:false인 경우 실행내용
```

- 이항연산자 사용시 최소 단위는 4byte int , short나 byte는 int로 바꿔주어야한다.
- 단항 연산자는 무관

## 조건문

**if 문에서 tip:**

서로 배타적인 조건은 if~if로 사용할 시 불필요한 조건 확인 연산이 일어나므로 if else로 사용

if~else if 가 여러 개인 경우 가장 위에 true빈도가 가장 높은 조건 위치시키기

**switch문 tip:**

값의 동등비교에 특화된 조건분기문

표현식의 값에 해당하는 case로 jump => case의 배치 순서가 실행 속도에 영향을 주지 않는다. 이것이 동등비교만 가능한 이유

표현식에 올 수 있는 값: byte, short, int, char, String(java 7부터)

case문에는 리터럴이나 상수만을 허용한다

## 반복문

1. while문: 선조건 후수행
2. do~while문: 선수행 후조건
3. for문: 반복횟수가 명확한 경우 사용
4. foreach문: 반복가능한 집합의 원소들을 꺼내어 처리”조회목적” -> array, iterable 타입
   1. 장점: 자료구조 사용에 대한 추상화
   2. 단점: 원소값의 수정이 불가능(지역변수의 수정이기 때문)
