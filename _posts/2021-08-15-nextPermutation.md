---
title: "nextPermutation"
excerpt: "순열 생성을 순서대로"

categories:
  - Algorithm
tags:
  - [Java, algorithm, nextPermutation]

  
toc: true
toc_sticky: true

date: 2021-08-15
last_modified_at: 2021-08-15
---

nextPermutation은 현재 주어진 순열보다 큰 순열을 순서대로 생성해 낼 수 있습니다. 예를 들어 {1,2,3,4} 다음 순열은 {1,2,4,3} 입니다. 다음과 같은 과정과 원리로 진행됩니다.

1. 뒤에서 부터 앞으로 가면서 숫자의 크기가 증가하다가 작아지는 숫자(A)을 찾습니다.
2. 하락한 숫자 뒤의 숫자들 해당 숫자보다 첫번째로 큰 숫자(B)를 찾습니다.
3. A와 B의 자리를 바꿉니다.
4. B뒤에 있는 숫자들을 뒤에서부터 오름차순으로 정렬합니다.

위와 같은 스텝을 따르면 주어진 순열의 다음 순열을 찾을 수 있습니다.

## nextPermutation을 활용한 순열 만들기

```java
import java.util.Arrays;

public class NextPermutation {
	static int N, R;
	public static void main(String[] args) {
		int[] numbers = new int[] {1,2,3,4,5};// 순열을 만들어야 하는 원소들을 저장하는 배열
		N = numbers.length;
		R = 3;
		do {
			System.out.println(Arrays.toString(numbers));
		}while(np(numbers));
		
	}
	private static boolean np(int[] numbers) {
		
		// step1. 꼭대기 위치 i 찾기
		int i = N-1;
		while(i!=0 && numbers[i-1]>numbers[i]) i--;
		if(i==0) return false;
		
		// step2. i-1원소보다 첫번째로 큰 수 찾기
		int j = N-1;
		while(numbers[i-1]>numbers[j]) j--;
		
		// step3. swap
		swap(numbers, i-1,j);
		
		// step4. i-1 뒤로 오름차순 정렬
		while(i<j) swap(numbers, i++, j--);
		
		return true;
	}
	private static void swap(int[] numbers, int i, int j) {
		int temp = numbers[i];
		numbers[i] = numbers[j];
		numbers[j] = temp;
	}
}
```
## nextPermutation을 활용한 조합 만들기
nextPermutation으로 조합을 생성할 수 도 있습니다. 조합에 사용하고자 하는 원소들을 갖는 배열과 같은 크기의 정수형 배열을 만들고 뽑아야되는 원소의 수만큼을 1로 만들어 이 배열에 대해 nextPermutation을 수행합니다. 1이 있는 자리의 인덱스가 원래 배열에서 선택된 원소들의 인덱스를 뜻합니다.

```java
import java.util.Arrays;

public class NextPermutation {
	static int N, R;
	public static void main(String[] args) {
		int[] numbers = new int[] {1,2,3,4,5};// 순열을 만들어야 하는 원소들을 저장하는 배열
		N = numbers.length;
		R = 3;
		int[] isSelected = new int[N];
		for(int i=0;i<R;i++) isSelected[N-1-i] = 1;
		do {
			for(int i=0;i<N;i++) if(isSelected[i]==1) System.out.print(numbers[i]+" ");
			System.out.println();
		}while(np(isSelected));
		
	}
	private static boolean np(int[] numbers) {
		
		// step1. 꼭대기 위치 i 찾기
		int i = N-1;
		while(i>0 && numbers[i-1]>=numbers[i]) i--;
		if(i==0) return false;
		
		// step2. i-1원소보다 첫번째로 큰 수 찾기
		int j = N-1;
		while(numbers[i-1]>=numbers[j]) j--;
		
		// step3. swap
		swap(numbers, i-1,j);
		
		// step4. i-1 뒤로 오름차순 정렬
		while(i<j) swap(numbers, i++, j--);
		
		return true;
	}
	private static void swap(int[] numbers, int i, int j) {
		int temp = numbers[i];
		numbers[i] = numbers[j];
		numbers[j] = temp;
	}
}

```