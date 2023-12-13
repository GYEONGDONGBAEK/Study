# [leetcode] 2206. Divide Array Into Equal Pairs

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/divide-array-into-equal-pairs/description/)

## 문제 설명:

You are given an integer array `nums` consisting of `2 * n` integers.

You need to divide `nums` into `n` pairs such that:

- Each element belongs to **exactly one** pair.
- The elements present in a pair are **equal**.

Return `true` *if nums can be divided into* `n` *pairs, otherwise return* `false`.

**Example 1:**

```
Input: nums = [3,2,3,2,2,2]
Output: true
Explanation:
There are 6 elements in nums, so they should be divided into 6 / 2 = 3 pairs.
If nums is divided into the pairs (2, 2), (3, 3), and (2, 2), it will satisfy all the conditions.

```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: false
Explanation:
There is no way to divide nums into 4 / 2 = 2 pairs such that the pairs satisfy every condition.

```

**Constraints:**

- `nums.length == 2 * n`
- `1 <= n <= 500`
- `1 <= nums[i] <= 500`

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public boolean divideArray(int[] nums) {
        HashMap<Integer,Integer> hm=new HashMap<>();
        for (int num : nums) {
            hm.put(num, hm.getOrDefault(num, 0) + 1);
        }
        for(int cnt:hm.keySet()){
            if(hm.get(cnt)%2 != 0) return false;
        }

        return true;
    }
}
----------------------------------------------------------
Runtime
8 ms
Beats
33.53%
Memory
43.5 MB
Beats
39.75%
```

### **문제 풀이 해석:**

HashMap을 이용해서 풀었다. getOrDefault 메서드를 써서 key가 이미 존재한다면 그 key에 대한 value를 1 증가시키고, 존재하지 않는다면 새롭게 map에 넣는 방식을 사용했고, keySet을 돌면서 value가 짝수가 아니라면 false를 리턴하도록 했다.