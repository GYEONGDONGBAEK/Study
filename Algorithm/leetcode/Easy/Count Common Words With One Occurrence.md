# [leetcode] 2085. Count Common Words With One Occurrence

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/count-common-words-with-one-occurrence/description/)

## 문제 설명:

Given two string arrays `words1` and `words2`, return *the number of strings that appear **exactly once** in **each** of the two arrays.*

**Example 1:**

```
Input: words1 = ["leetcode","is","amazing","as","is"], words2 = ["amazing","leetcode","is"]
Output: 2
Explanation:
- "leetcode" appears exactly once in each of the two arrays. We count this string.
- "amazing" appears exactly once in each of the two arrays. We count this string.
- "is" appears in each of the two arrays, but there are 2 occurrences of it in words1. We do not count this string.
- "as" appears once in words1, but does not appear in words2. We do not count this string.
Thus, there are 2 strings that appear exactly once in each of the two arrays.

```

**Example 2:**

```
Input: words1 = ["b","bb","bbb"], words2 = ["a","aa","aaa"]
Output: 0
Explanation: There are no strings that appear in each of the two arrays.

```

**Example 3:**

```
Input: words1 = ["a","ab"], words2 = ["a","a","a","ab"]
Output: 1
Explanation: The only string that appears exactly once in each of the two arrays is "ab".

```

**Constraints:**

- `1 <= words1.length, words2.length <= 1000`
- `1 <= words1[i].length, words2[j].length <= 30`
- `words1[i]` and `words2[j]` consists only of lowercase English letters.

## 문제 풀이:

```java
class Solution {
    public int countWords(String[] words1, String[] words2) {
        HashMap<String,Integer> hm1 = new HashMap<>();
        HashMap<String,Integer> hm2 = new HashMap<>();
        int ans=0;
        for(String word : words1) {
            hm1.put(word, hm1.getOrDefault(word, 0) + 1);
        }
        for(String word : words2){
            hm2.put(word, hm2.getOrDefault(word, 0) + 1);
        }
        for(String s : hm1.keySet()){
            if(hm2.containsKey(s) && hm2.get(s)==1 && hm1.get(s)==1){
                ans++;
            }
        }
        return ans;
    }
}
----------------------------------------------------------
Runtime
6 ms
Beats
65.26%
Memory
43 MB
Beats
74.74%
```

### **문제 풀이 해석:**

Map을 사용해서 풀었다. words1과 words2를 순회하면서 word를 getOrDefault 메서드를 사용해서 Key가 존재한다면 value를 1증가시키고 아니라면 그 Key에 대한 Value값을 1로 설정해주었다. 그리고 keySet을 사용해서 그 Key에 대해 hm2에 그 키가 존재하고 둘다 Value가 1일때 ans를 1씩 증가시키는 방법을 사용했다.