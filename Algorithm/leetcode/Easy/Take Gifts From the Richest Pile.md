# [leetcode] 2558. Take Gifts From the Richest Pile

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/take-gifts-from-the-richest-pile/description/)

## 문제 설명:

You are given an integer array `gifts` denoting the number of gifts in various piles. Every second, you do the following:

- Choose the pile with the maximum number of gifts.
- If there is more than one pile with the maximum number of gifts, choose any.
- Leave behind the floor of the square root of the number of gifts in the pile. Take the rest of the gifts.

Return *the number of gifts remaining after* `k` *seconds.*

**Example 1:**

```
Input: gifts = [25,64,9,4,100], k = 4
Output: 29
Explanation:
The gifts are taken in the following way:
- In the first second, the last pile is chosen and 10 gifts are left behind.
- Then the second pile is chosen and 8 gifts are left behind.
- After that the first pile is chosen and 5 gifts are left behind.
- Finally, the last pile is chosen again and 3 gifts are left behind.
The final remaining gifts are [5,8,9,4,3], so the total number of gifts remaining is 29.

```

**Example 2:**

```
Input: gifts = [1,1,1,1], k = 4
Output: 4
Explanation:
In this case, regardless which pile you choose, you have to leave behind 1 gift in each pile.
That is, you can't take any pile with you.
So, the total gifts remaining are 4.

```

**Constraints:**

- `1 <= gifts.length <= 103`
- `1 <= gifts[i] <= 109`
- `1 <= k <= 103`

## 문제 풀이:

```java
class Solution {
    public long pickGifts(int[] gifts, int k) {
         PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);

        for (int gift : gifts) {
            pq.offer(gift);
        }

        for (int i = 0; i < k; i++) {
            int max = pq.poll();
            int cnt = (int) Math.floor(Math.sqrt(max));
            pq.offer(cnt);
        }

        long total = 0;
        while (!pq.isEmpty()) {
            total += pq.poll();
        }

        return total;
    }
}
----------------------------------------------------------
Runtime
6 ms
Beats
60.52%
Memory
41.7 MB
Beats
22.48%
```

### **문제 풀이 해석:**

PriorityQueue를 이용하여 풀었다. 제일 큰값부터 poll 해주어야 했기 때문에 내림차순으로 정렬시켰다. gifts 배열을 순회하면서 pq에 값을 넣어주고 문제에서 제곱근을 남겨두고 나머지를 가져가라고 했기때문에 Math의 sqrt를 사용했다. 이후 return값이 long형이기 때문에, total를 long 형으로 선언한 후 값을 넣어주었다.