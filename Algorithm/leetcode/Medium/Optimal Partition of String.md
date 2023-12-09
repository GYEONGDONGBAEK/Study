# [leetcode] 2405. Optimal Partition of String

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/optimal-partition-of-string/description/)

## 문제 설명:

Given a string `s`, partition the string into one or more **substrings** such that the characters in each substring are **unique**. That is, no letter appears in a single substring more than **once**.

Return *the **minimum** number of substrings in such a partition.*

Note that each character should belong to exactly one substring in a partition.

**Example 1:**

```
Input: s = "abacaba"
Output: 4
Explanation:
Two possible partitions are ("a","ba","cab","a") and ("ab","a","ca","ba").
It can be shown that 4 is the minimum number of substrings needed.

```

**Example 2:**

```
Input: s = "ssssss"
Output: 6
Explanation:
The only valid partition is ("s","s","s","s","s","s").

```

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of only English lowercase letters.

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public int partitionString(String s) {
        HashSet<Character> set = new HashSet<>();
        int cnt = 1;
        for(char ch : s.toCharArray()){
            boolean flag = set.add(ch);
            if(!flag){
                cnt++;
                set.clear();
                set.add(ch);
            }  
        }
        return cnt;
    }
}
----------------------------------------------------------
Runtime
26 ms
Beats
67.90%
Memory
44.9 MB
Beats
13.6%
```

### **문제 풀이 해석:**

set을 사용하였고, flag 라는 boolean 변수를 사용하여 set에 add를 시켜주었다. 만약 flag가 false가 된다면 add가 실패하는것이고, 즉 똑같은 알파벳이 들어온 것이기 때문에, cnt를 1 늘려주고 set을 초기화시키고 ch를 다시 set에 추가하는 방법을 사용했다.