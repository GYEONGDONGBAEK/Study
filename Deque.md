# Deque (Double Ended Queue)


## ****Deque****

- 큐의 양쪽으로 엘리먼트의 삽입과 삭제를 수행할 수 있는 자료구조를 의미
- 덱(Deque)은 어떤 쪽으로 입력하고 어떤 쪽으로 출력하느냐에 따라서 스택(Stack)으로 사용할 수도 있고, 큐(Queue)로도 사용할 수 있다.
- 한쪽으로만 입력 가능하도록 설정한 덱을 스크롤(scroll)이라고 하며, 한쪽으로만 출력 가능하도록 설정한 덱을 셸프(shelf)라고 한다.

---

### ****Deque에 값 삽입****

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/ebdd1a12-4590-4e4a-a867-c3d5752611fc">

- add(): 마지막에 원소 삽입용량 초과 시 예외 발생
- addFirst(): 맨 앞에 원소 삽입용량 초과 시 예외 발생
- addLast(): 마지막에 원소 삽입용량 초과 시 예외 발생
- offer(): 마지막에 원소 삽입삽입 성공 시 true, 용량 제한에 걸리는 경우 false 반환
- offerFirst(): 맨 앞에 원소 삽입삽입 성공 시 true, 용량 제한에 걸리는 경우 false 반환
- offerLast(): 마지막에 원소 삽입삽입 성공 시 true, 용량 제한에 걸리는 경우 false 반환

### Deque 값 삭제

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/43f71a2e-afea-4b65-bd8b-44a1f20b3451">

- remove(): 맨 앞의 원소 제거 후 해당 원소를 리턴덱이 비어있는 경우 예외 발생
- removeFirst(): 맨 앞의 원소 제거 후 해당 원소를 리턴덱이 비어있는 경우 예외 발생
- removeLast(): 마지막 원소 제거 후 해당 원소를 리턴덱이 비어있는 경우 예외 발생
- poll: 맨 앞의 원소 제거 후 해당 원소를 리턴덱이 비어있는 경우 null 리턴
- pollFirst(): 맨 앞의 원소 제거 후 해당 원소를 리턴덱이 비어있는 경우 null 리턴
- pollLast(): 마지막 원소 제거 후 해당 원소를 리턴덱이 비어있는 경우 null 리턴

### Deque 원소 확인

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/43f71a2e-afea-4b65-bd8b-44a1f20b3451">

- getFirst(): 맨 앞의 원소를 리턴덱이 비어있는 경우 예외 발생
- getLast(): 마지막 원소를 리턴덱이 비어있는 경우 예외 발생
- peek(): 맨 앞의 원소를 리턴덱이 비어있는 경우 null 리턴
- peekFirst(): 맨 앞의 원소를 리턴덱이 비어있는 경우 null 리턴
- peekLast(): 마지막 원소를 리턴덱이 비어있는 경우 null 리턴

### **기타**

- removeFirstOccurrence(x): 덱의 맨 앞부터 탐색하여 x와 동일한 첫 원소를 제거동일한 원소가 없을 시 덱이 변경되지 않음
- removeLastOccurrence(x): 덱의 마지막부터 탐색하여 x와 동일한 첫 원소를 제거동일한 원소가 없을 시 덱이 변경되지 않음
- element(): removeFirst() 와 동일
- addFirst() : push() 와 동일
- removeFirst(): pop() 과 동일
- remove(x): removeFirstOccurrence(x)와 동일
- contains(x):덱에 x와 동일한 원소가 있는지 true 혹은 false 반환
- size(): 덱의 원소 개수 리턴
- iterator(): 덱의 반복자(iterator) 반환
- isEmpty(): 덱이 비어있는지 true 혹은 false 반환