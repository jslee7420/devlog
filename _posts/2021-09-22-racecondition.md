---
title: "Race Condition"
excerpt: "상호작용 프로세싱에서의 문제점"

categories:
  - OS
tags:
  - [OS, race condition]

toc: true
toc_sticky: true

date: 2021-09-22
last_modified_at: 2021-09-22
---
## Race Condition이란?

**여러 프로세스(혹은 쓰레드)가  동시에 공통 자원을 읽거나 쓰는 동작을 하고 그 실행 결과가 접근이 발생한 순서에 의존하는 상황**을 경쟁 상태(race condition)라고 합니다. 경쟁상태에서는 실행 결과가 개발자의 의도와 다르게 나올 수 있습니다. 다음 Producer-Consumer 예시를 살펴봅시다.<br><br>
쓰레드 A는 공유버퍼에 새항목을 추가하고 전역변수 counter의 값을 1 증가시키는 작동을 합니다. 쓰레드 B는 공유 버퍼에서 한 항목을 꺼내고 전역변수 counter의 값을 1 감소시키는 작동을 합니다.

```C
// Thread A(Producer)
while(true){
  /* Produce an item in next produced */
  while(count == BUFFER_SIZE)
  ; /* do nothing */

  buffer[in] = next_produced;
  in = (in + 1 ) % BUFFER_SIZE;
  count++;
}

// Thread B(Consumer)
while(true){
  while(count == 0)
  ; /* do nothing */

  next_consumed = buffer[out];
  out  = (out +1) % BUFFER_SIZE;
  count--;
  /* consume the item in next_consumed */
}
```

현재 카운터의 값이 5라면 두 쓰레드가 각각 한번 실행된 결과는 원래 값인 5가 나와야 합니다. 하지만, 아래와 같은 순서로 번갈아 실행되면 counter는 개발자의 의도와 달리 4 또는 6 이 될 수 있습니다.

<br>
<table>
  <tr>
    <th></th>
    <th>Thread A</th>
    <th>Thread B</th>
  </tr>
  <tr>
    <th>고급어</th>
    <td>counter = counter + 1;</td>
    <td>counter = counter - 1;</td>
  </tr>
  <tr>
    <th>기계어</th>
    <td>register1 = counter;<br>register1 = register1 + 1;<br>counter = register1;</td>
    <td>register2 = counter;<br>register2 = register2 - 1;<br>
counter = register2;</td>
  </tr>
  <tr>
    <td colspan=3>T0: Thread A가 register1 = counter 수행 {register1 = 5}<br>
T1: Thread A가 register1 = register1+1 수행 {register1 = 6}<br>
T2: Thread B가 register2 = counter 수행 {register2 = 5}<br>
T3: Thread B가 register2 = register2 1 수행 {register2 = 4}<br>
T4: Thread A가 counter = register1 수행 {counter = 6}<br>
T5: Thread B가 counter = register2 수행 {counter = 4}</td>
  </tr>
</table>
<br>

위와 같이 Race condition에서는 비정상적인 결과가 나올 수 있습니다. 이 문제는 항상 발생하는 게 아니라 기계어 레벨에서 특정한 순서로 수행되었을 때만 발생하게 되므로 디버깅 시에는 문제점이 전혀 보이지 않아 고치기가 매우 어렵습니다. 그래서 멀티프로세스 프로그래밍을 할 경우에 Race condition 방지를 위해 **프로세스 동기화(한번에 하나의 프로세스만 자원에 접근하도록 하는 것)** 를 해야합니다.

## 임계구역(Critical Section)

프로세스 동기화를 위해 우리는 임계구역에 대해 알 필요가 있습니다. 임계구역이란 **다른 프로세스와 공유하는 자원에 접근하는 코드 세그먼트**를 말합니다. 프로세스 동기화는 임계구역에 한번에 하나의 프로세스만 들어갈 수 있도록 함으로써 구현할 수 있습니다. 임계 구역 진입 통제를 위해 작성하는 코드는 다음과 같이 크게 네부분으로 나뉩니다.

```c
while(true){
  // entry section: 임계구역 진입 요청 코드

  // critical section:  임계 구역

  // exit section: 임계구역에서 빠져나오는 코드

  // remainder section: 나머지 코드 총칭
}
```

### 임계구역 문제에서 고려해야할 요구조건들

프로세스들이 데이터를 협력적으로 공유하기 위해서 자신들의 활동을 동기화 할 때 사용할 수 있는 프로토콜을 설계하는 것을 **임계구역 문제**라고 하고 이에 대한 해결안은 다음과 같은 세가지 요구조건을 충족해야 합니다.

1. **상호 배제(mutual exclusion)**: 프로세스 Pi가 자기의 임계구역에서 실행된다면 다른 프로세스 들은 그들 자신의 임계구역에서 실행될 수 없다.
2. **진행(progress)**: 임계구역에서 실행되는 프로세스가 없고 임계구역으로 진입하려고 하는 다른 프로세스들이 있다면, 기다리는 프로세스들만 다음에 누가 그 임계구역으로 진입할 수 있는지를 결정하는 데 참여가능하며 이 선택은 무한정 연기될 수 없다.
3. **한정된 대기(bounded waiting)***: 프로세스가 자기의 임계구역에 진입하려는 요청을 한 후부터 그 요청이 허용될 때까지 다른 프로세스들이 그들 자신의 임계구역에 진입하도록 허용되는 횟수에 한계가 있어야 한다.

이러한 요구조건들이 모두 충족되어야 프로세스 동기화가 정상작동할 수 있으며 앞으로 살펴볼 여러 동기화 기법들은 모두 이 요구조건을 충족합니다.

## 동기화 기법들

동기화를 구현하는 다양한 기법들이 존재합니다.

- 소프트웨어 기반 해결책: 알고리즘이 상호 배제를 보장하기 위해 운영체제나 특정 하드웨어 명령어의 특별한 지원을 포함하지 않는 방법)
  - Peterson's Solution: 임계 구역에 대한 고전적인 소프트웨어 기반 해결책, 현대 컴퓨터 구조에서 올바르게 실행됨을 보장하지 않음, 이론적으로 임계구역 문제의 세가지 요구조건을 충족하는 소프트웨어 설계시 필요한 복잡성을 잘 설명하는 기법 (https://dailyheumsi.tistory.com/132)
- 하드웨어 기반 해결책: 운영체제나 특정 하드웨어 명령어의 특별한 지원을 활용하는 방법
  - 메모리 장벽
  - 하드웨어 명령어(test_and_set(), compare_and_swap())
  - 원자적 변수
- Mutex Locks: 응용 프로그래머가 사용할 수 있도록 운영체제 설계자들이 제공하는 상위 수준 소프트웨어 도구 중 가장 간단한 형태.
- Semaphore: mutex와 유사하지만 프로세스들이 자신의 행동을 더 정교하게 동기화 할 수 있는 방법을 제공하는 도구
- Monitor