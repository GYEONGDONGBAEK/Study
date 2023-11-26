# [자료구조] PriorityQueue

---

# Priority Queue

PriorityQueue란 우선순위 큐로써 일반적인 큐의 구조 FIFO(First In First Out)를 가지면서, 데이터가 들어온 순서대로 데이터가 나가는 것이 아닌 우선순위를 먼저 결정하고 그 우선순위가 높은 데이터가 먼저 나가는 자료구조이다.

PriorityQueue를 사용하기 위해선 우선순위 큐에 저장할 객체는 필수적으로 Comparable Interface를 구현해야한다.

Comparable Interface를 구현하면 compareTo method를 override 하게 되고 해당 객체에서 처리할 우선순위 조건을 리턴해주면 PriorityQueue 가 알아서 우선순위가 높은 객체를 추출 해준다.

PriorityQueue는 Heap을 이용하여 구현하는 것이 일반적이다.

데이터를 삽입할 때 우선순위를 기준으로 최대 힙 혹은 최소 힙을 구성하고 데이터를 꺼낼 때 루트 노드를 얻어낸 뒤 루트 노드를 ****삭제할 때는 빈 루트 노드 위치에 맨 마지막 노드를 삽입한 후 아래로 내려가면서 적절한 자리를 찾아 옮기는 방식으로 진행된다.

## Priority Queue 선언

Priority Queue를 사용하려면 java.util.PriorityQueue를 import해야 한다.

```java
import java.util.PriorityQueue;
import java.util.Collections;

//낮은 숫자가 우선 순위인 int 형 우선순위 큐 선언
PriorityQueue<Integer> priorityQueueLowest = new PriorityQueue<>();

//높은 숫자가 우선 순위인 int 형 우선순위 큐 선언
PriorityQueue<Integer> priorityQueueHighest = new PriorityQueue<>(Collections.reverseOrder());
```

## Priority Queue 동작

### Priority Queue Add

```java
// add(value) 메서드의 경우 만약 삽입에 성공하면 true를 반환,
// 큐에 여유 공간이 없어 삽입에 실패하면 IllegalStateException을 발생
priorityQueueLowest.add(1);
priorityQueueLowest.add(10);
priorityQueueLowest.offer(100);

priorityQueueHighest.add(1);
priorityQueueHighest.add(10);
priorityQueueHighest.offer(100);
```

`Priority Queue`에 삽입이 실행되면 아래와 같은 구조로 데이터의 삽입이 이루어 진다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/51f80b2b-a953-44f2-bf6c-267a684c8d79">

### Priority Queue remove

```java
// 첫번째 값을 반환하고 제거 비어있다면 null
priorityQueueLowest.poll();

// 첫번째 값 제거 비어있다면 예외 발생
priorityQueueLowest.remove();

// 첫번째 값을 반환만 하고 제거 하지는 않는다.
// 큐가 비어있다면 null을 반환
priorityQueueLowest.peek();

// 첫번째 값을 반환만 하고 제거 하지는 않는다.
// 큐가 비어있다면 예외 발생
priorityQueueLowest.element();

// 초기화
priorityQueueLowest.clear();
```

`Priority Queue`에 삭제는 아래와 같은 구조로 이루어 진다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/80dd767d-4023-43fd-8d26-cf313a5a840e">