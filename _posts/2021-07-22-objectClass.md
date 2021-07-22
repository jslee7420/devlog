---
title: "Object Class"
excerpt: "최상위 객체 Object Class"

categories:
  - Java
tags:
  - [Java, Object]

toc: true
toc_sticky: true

date: 2021-07-22
last_modified_at: 2021-07-22
---

- 모든 클래스의 조상 클래스
- 별도의 extends 선언이 없는 클래스들은 extends Object가 생략됨
- 모든 클래스에는 Object클래스에 정의된 메서드가 있음(hasCode, toString 등등)
- 멤버 변수가 없음

## 재정의가 필요한 주요 메서드

### toString 메서드

객체를 문자열로 변경해주는 메서드

```java
public String toString(){
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
```

- 기본적으로 객체의 이름과 주소값 리턴
- 하지만 우리가 궁금한 내용은 주소값이 아니므로 사용하기 위해서는 overriding 필수!

### equals 메서드

두 객체가 같은지 확인하는 메서드
