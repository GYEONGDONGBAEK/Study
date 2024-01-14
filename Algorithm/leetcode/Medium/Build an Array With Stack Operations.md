# [leetcode] 1441. Build an Array With Stack Operations

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/build-an-array-with-stack-operations/description/)

## 문제 설명:

You are given an integer array `target` and an integer `n`.

You have an empty stack with the two following operations:

- **`"Push"`**: pushes an integer to the top of the stack.
- **`"Pop"`**: removes the integer on the top of the stack.

You also have a stream of the integers in the range `[1, n]`.

Use the two stack operations to make the numbers in the stack (from the bottom to the top) equal to `target`. You should follow the following rules:

- If the stream of the integers is not empty, pick the next integer from the stream and push it to the top of the stack.
- If the stack is not empty, pop the integer at the top of the stack.
- If, at any moment, the elements in the stack (from the bottom to the top) are equal to `target`, do not read new integers from the stream and do not do more operations on the stack.

Return *the stack operations needed to build* `target` following the mentioned rules. If there are multiple valid answers, return **any of them**.

**Example 1:**

```
Input: target = [1,3], n = 3
Output: ["Push","Push","Pop","Push"]
Explanation: Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Pop the integer on the top of the stack. s = [1].
Read 3 from the stream and push it to the stack. s = [1,3].

```

**Example 2:**

```
Input: target = [1,2,3], n = 3
Output: ["Push","Push","Push"]
Explanation: Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Read 3 from the stream and push it to the stack. s = [1,2,3].

```

**Example 3:**

```
Input: target = [1,2], n = 4
Output: ["Push","Push"]
Explanation: Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Since the stack (from the bottom to the top) is equal to target, we stop the stack operations.
The answers that read integer 3 from the stream are not accepted.

```

**Constraints:**

- `1 <= target.length <= 100`
- `1 <= n <= 100`
- `1 <= target[i] <= n`
- `target` is strictly increasing.

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public List<String> buildArray(int[] target, int n) {
        List<String> list=new ArrayList<>();
        int current=1;
        int index=0;
        while(current<=n && index< target.length){
            int num= target[index];
            if(num == current){
                list.add("Push");
                current++;
                index++;
            } else{
                list.add("Push");
                list.add("Pop");
                current++;
            }
        }
        return list;
    }
}
----------------------------------------------------------
Runtime
1 ms
Beats
15.75%
Memory
42.6 MB
Beats
9.30%
```

### **문제 풀이 해석:**

우리가 만들어야 할 배열이 target으로 주어지고 범위의 값인 n이 주어진다. 배열의 크기를 알 수 없고, 반환값이 list이기 때문에 ArrayList를 선언해주었다. 이 후 현재 값을 1로 설정하고 while문을 순회하면서, 만약 현재의 값이 target에 존재한다면 list에 Push을 add 한 후 현재의 값과 인덱스 값을 모두 올리고, 만약 현재의 값이 target에 존재하지 않는다면 Push와 Pop을 add 한 후 현재의 값만 올리면 된다. 이 후 list를 리턴하면 된다.