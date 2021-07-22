---
title: "Annotation"
excerpt: "어노테이션의 의미와 예"

categories:
  - Java
tags:
  - [Java, annotation]

toc: true
toc_sticky: true

date: 2021-07-22
last_modified_at: 2021-07-22
---

- 컴파일러, JVM, 프레임워크 등이 보는 주석
- 소스코드에 붙여높은 라벨로 코드에 대한 정보 추가(소스 코드의 구조 변경, 환경 설정 정보 추가 등의 작업 진행)

JDK1.5 기본 annotation 예

- @Deprecated: 컴파일러에게 해당 메서드가 더 이상 사용되지 않는다고 알려줌
- @Override: 컴파일러에게 해당 메서드는 overrid한 메서드임을 알려줌(super class에 선언되어 있는 메서드인지 컴파일러가 확인 후 알려줌)
- @SuppressWarnings: 컴파일러에게 사소한 warning을 무시하라고 알려줌
