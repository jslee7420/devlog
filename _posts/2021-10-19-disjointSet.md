---
title: "서로소 집합(Disjoint-set)"
excerpt: ""

categories:
  - Algorithm
tags:
  - [algorithm]

toc: true
toc_sticky: true

date: 2021-10-19
last_modified_at: 2021-10-19
---

서로소 집합은 상호배타 집합이라고도 하며 서로 중복 포함된 원소가 없는 집합들을 말합니다. 집합에 속한 하나의 특정 멤버를 대표자로 하여 각 집합들을 구분합니다.

## 서로소 집합을 표현하는 방법

1. 연결리스트

- 같은 집합의 원소들을 하나의 연결리스트로 관리
- 연결리스트의 맨 앞의 원소가 대표자
- 각 원소는 대표자를 가리키는 링크를 갖는다

2. 트리

- 하나의 집합을 트리로 표현
- 자식노드가 부모 노드를 가리키며 루트 노드가 대표자

## 서로소 집합의 연산

- Make-Set(x): 유일한 원소 x를 포함하는 새로운 집합 생성 연산
- Find-Set(x): x를 포함하는 집합을 찾는 연산(대표자를 찾는 연산)
- Union(x,y): x와 y를 포함하는 두 집합을 통합하는 연산

## 트리로 구현한 서로소 집합의 연산

```java
static int[] p; // 인덱스를 노드의 번호로 하고 자신이 가르키는 노드를 원소로 하는 정수형 1차원 배열

public static void makeSet(int n) {
    p = new int[n+1];
    for (int i = 0; i < p.length; i++)
        p[i] = 0;
}

public static int findSet(int a) {
    if(p[a]==a) return a;
    return findSet(p[a]);
}

public static boolean union(int a, int b) {
    int rootA = findSet(a);
    int rootB = findSet(b);
    if(rootA == rootB) return false;
    p[rootA] = rootB;
    return true;
}
```

## 연산의 효율을 높이는 방법

- Rank를 이용한 Union

  - 각 노드는 자신을 루트로 하는 subtree의 높이+1을 음수형태의 랭크로 표현
  - 두 집합을 합칠 때 rank가 낮은 집합을 rank가 높은 집합에 붙이기
  - 전체 트리의 레벨(높이)는 더 높은 랭크의 서브트리와 같음(높이 변화 X)
  - 하지만 두 트리의 높이가 같은 경우 union시 랭크는 1 증가

  ```java
    static int[] p; // 인덱스를 노드의 번호로 하고 자신이 가르키는 노드를 원소로 하는 정수형 1차원 배열

    public static void makeSet(int n) {
        p = new int[n+1];
        for (int i = 0; i < p.length; i++)
            p[i] = -i;
    }

    public static int findSet(int a) {
        if(p[a]<0) return a;
        return findSet(p[a]);
    }

    public static boolean union(int a, int b) {
        int rootA = findSet(a);
        int rootB = findSet(b);
        if(rootA == rootB) return false;
        if(rootA<rootB) p[rootB] = rootA;
        else p[rootA] = rootB;
        return true;
    }
  ```

- Path compression
  - Find-Set을 행하는 과정에서 만나는 모든 노드들이 직접 root를 가리키도록 포인터를 변경
  ```java
  public static int findSet(int a) {
      if(p[a]==a) return a;
      return p[a] = findSet(p[a]);
  }
  ```
