# [leetcode] 946. Validate Stack Sequences

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/validate-stack-sequences/)

## 문제 설명:

Given two integer arrays `pushed` and `popped` each with distinct values, return `true` *if this could have been the result of a sequence of push and pop operations on an initially empty stack, or* `false` *otherwise.*

**Example 1:**

```
Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
Output: true
Explanation: We might do the following sequence:
push(1), push(2), push(3), push(4),
pop() -> 4,
push(5),
pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1

```

**Example 2:**

```
Input: pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
Output: false
Explanation: 1 cannot be popped before 2.

```

**Constraints:**

- `1 <= pushed.length <= 1000`
- `0 <= pushed[i] <= 1000`
- All the elements of `pushed` are **unique**.
- `popped.length == pushed.length`
- `popped` is a permutation of `pushed`.

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Stack<Integer> st=new Stack<>();
        int poppedcnt=0;
        for(int i=0;i<pushed.length;i++){
            st.push(pushed[i]);
            while(!st.isEmpty()&&st.peek()==popped[poppedcnt]){
                st.pop();
                poppedcnt++;
            }
        }
        return st.isEmpty();
    }
}
----------------------------------------------------------
Runtime
3 ms
Beats
19.45%
Memory
43.3 MB
Beats
24.4%
```

### **문제 풀이 해석:**

Stack을 사용하였고, pushed 배열을 순회하면서 스택에 push 하고 만약 st의 peek가 popped 배열의 원소와 같다면 pop을 해주면서 poppedcnt의 값을 1 증가시켰다. 반환할때 스택이 비어있다면 true, 비어있지 않다면 false를 리턴하는 방법으로 풀었다.