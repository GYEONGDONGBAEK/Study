# [leetcode] 2255. Count Prefixes of a Given String

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/count-prefixes-of-a-given-string/)

## 문제 설명:

You are given a string array `words` and a string `s`, where `words[i]` and `s` comprise only of **lowercase English letters**.

Return *the **number of strings** in* `words` *that are a **prefix** of* `s`.

A **prefix** of a string is a substring that occurs at the beginning of the string. A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

```
Input: words = ["a","b","c","ab","bc","abc"], s = "abc"
Output: 3
Explanation:
The strings in words which are a prefix of s = "abc" are:
"a", "ab", and "abc".
Thus the number of strings in words which are a prefix of s is 3.
```

**Example 2:**

```
Input: words = ["a","a"], s = "aa"
Output: 2
Explanation:
Both of the strings are a prefix of s.
Note that the same string can occur multiple times in words, and it should be counted each time.
```

**Constraints:**

- `1 <= words.length <= 1000`
- `1 <= words[i].length, s.length <= 10`
- `words[i]` and `s` consist of lowercase English letters **only**.

## 문제 풀이:

```java
class Solution {
    public int countPrefixes(String[] words, String s) {
        int cnt = 0;

        for (String word : words) {
            if (s.startsWith(word)) {
                cnt++;
            }
        }

        return cnt;
    }
}
----------------------------------------------------------
Runtime
0 ms
Beats
100%
Memory
43.8 MB
Beats
19.39%
```

### **문제 풀이 해석:**

startsWith 메서드를 사용해서 풀었다.