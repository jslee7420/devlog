---
title: "Generic 와일드 카드"
excerpt: ""

categories:
  - TIL
tags:
  - [Java, Generic]

toc: true
toc_sticky: true

date: 2021-07-28
last_modified_at: 2021-07-28
---

## 제네릭 와일드 카드의 탄생 배경

아래와 같은 구조로 클래스가 구성된 경우

- Animal
  - Cat
    - Tiger
  - Dog

```java
ArrayList<Animal> = ArrayList<Dog> // 불가능 ArrayList<type>을 하나의 타입으로 보아야한다.
```

## 와일드카드

제네릭 타입에 상관없이 모든 타입을 받아주는 역할을 함

- \<?>
- \<? extends ClassName>: 타입의 상한선 지정
- \<? super ClassName>: 타입의 하한선 지정

```java
ArrayList<?> = ArrayList<Dog>;
ArrayList<?> = ArrayList<Cat>;
ArrayList<?> = ArrayList<Animal>;
ArrayList<?> = ArrayList<String>;

ArrayList<? extends Animal> = ArrayList<Dog>; // Animal 포함
ArrayList<? extends Animal> = ArrayList<Cat>;
ArrayList<? extends Animal> = ArrayList<Animal>;
ArrayList<? extends Animal> = ArrayList<Tiger>;

ArrayList<? super Tiger> = ArrayList<Tiger>; // Tiger 포함
ArrayList<? super Tiger> = ArrayList<Cat>;
ArrayList<? super Tiger> = ArrayList<Animal>;
ArrayList<? super Tiger> = ArrayList<Object>;
```

다른 예

```java
calculate(ArrayList<? extends Number> list){
    // 모든 숫자형 데이터를 받아와 계산을 해줄 수 있음, 타입별 오버라이딩 불필요
}
```
