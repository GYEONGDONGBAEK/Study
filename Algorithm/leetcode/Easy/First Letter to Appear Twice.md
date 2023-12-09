# [leetcode] 2351. First Letter to Appear Twice

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/first-letter-to-appear-twice/description/)

## 문제 설명:

Given a string `s` consisting of lowercase English letters, return *the first letter to appear **twice***.

**Note**:

- A letter `a` appears twice before another letter `b` if the **second** occurrence of `a` is before the **second** occurrence of `b`.
- `s` will contain at least one letter that appears twice.

**Example 1:**

```
Input: s = "abccbaacz"
Output: "c"
Explanation:
The letter 'a' appears on the indexes 0, 5 and 6.
The letter 'b' appears on the indexes 1 and 4.
The letter 'c' appears on the indexes 2, 3 and 7.
The letter 'z' appears on the index 8.
The letter 'c' is the first letter to appear twice, because out of all the letters the index of its second occurrence is the smallest.

```

**Example 2:**

```
Input: s = "abcdd"
Output: "d"
Explanation:
The only letter that appears twice is 'd' so we return 'd'.

```

**Constraints:**

- `2 <= s.length <= 100`
- `s` consists of lowercase English letters.
- `s` has at least one repeated letter.

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public char repeatedCharacter(String s) {
        HashSet<Character> set=new HashSet<>();
        for(char c:s.toCharArray()){
            if(!set.add(c)) return c;
        }
        return ' ';
    }
}
----------------------------------------------------------
Runtime
0 ms
Beats
100%
Memory
40.6 MB
Beats
40.2%
```

### **문제 풀이 해석:**

Set을 이용해서 풀었다. set에 add가 안된다면 그 값이 이미 set에 존재하는 것이기 때문에 그때의 문자값을 리턴시켰다.