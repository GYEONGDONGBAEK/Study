# [leetcode] 2185. Counting Words With a Given Prefix

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/counting-words-with-a-given-prefix/)

## 문제 설명:

You are given an array of strings `words` and a string `pref`.

Return *the number of strings in* `words` *that contain* `pref` *as a **prefix***.

A **prefix** of a string `s` is any leading contiguous substring of `s`.

**Example 1:**

```
Input: words = ["pay","attention","practice","attend"],pref= "at"
Output: 2
Explanation: The 2 strings that contain "at" as a prefix are: "attention" and "attend".

```

**Example 2:**

```
Input: words = ["leetcode","win","loops","success"],pref= "code"
Output: 0
Explanation: There are no strings that contain "code" as a prefix.

```

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length, pref.length <= 100`
- `words[i]` and `pref` consist of lowercase English letters.

## 문제 풀이:

```java
class Solution {
    public int prefixCount(String[] words, String pref) {
        int ans=0;
        int cnt=pref.length();
        for(String word: words){
            if(word.length() >= cnt && word.substring(0,cnt).equals(pref)) ans++;
        }
        return ans;
    }
}
----------------------------------------------------------
Runtime
1 ms
Beats
47.48%
Memory
43.1 MB
Beats
19.70%
```

### **문제 풀이 해석:**

pref의 길이만큼의 cnt 변수를 설정한 후 for문을 돌면서 if문에 cnt는 word의 length 보다 작거나 같을때와 word를 cnt만큼 substring한 값이 pref와 같을때마다 ans를 올렸다. 만약 cnt가 word의 length보다 작다는 조건이 없으면 만약 words의 원소중 cnt의 길이보다 작은 원소가 있다면, IndexOutOfBoundsException 에러가 나기때문에 조건을 추가해주어야 한다.