---
title: "완전탐색"
excerpt: "순열, 조합, 부분집합"

categories:
  - Algorithm
tags:
  - [Java, algorithm]

toc: true
toc_sticky: true

date: 2021-08-14
last_modified_at: 2021-08-14
---

## 완전탐색이란?

완전 탐색은 가능한 모든 경우의 수를 시도해보는 방법입니다. Brute-force 혹은 generate-and-test기법이라고도 불립니다. 모든 경우의 수를 생성하고 테스트하기 때문에 수행 속도는 느리지만, 해답을 찾아내지 못할 확률이 작습니다. 상대적으로 빠른 시간에 알고리즘을 설계할수 있지만 경우의 수가 많은 경우에는 사용할 수 없을 수도 있습니다. 보통 순열, 조합, 부분집합과 같은 조합적 문제들과 연관이됩니다.

## 순열(Permutation)

서로 다른 n개중에서 r개를 택하여 나열하는 것을 순열이라고 합니다. 수학적으로 nPr과 같이 표현합니다. nPr은 다음과 같은 식이 성립합니다.

nPr = n _ (n-1) _ (n-2) _... _ (n-r+1)  
nPn = n!

nPn 문제에서 n이 12를 넘어가는 경우 12! = 479,001,600으로 시간복잡도가 폭발적으로 증가하기 때문에 **n이 12를 넘어가는 경우 순열을 사용해서 문제를 풀 수 없습니다.**

r개의 원소를 선택한다고 했을때 각 자리에서 이미 선택된 원소를 제외한 원소들 중 하나의 원소를 선택하여야 합니다. 이를 코드로 옮겨봅시다.

### 반복문을 통한 순열 생성

r이 고정된 값이고 크기가 작은 경우 for문을 사용하여 쉽고 빠르게 순열을 구현할 수 있습니다. 뽑아야하는 원소의 수만큼 for문을 중첩하여 구합니다.

```java
import java.util.Arrays;

public class Permutation {
	/*
	 * 3P3
	 */
	static int N, R, numbers[], result[];
	public static void main(String[] args) {
		N = 3;
		R = 3;
		numbers = new int[] {1,2,3};
		result = new int[R];

		for(int i=0;i<N;i++) {
			for(int j=0;j<N;j++) {
				if(j==i) continue;
				for(int k=0;k<N;k++) {
					if(k==j||k==i) continue;
					result[0] = numbers[i];
					result[1] = numbers[j];
					result[2] = numbers[k];
					System.out.println(Arrays.toString(result));
				}
			}
		}
	}
}
```

### 재귀적으로 구현한 순열 생성

구현단계에서 몇개의 원소를 선택하여 나열해야하는지 알수 없는 경우 재귀적으로 구현하여야 합니다.

```java
import java.util.Arrays;

public class Permutation {
	/*
	 * 3P3
	 */
	static int N, R, numbers[], result[];
	static boolean[] isSelected;
	public static void main(String[] args) {
		N = 3;
		R = 3;
		numbers = new int[] {1,2,3};// 순열을 만들어야 하는 원소들을 저장하는 배열
		result = new int[R]; // 순열 결과 저장 배열
		isSelected = new boolean[N]; // 원소 선택 여부 체크하는 배열

		permutation(0);
	}

	private static void permutation(int cnt) {
		if(cnt==R) {// 모든 자리의 수를 결정하면 순열 완성
			System.out.println(Arrays.toString(result));
			return;
		}
		for(int i=0;i<N;i++) { // 각 자리에 모든 원소 대입 시도
			if(isSelected[i])continue; // 이미 다른 자리에서 사용하는 원소면 스킵
			result[cnt] = numbers[i]; // 결과 배열에 원소 넣기
			isSelected[i] = true; // 원소 사용 여부 체크
			permutation(cnt+1); // 재귀 호출
			isSelected[i] = false; // 원소 사용여부 해제
		}
	}
}

```

### + 비트마스킹 활용

boolean배열을 대신하여 비트 마스킹으로 이미 선택한 원소를 구분할 수 있습니다. 비트마스킹이 boolean배열보다 연산속도에서 더 빠른 성능을 보입니다.

