# [leetcode] 1550. Three Consecutive Odds

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/three-consecutive-odds/)

## 문제 설명:

Given an integer array

```
arr
```

, return

```
true
```

if there are three consecutive odd numbers in the array. Otherwise, return

```
false
```

.

**Example 1:**

```
Input: arr = [2,6,4,1]
Output: false
Explanation: There are no three consecutive odds.

```

**Example 2:**

```
Input: arr = [1,2,34,3,4,5,7,23,12]
Output: true
Explanation: [5,7,23] are three consecutive odds.

```

**Constraints:**

- `1 <= arr.length <= 1000`
- `1 <= arr[i] <= 1000`

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public boolean threeConsecutiveOdds(int[] arr) {
        int cnt = 0;

        for (int num : arr) {
            if (num % 2 != 0) {
                cnt++;
                if (cnt == 3) {
                    return true;
                }
            } else {
                cnt = 0;
            }
        }

        return false;
    }
}
----------------------------------------------------------
Runtime
0 ms
Beats
100%
Memory
41.4 MB
Beats
28.98%
```

### **문제 풀이 해석:**

카운트를 셀 cnt 변수를 설정하고 arr을 순회하면서 num이 짝수가 아니라면 cnt를 1씩 올려주고 아니라면 0으로 초기화 시켜주었다. 만약 cnt가 3이 된다면 true를 반환하도록 했다.