# [leetcode] 1700. Number of Students Unable to Eat Lunch

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch/description/)

## 문제 설명:

The school cafeteria offers circular and square sandwiches at lunch break, referred to by numbers `0` and `1` respectively. All students stand in a queue. Each student either prefers square or circular sandwiches.

The number of sandwiches in the cafeteria is equal to the number of students. The sandwiches are placed in a **stack**. At each step:

- If the student at the front of the queue **prefers** the sandwich on the top of the stack, they will **take it** and leave the queue.
- Otherwise, they will **leave it** and go to the queue's end.

This continues until none of the queue students want to take the top sandwich and are thus unable to eat.

You are given two integer arrays `students` and `sandwiches` where `sandwiches[i]` is the type of the `ith` sandwich in the stack (`i = 0` is the top of the stack) and `students[j]` is the preference of the `jth` student in the initial queue (`j = 0` is the front of the queue). Return *the number of students that are unable to eat.*

**Example 1:**

```
Input: students = [1,1,0,0], sandwiches = [0,1,0,1]
Output: 0
Explanation:
- Front student leaves the top sandwich and returns to the end of the line making students = [1,0,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,0,1,1].
- Front student takes the top sandwich and leaves the line making students = [0,1,1] and sandwiches = [1,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [1,1,0].
- Front student takes the top sandwich and leaves the line making students = [1,0] and sandwiches = [0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,1].
- Front student takes the top sandwich and leaves the line making students = [1] and sandwiches = [1].
- Front student takes the top sandwich and leaves the line making students = [] and sandwiches = [].
Hence all students are able to eat.

```

**Example 2:**

```
Input: students = [1,1,1,0,0,1], sandwiches = [1,0,0,0,1,1]
Output: 3

```

**Constraints:**

- `1 <= students.length, sandwiches.length <= 100`
- `students.length == sandwiches.length`
- `sandwiches[i]` is `0` or `1`.
- `students[i]` is `0` or `1`.

Accepted

**86.9K**

Submissions

**123.5K**

Acceptance Rate

**70.4%**

## 문제 풀이:

```java
class Solution {
    public int countStudents(int[] students, int[] sandwiches) {
        Stack<Integer> st = new Stack<>();
        Queue<Integer> q = new LinkedList<>();

        for (int i = 0; i < students.length; i++) {
            st.push(sandwiches[sandwiches.length - i - 1]);
            q.offer(students[i]);
        }

        int cnt = 0;
        while (true) {
            if (st.peek() == q.peek()) {
                cnt = 0;
                st.pop();
                q.poll();
            } else {
                cnt++;
                q.offer(q.poll());
            }

            if (cnt == q.size()) {
                break;
            }
        }

        return cnt;
    }
}
----------------------------------------------------------
Runtime
2 ms
Beats
52.44%
Memory
41.1 MB
Beats
11.73%
```

### **문제 풀이 해석:**

Queue와 Stack을 사용해서 풀었다. 샌드위치를 stack에 넣고, 학생을 queue에 넣었다. 이 후 While문을 반복하면서, 학생이 선호하는 샌드위치라면 st과 q에서 둘다 값을 제거하고, 만약 아니라면 학생을 다시 queue에 넣는다. 만약 cnt와 q.size가 같아지는 지점이 온다면, 그 학생들은 모두 샌드위치를 못먹는 학생이 되기때문에 break를 하고 그 때의 cnt를 리턴한다. 만약 break를 하지 않으면 계속 반복되어 time limited exception이 발생한다.