# [leetcode] 1249. Minimum Remove to Make Valid Parentheses

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description/)

## 문제 설명:

Given a string s of `'('` , `')'` and lowercase English characters.

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting *parentheses string* is valid and return **any** valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

**Example 1:**

```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.

```

**Example 2:**

```
Input: s = "a)b(c)d"
Output: "ab(c)d"

```

**Example 3:**

```
Input: s = "))(("
Output: ""
Explanation: An empty string is also valid.

```

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is either`'('` , `')'`, or lowercase English letter`.`

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public String minRemoveToMakeValid(String s) {
        Stack<Integer> st = new Stack<>();
        boolean[] flag = new boolean[s.length()];

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch == '(') {
                st.push(i);
            } else if (ch == ')') {
                if (!st.isEmpty()) {
                    st.pop();
                } else {
                    flag[i] = true;
                }
            }
        }

        while (!st.isEmpty()) {
            flag[st.pop()] = true;
        }

        StringBuilder ans = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (!flag[i]) {
                ans.append(s.charAt(i));
            }
        }

        return ans.toString();
    }
----------------------------------------------------------
Runtime
18 ms
Beats
71.12%
Memory
44.6 MB
Beats
32.32%
```

### **문제 풀이 해석:**

문제를 완벽히 이해하진 못했는데, 괄호의 모양이 정상적이거나, 정상적이면서 괄호안에 알파벳이 들어가있게 만들기 위해 최소한의 괄호모양을 제거하는걸로 생각했다.

Stack을 이용해서 풀었고, flag라는 boolean 배열을 s의 길이만큼 생성해서 s를 돌면서 괄호 모양을 stack에 넣고, 만약 괄호의 모양이 정상적이지 않다면 true로 바꾼 후 , StringBuilder를 이용해 boolean의 값이 true일때 빼고, 모든 값을 넣어준 후 toString으로 변환했다.