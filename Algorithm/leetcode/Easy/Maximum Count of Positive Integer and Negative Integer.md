# [leetcode] 2529. Maximum Count of Positive Integer and Negative Integer

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer/description/)

## 문제 설명:

Given an array `nums` sorted in **non-decreasing** order, return *the maximum between the number of positive integers and the number of negative integers.*

- In other words, if the number of positive integers in `nums` is `pos` and the number of negative integers is `neg`, then return the maximum of `pos` and `neg`.

**Note** that `0` is neither positive nor negative.

**Example 1:**

```
Input: nums = [-2,-1,-1,1,2,3]
Output: 3
Explanation: There are 3 positive integers and 3 negative integers. The maximum count among them is 3.

```

**Example 2:**

```
Input: nums = [-3,-2,-1,0,0,1,2]
Output: 3
Explanation: There are 2 positive integers and 3 negative integers. The maximum count among them is 3.

```

**Example 3:**

```
Input: nums = [5,20,66,1314]
Output: 4
Explanation: There are 4 positive integers and 0 negative integers. The maximum count among them is 4.

```

**Constraints:**

- `1 <= nums.length <= 2000`
- `2000 <= nums[i] <= 2000`
- `nums` is sorted in a **non-decreasing order**.

## 문제 풀이:

```java
class Solution {
    public int maximumCount(int[] nums) {
        int cnt1=0;
        int cnt2=0;
        for(int num : nums){
            if(num>0) cnt1++;
            else if(num<0) cnt2++;
        }
        if(cnt1>cnt2) return cnt1;
        else return cnt2;
    }
}
----------------------------------------------------------
Runtime
0 ms
Beats
100%
Memory
44.9 MB
Beats
6.13%
```

### **문제 풀이 해석:**

양수를 담을 cnt1 변수, 음수를 담을 cnt2 변수를 설정한 후 , nums 배열을 순회하면서 조건에 맞게 분류한 뒤, 리턴했다.