```java
import java.util.Arrays;

public class Permutation {
	/*
	 * 3P3
	 */
	static int N, R, numbers[], result[];
	public static void main(String[] args) {
		N = 3;
		R = 3;
		numbers = new int[] {1,2,3};// 순열을 만들어야 하는 원소들을 저장하는 배열
		result = new int[R]; // 순열 결과 저장 배열

		permutation(0, 0);
	}

	private static void permutation(int cnt, int flag) {
		if(cnt==R) {// 모든 자리의 수를 결정하면 순열 완성
			System.out.println(Arrays.toString(result));
			return;
		}
		for(int i=0;i<N;i++) { // 각 자리에 모든 원소 대입 시도
			if((flag&1<<i)!=0)continue; // 이미 다른 자리에서 사용하는 원소면 스킵
			result[cnt] = numbers[i]; // 결과 배열에 원소 넣기
			permutation(cnt+1, flag|(1<<i)); // 재귀 호출(원소 사용 여부 체크)
		}
	}
}
```

### 중복 순열

원소의 중복을 허용하는 순열을 중복 순열이라고 합니다. 중복 순열은 원소 사용 여부를 체크하지 않음으로써 구현가능합니다.

```java
import java.util.Arrays;

public class Permutation {
	/*
	 * 3P3
	 */
	static int N, R, numbers[], result[];
	public static void main(String[] args) {
		N = 3;
		R = 3;
		numbers = new int[] {1,2,3};// 순열을 만들어야 하는 원소들을 저장하는 배열
		result = new int[R]; // 순열 결과 저장 배열

		permutation(0);
	}

	private static void permutation(int cnt) {
		if(cnt==R) {// 모든 자리의 수를 결정하면 순열 완성
			System.out.println(Arrays.toString(result));
			return;
		}
		for(int i=0;i<N;i++) { // 각 자리에 모든 원소 대입 시도
			result[cnt] = numbers[i]; // 결과 배열에 원소 넣기
			permutation(cnt+1); // 재귀 호출
		}
	}
}

```

## 조합(Combination)

서로 다른 n개의 원소중에서 r개를 순서 없이 골라낸 것을 조합이라고 합니다. 수학적으로 nCr과 같이 표현합니다. nCr은 다음과 같은 식이 성립합니다.

nCr = n! / (n-r)!r!  
nCr = n-1Cr-1 + n-1Cr  
nC0 = 1

조합의 경우 nCn/2에서의 경우의 수로 시간 복잡도를 판단합니다. 30C15 = 1억 5000 이므로 이를 암기하여 시간복잡도 계산의 기준으로 사용하는 것이 좋습니다.

조합은 순서에 상관없이 원소를 뽑아야 합니다. 자리를 옮겨가며 원소를 뽑을때 앞에서 뽑은 숫자보다 큰 숫자를 뽑도록 강제하면 이를 구현할 수 있습니다.

### 반복문을 통한 조합 생성

순열과 마찬가지로 R의 크기가 작고 고정되어 있으면 for문을 중첩하여 조합을 구할 수 있습니다.

```java
import java.util.Arrays;

public class Combination {
	/*
	 * 5C3
	 */

	static int N, R, numbers[], result[];
	public static void main(String[] args) {
		N = 5;
		R = 3;
		numbers = new int[] {1,2,3,4,5};// 순열을 만들어야 하는 원소들을 저장하는 배열
		result = new int[R]; // 조합 결과 저장 배열

		for(int i=0;i<N;i++) {
			for(int j=i+1;j<N;j++) {
				for(int k=j+1;k<N;k++) {
					result[0] = numbers[i];
					result[1] = numbers[j];
					result[2] = numbers[k];
					System.out.println(Arrays.toString(result));
				}
			}
		}
	}
}

```

### 재귀적으로 구현한 조합 생성

```java
import java.util.Arrays;

public class Combination {
	/*
	 * 5C3
	 */

	static int N, R, numbers[], result[];
	public static void main(String[] args) {
		N = 5;
		R = 3;
		numbers = new int[] {1,2,3,4,5};// 순열을 만들어야 하는 원소들을 저장하는 배열
		result = new int[R]; // 조합 결과 저장 배열

		combination(0,0);
	}
	private static void combination(int cnt, int start) {
		if(cnt==R) {// 각 자리의 원소가 모두 결정되면 조합 완성
			System.out.println(Arrays.toString(result));
			return;
		}
		for(int i=start;i<N;i++) {
			result[cnt] = numbers[i];
			combination(cnt+1, i+1);
		}
	}

}

```

