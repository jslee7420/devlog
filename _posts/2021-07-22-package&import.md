---
title: "패키지"
excerpt: "패키지의 정의와 탄생 배경"

categories:
  - Java
tags:
  - [Java, 역사, 탄생 배경]

toc: true
toc_sticky: true

date: 2021-07-22
last_modified_at: 2021-07-22
---

- pc에서 폴더와 같은 역할
- 계층적 구조
- 물리적으로는 패키지는 클래스 파일을 담고 있는 디렉토리
- 첫번째 문장에 하나의 패키지만 선언
- 모든 클래스는 반드시 하나의 패키지에 속한다.
- 생략시 default package(default package는 사용하지 않는다.)

### naming rule

- 소속.프로젝트.용도(com.ssafy.hrm.commn)

## import

- 다른패키지에 선언된 클래스를 사용하기 위한 키워드
- import 패키지명.클래스명;
- import 패키지명.\*;
  - 하위 패키지 까지 import하지 않는다.(import는 클래스단위로)
- import한 패키지의 클래스 이름이 동일한 경우 클래스 이름 앞에 전체 패키지 명을 입력
  - jaca.util.List list = new java.util.ArrayList();
- default import package
  - java.lang.\*;
  - String, System 등 포함
