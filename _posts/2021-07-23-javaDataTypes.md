---
title: "Java 데이터 타입"
excerpt: "Java의 자료형들"

categories:
  - Java
tags:
  - [Java, Datatypes]

toc: true
toc_sticky: true

date: 2021-07-23
last_modified_at: 2021-07-24
---

- Primitive type: 변수 공간에 값이 직접 들어가는 자료형, 원자성의 data
  - 논리형: Boolean(true, false/호환성 없음) => 1bit
  - 문자형: char(‘’, “”와 다름) => 2byte(유니코드를 지원하기 때문에 2byte지원)
  - 정수형: byte, short, int(default), long => 1byte, 2byte,4byte, 8byte
  - 실수형: float, double(default) => 4byte, 8byte
- Reference type(non-Primitive type): 객체를 참조할 수 있는 참조타입
  - Class type
  - Interface type
  - Array type

### primitive type 데이터들의 저장가능한 수의 범위 비교

byte<short!=char<int<long<float<double

----------------------------------------→묵시적 형변환

←---------------------------------------- 명시적 형변환

- float과 double은 부동 소수점을 사용하므로 더 큰 범위의 수를 저장할 수 있다.
- 실수는 오차가 있기 때문에 소수점이 없으면 정수형을 사용
- char에는 음수가 없으므로 short 보다 더 큰 양수 저장가능
- Big Decimal long형 보다 큰 수를 다룰 때 사용, 수를 문자열로 바꾸어 사용
- **int 사용시 주의 점 overflow**
- **실수 사용시 주의점 연산이 정확하지 않음**

### primitive type과 Reference type 비교

primitive type의 경우 변수공간에 값이 직접 저장된다. 하지만 reference type의 경우 변수 공간에 저장되는 것은 객체의 레퍼런스이고 메모리의 heap 영역에 객체가 생성된다. 변수에 저장된 값은 이 객체를 가르킨다.