### 중복 조합

원소의 중복을 허용하는 조합을 중복 조합이라고 합니다. 바로 앞자리에 뽑은 숫자 이상의 숫자를 뽑을 수 있도록 제한함으로써 구현가능합니다.

```java
import java.util.Arrays;

public class Combination {
	/*
	 * 5C3
	 */
	static int N, R, numbers[], result[];
	static boolean[] isSelected;
	public static void main(String[] args) {
		N = 5;
		R = 3;
		numbers = new int[] {1,2,3,4,5};// 순열을 만들어야 하는 원소들을 저장하는 배열
		result = new int[R]; // 조합 결과 저장 배열

		combination(0,0);
	}
	private static void combination(int cnt, int start) {
		if(cnt==R) {// 각 자리의 원소가 모두 결정되면 조합 완성
			System.out.println(Arrays.toString(result));
			return;
		}
		for(int i=start;i<N;i++) {
			result[cnt] = numbers[i];
			combination(cnt+1, i); // 다음 자리에는 현재 선택한 원소보다 크거나 같은 원소 선택 가능하도록 제한
		}
	}
}

```

## 부분집합

집합에 포함된 원소들을 선택하는 것입니다. 부분집합의 수는 집합의 원소가 n개 일때, 2^n개입니다. 각 원소를 부분집합에 포함하거나 포함하지 않는 두가지 경우를 모든 원소에 적용한 경우의 수와 같습니다.

2^30 = 1,073,741,824 이므로 n이 30개 이상인 문제에서는 모든 부분 집합을 구하는 것이 아닌 다른 방법을 사용해야 합니다.

### 재귀적으로 구현한 부분집합 생성

```java
public class Subset {

	static int N, R, numbers[], result[];
	static boolean[] isSelected;
	public static void main(String[] args) {
		N = 3;
		R = 3;
		numbers = new int[] {1,2,3}; // 전체 집합
		isSelected = new boolean[N]; // 원소의 포함여부 저장 배열

		subset(0);
	}
	private static void subset(int cnt) {
		if(cnt==N) {
			for(int i=0;i<N;i++) if(isSelected[i]) System.out.print(numbers[i]+" ");
			System.out.println();
			return;
		}
		// 현재 원소를 부분집합에 포함하는 경우
		isSelected[cnt] = true;
		subset(cnt+1);

		// 현재 원소를 부분집합에 포함하지 않는 경우
		isSelected[cnt] = false;
		subset(cnt+1);
	}
}
```

### 바이너리 카운팅을 통한 사전적 순서 부분집합 생성

부분집합을 생성하기 위한 가장 자연스럽고 간단한 방법입니다. 원소 수에 해당하는 N개의 비트열을 이용합니다. n번째 비트값이 1이면 n번째 원소가 포함되었음을 의미합니다.

| 10진수 | 2진수 | {A,B,C} |
| ------ | ----- | ------- |
| 0      | 000   | {}      |
| 1      | 001   | {A}     |
| 2      | 010   | {B}     |
| 3      | 011   | {B,A}   |
| 4      | 100   | {C}     |
| 5      | 101   | {C,A}   |
| 6      | 110   | {C,B}   |
| 7      | 111   | {C,B,A} |

```java
public class Subset {

	static int N, numbers[], result[];
	static boolean[] isSelected;
	public static void main(String[] args) {
		N = 3;
		numbers = new int[] {1,2,3};// 순열을 만들어야 하는 원소들을 저장하는 배열

		subset();

	}
	private static void subset() {
		for(int i=0;i<(1<<N);i++) { // 1<<n: 부분집합의 개수
			for(int j=0;j<N;j++)  // 원소의 수 만큼 비트 비교
      if((i&1<<j)!=0) System.out.print(numbers[j]+" ");
			System.out.println();
		}
	}

}

```
