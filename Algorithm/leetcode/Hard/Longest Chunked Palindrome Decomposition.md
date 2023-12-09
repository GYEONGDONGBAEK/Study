# [leetcode] 1147. Longest Chunked Palindrome Decomposition

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/longest-chunked-palindrome-decomposition/description/)

## 문제 설명:

You are given a string `text`. You should split it to k substrings `(subtext1, subtext2, ..., subtextk)` such that:

- `subtexti` is a **non-empty** string.
- The concatenation of all the substrings is equal to `text` (i.e., `subtext1 + subtext2 + ... + subtextk == text`).
- `subtexti == subtextk - i + 1` for all valid values of `i` (i.e., `1 <= i <= k`).

Return the largest possible value of `k`.

**Example 1:**

```
Input: text = "ghiabcdefhelloadamhelloabcdefghi"
Output: 7
Explanation: We can split the string on "(ghi)(abcdef)(hello)(adam)(hello)(abcdef)(ghi)".

```

**Example 2:**

```
Input: text = "merchant"
Output: 1
Explanation: We can split the string on "(merchant)".

```

**Example 3:**

```
Input: text = "antaprezatepzapreanta"
Output: 11
Explanation: We can split the string on "(a)(nt)(a)(pre)(za)(tep)(za)(pre)(a)(nt)(a)".

```

**Constraints:**

- `1 <= text.length <= 1000`
- `text` consists only of lowercase English characters.

## 문제 풀이:

```java
class Solution {
    public int longestDecomposition(String text) {
        int k = 1;
        StringBuilder sb1 = new StringBuilder();
        StringBuilder sb2 = new StringBuilder();
        for(int i = 0,j = text.length() - 1;j >= 0;i++,--j){
            sb1.append(text.charAt(i));
            sb2.insert(0,text.charAt(j));
            if(sb1.toString().equals(sb2.toString())){
                k += 2;
                sb1.delete(0,sb1.length());
                sb2.delete(0,sb2.length());
            }
        }
        return k / 2;
    }
}
----------------------------------------------------------
Runtime
5 ms
Beats
34.67%
Memory
43.1 MB
Beats
69.33%
```

### **문제 풀이 해석:**

StringBuilder를 사용해 문자열을 처리한 후 , 같다면 k를 2개 증가시키고 문자열을 비운다. 모든 처리가 끝나면 마지막 중간에 한개 남아있는 문자열을 처리하기위해 k에 1을 더해준다, 마지막에 k를 2로 나눈이유는 예를들어 `"ghiabcdefhelloadamhelloabcdefghi"` 의 문자열이 있다고 가정했을때, sb1이 앞에서 ghi였을때, sb2가 뒤에서부터 시작한 ghi가 연산이 한번 되고, 반복문이 문자열을 끝까지 순회하기 때문에 sb1이 뒤에있는 ghi고, sb2가 앞에있는 ghi일때 연산이 한번 더 되기 때문에 마지막에 2로 나누어 주었다.