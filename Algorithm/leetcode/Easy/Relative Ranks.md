# [leetcode] 506. Relative Ranks

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/relative-ranks/description/)

## 문제 설명:

You are given an integer array `score` of size `n`, where `score[i]` is the score of the `ith` athlete in a competition. All the scores are guaranteed to be **unique**.

The athletes are **placed** based on their scores, where the `1st` place athlete has the highest score, the `2nd` place athlete has the `2nd` highest score, and so on. The placement of each athlete determines their rank:

- The `1st` place athlete's rank is `"Gold Medal"`.
- The `2nd` place athlete's rank is `"Silver Medal"`.
- The `3rd` place athlete's rank is `"Bronze Medal"`.
- For the `4th` place to the `nth` place athlete, their rank is their placement number (i.e., the `xth` place athlete's rank is `"x"`).

Return an array `answer` of size `n` where `answer[i]` is the **rank** of the `ith` athlete.

**Example 1:**

```
Input: score = [5,4,3,2,1]
Output: ["Gold Medal","Silver Medal","Bronze Medal","4","5"]
Explanation: The placements are [1st, 2nd, 3rd, 4th, 5th].
```

**Example 2:**

```
Input: score = [10,3,8,9,4]
Output: ["Gold Medal","5","Bronze Medal","Silver Medal","4"]
Explanation: The placements are [1st, 5th, 3rd, 2nd, 4th].

```

**Constraints:**

- `n == score.length`
- `1 <= n <= 104`
- `0 <= score[i] <= 106`
- All the values in `score` are **unique**.

## 문제 풀이:

```java
class Solution {
    public String[] findRelativeRanks(int[] score) {
        int n = score.length;
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0; i<n; i++){
            pq.add(score[i]);
        }
        int cnt=1;
        while(pq.size()>0){
            map.put(pq.poll(),cnt++);
        }
        String[] ans = new String[n];

        for (int i = 0; i < n; i++) {
            int rank= map.get(score[i]);
            if (rank == 1) {
                ans[i] = "Gold Medal";
            } else if (rank == 2) {
                ans[i] = "Silver Medal";
            } else if (rank == 3) {
                ans[i] = "Bronze Medal";
            } else {
                ans[i] = String.valueOf(rank);
            }
        }

        return ans;
    }
}
----------------------------------------------------------
Runtime
9 ms
Beats
53.64%
Memory
44.6 MB
Beats
76.38%
```

### **문제 풀이 해석:**

Map과 PriorityQueue로 풀었다. reverseorder를 사용해서 내림차순으로 정렬한 후 , 그 값 순서대로 Map에 1 ,2, 3, …순서로 넣었다. 이 후 반복문을 순회하면서 ans배열에 맞게 처리하였다.