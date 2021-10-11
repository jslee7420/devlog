---
title: "Comparable과 Comparator"
excerpt: "객체의 크기 비교"

categories:
  - Java
tags:
  - [java, database]

toc: true
toc_sticky: true

date: 2021-08-11
last_modified_at: 2021-08-11
---

아래와 같은 코드를 살펴봅시다.

```java
import java.util.Arrays;

public class ArraySortTest {

	public static void main(String[] args) {
		int[] arr  = {50, 30,10,23,45};
		System.out.println("정렬전: "+Arrays.toString(arr));
		Arrays.sort(arr);
		System.out.println("정렬후: "+Arrays.toString(arr));

		String[] arr2 = {"서울","대전","광주","구미","부울경"};
		System.out.println("정렬전: "+Arrays.toString(arr2));
		Arrays.sort(arr2);
		System.out.println("정렬후: "+Arrays.toString(arr2));

        Person[] arr3 = {new Person p1, new Person p2,new Person p3,new Person p4};
		System.out.println("정렬전: "+Arrays.toString(arr2));
		Arrays.sort(arr2);
		System.out.println("정렬후: "+Arrays.toString(arr2));
	}
}
```

primitive type의 경우 값이 하나이기 때문에 크기 비교가 바로 가능합니다. 하지만 reference type 객체간의 크기 비교를 위해서는 무엇을 기준으로 크기를 비교할 것인지를 명시하여야 합니다. Object객체에는 비교하는 메소드가 equals()메소드 뿐인데 이것은 동등비교연산을 할뿐 크기비교는 할수 없습니다. 따라서 어떤 객체가 들어와도 크기비교를 가능하게 하기 위해 Comparable이라는 인터페이스를 implement해서 compareTo라는 추상메서드를 override하여 크기비교를 가능하게 합니다.

위 코드에서 String은 이미 Comparable 인터페이스를 implement한 상태로 바로 크기비교가 가능하여 sorting이 일어나지만 Person객체의 경우 Comparable이 implement되어 있지 않아 sorting이 불가능합니다.

## Comparable<T> 인터페이스

- int compareTo(T o)
- compareTo는 객체가 다른 객체와 자신의 크기를 비교
- 리턴값의 의미

| 리턴값의 부호 | 의미            | 작동        |
| ------------- | --------------- | ----------- |
| 음수          | 내가 o보다 작다 | 둘을 그대로 |
| 0             | 나와 o가 같다   | 둘을 그대로 |
| 양수          | 내가 크다       | 교환        |

## Comparator 클래스

- int compare(T o, T o)
- compare는 제 3의 객체가 서로다른 두 객체의 크기를 비교
- 다차원 배열의 경우 클래스가 아니므로 Comparable 인터페이스 사용불가능 항상 Comparator 클래스를 사용하여야 합니다.
- reverseOrder(): Comparable객체의 CompareTo의 원소의 순서를 반대로 바꿔줌. 따라서 기존의 비교를 반대로 해줌.
