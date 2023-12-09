# [leetcode] 1944. Number of Visible People in a Queue

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/number-of-visible-people-in-a-queue/description/)

## 문제 설명:

There are `n` people standing in a queue, and they numbered from `0` to `n - 1` in **left to right** order. You are given an array `heights` of **distinct** integers where `heights[i]` represents the height of the `ith` person.

A person can **see** another person to their right in the queue if everybody in between is **shorter** than both of them. More formally, the `ith` person can see the `jth` person if `i < j` and `min(heights[i], heights[j]) > max(heights[i+1], heights[i+2], ..., heights[j-1])`.

Return *an array* `answer` *of length* `n` *where* `answer[i]` *is the **number of people** the* `ith` *person can **see** to their right in the queue*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/05/29/queue-plane.jpg](https://assets.leetcode.com/uploads/2021/05/29/queue-plane.jpg)

```
Input: heights = [10,6,8,5,11,9]
Output: [3,1,2,1,1,0]
Explanation:
Person 0 can see person 1, 2, and 4.
Person 1 can see person 2.
Person 2 can see person 3 and 4.
Person 3 can see person 4.
Person 4 can see person 5.
Person 5 can see no one since nobody is to the right of them.

```

**Example 2:**

```
Input: heights = [5,1,2,3,10]
Output: [4,1,1,1,0]

```

**Constraints:**

- `n == heights.length`
- `1 <= n <= 105`
- `1 <= heights[i] <= 105`
- All the values of `heights` are **unique**.

## 문제 풀이:

```java
class Solution {
    public int[] canSeePersonsCount(int[] heights) {
        Stack<Integer> st = new Stack<>();        
        int ans[] = new int[heights.length];      
        for(int i = heights.length - 1; i >= 0; i--) {
            int vis = 0;        
            while(!st.isEmpty() && heights[i] > st.peek()) {
                st.pop();
                vis++;
            }            
            if(!st.isEmpty()) {
                vis++;
            }            
            st.push(heights[i]);            
            ans[i] = vis;
        }        
        return ans;
    }
}
----------------------------------------------------------
Runtime
50 ms
Beats
71.36%
Memory
60.5 MB
Beats
12.14%
```

### **문제 풀이 해석:**

Stack을 이용해서 풀었다. 배열의 맨 끝에서부터 순회하면서, 스택이 비어있지 않거나, 배열의 인덱스가 peek보다 크다면 스택에 들어있는 값을 pop 하고 vis를 1씩 증가시켰다. 그리고 스택이 비어있지 않으면 vis를 1씩 증가시켰다.

인덱스의 값을 스택에 푸쉬하고 그 인덱스의 vis값을 정답배열로 반환했다.