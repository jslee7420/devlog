---
title: "플로이드-워샬 알고리즘"
excerpt: "최단 거리쌍 구하기"

categories:
  - TIL
tags:
  - [algorithmn]

toc: true
toc_sticky: true

date: 2021-09-17
last_modified_at: 2021-09-17
---

## 무한대값 설정시 주의 할점

```java
Math.min(INF, IFN+a)
```

에서 INF를 Integer.MAX_INTEGER로 두게 되면 IFN+a에서 오버 플로우가 발생하여 IFN+a가 선택되어 버립니다. 따라서 INF는 간선이 갖을 수 있는 최대 비용 \* N-2+1 로 설정하여야 합니다.

## 반복문에서 주의해야 할 점

```java
for(int k=0; k<4; k++){
    for(int k=0; k<4; k++){
        for(int k=0; k<4; k++){

        }
    }
}
```

1. k=i 인 경우: 경유지가 출발지와 같으므로 의미가 없음
2. k=j 인 경우: 경유지가 도착지와 같으므로 의미가 없음
3. i=j 인 경우: 출발지와 도착지와 같으므로 의미가 없음(간선이 음수값을 갖는 경우에는 갱신이 일어날 수 있음)

## 하나의 2차원 배열을 사용하여 구현할 수 있는 이유 증명

## 반복문 순서가 k, i, j가 되어야 하는 이유

## 양수간선으로만 구성된 프로이드 워살에서 연산을 줄이는 방법

```java
for (int k = 0; k < N; k++) {
			for (int i = 0; i < N; i++) {
				if(i==k) continue; // 출발지 = 경유지  -> 경유효과 없음
				for (int j = 0; j < N; j++) {
//					if(j==k || i==j) continue; // 출발지= 도착지 or 출발지=도착지 -> 경유효과 없음
					D[i][j] = Math.min(D[i][j], D[i][k] + D[k][j]);
				}
			}
		}
```

if문을 줄여서 연산 속도 향상

## 음수 간선이 포함된 플로이드 워샬

```java
for (int k = 0; k < N; k++) {
			for (int i = 0; i < N; i++) {
				if(i==k) continue; // 출발지 = 경유지  -> 경유효과 없음
				for (int j = 0; j < N; j++) {
//					if(j==k || i==j) continue; // 출발지= 도착지 or 출발지=도착지 -> 경유효과 없음
					D[i][j] = Math.min(D[i][j], D[i][k] + D[k][j]);
				}
			}
		}
```
