# [leetcode] 1743. Restore the Array From Adjacent Pairs

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs/description/)

## 문제 설명:

There is an integer array `nums` that consists of `n` **unique** elements, but you have forgotten it. However, you do remember every pair of adjacent elements in `nums`.

You are given a 2D integer array `adjacentPairs` of size `n - 1` where each `adjacentPairs[i] = [ui, vi]` indicates that the elements `ui` and `vi` are adjacent in `nums`.

It is guaranteed that every adjacent pair of elements `nums[i]` and `nums[i+1]` will exist in `adjacentPairs`, either as `[nums[i], nums[i+1]]` or `[nums[i+1], nums[i]]`. The pairs can appear **in any order**.

Return *the original array* `nums`*. If there are multiple solutions, return **any of them***.

**Example 1:**

```
Input: adjacentPairs = [[2,1],[3,4],[3,2]]
Output: [1,2,3,4]
Explanation: This array has all its adjacent pairs in adjacentPairs.
Notice that adjacentPairs[i] may not be in left-to-right order.

```

**Example 2:**

```
Input: adjacentPairs = [[4,-2],[1,4],[-3,1]]
Output: [-2,4,1,-3]
Explanation: There can be negative numbers.
Another solution is [-3,1,4,-2], which would also be accepted.

```

**Example 3:**

```
Input: adjacentPairs = [[100000,-100000]]
Output: [100000,-100000]

```

**Constraints:**

- `nums.length == n`
- `adjacentPairs.length == n - 1`
- `adjacentPairs[i].length == 2`
- `2 <= n <= 105`
- `105 <= nums[i], ui, vi <= 105`
- There exists some `nums` that has `adjacentPairs` as its pairs.

## 문제 풀이:

```java
class Solution {
    public int[] restoreArray(int[][] adjacentPairs) {
        Map<Integer, List<Integer>> map = new HashMap<>();

        for (int[] pair : adjacentPairs) {
            
            map.computeIfAbsent(pair[0], k -> new ArrayList<>()).add(pair[1]);
            map.computeIfAbsent(pair[1], k -> new ArrayList<>()).add(pair[0]);
        }
        int n = adjacentPairs.length + 1;
        int[] ans = new int[n];

        for (Map.Entry<Integer, List<Integer>> entry : map.entrySet()) {
            if (entry.getValue().size() == 1) {
                ans[0] = entry.getKey();
                break;
            }
        }

        ans[1] = map.get(ans[0]).get(0);

        for (int i = 2; i < n; i++) {
            List<Integer> neighbors = map.get(ans[i - 1]);
            ans[i] = ans[i - 2] == neighbors.get(0) ? neighbors.get(1) : neighbors.get(0);
        }

        return ans;
    }
}
----------------------------------------------------------
Runtime
57 ms
Beats
91.99%
Memory
77.7 MB
Beats
97.63%
```

### **문제 풀이 해석:**

Map을 이용하여 풀었다. 반복문을 돌면서 computeIfAbsent을 사용하여 Map에 값을 저장하였다.Map에 값은 {1=[2], 2=[1, 3], 3=[4, 2], 4=[3]} 저장된다. 이 후 Map에 한번만 나오는 값을 출발점으로 설정하고, 그 값의 Value를 ans[1]로 설정하고 나머지 연산을 해주었다. 

computeIfAbsent메서드:특정 키에 대한 값이 없을 때 새로운 값을 계산하고 맵에 추가합니다. 이 메서드는 다음과 같이 정의