# [leetcode] 1502. Can Make Arithmetic Progression From Sequence

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence/description/)

## 문제 설명:

A sequence of numbers is called an **arithmetic progression** if the difference between any two consecutive elements is the same.

Given an array of numbers `arr`, return `true` *if the array can be rearranged to form an **arithmetic progression**. Otherwise, return* `false`.

**Example 1:**

```
Input: arr = [3,5,1]
Output: true
Explanation:We can reorder the elements as [1,3,5] or [5,3,1] with differences 2 and -2 respectively, between each consecutive elements.

```

**Example 2:**

```
Input: arr = [1,2,4]
Output: false
Explanation:There is no way to reorder the elements to obtain an arithmetic progression.

```

**Constraints:**

- `2 <= arr.length <= 1000`
- `106 <= arr[i] <= 106`

## 문제 풀이:

```java
class Solution {
    public boolean canMakeArithmeticProgression(int[] arr) {
        Arrays.sort(arr);
        int cnt=arr[1]-arr[0];
        for(int i=2;i<arr.length;i++){
            if(arr[i]-arr[i-1]!=cnt) return false;
        }
        return true;
    }
}
----------------------------------------------------------
Runtime
2 ms
Beats
97.71%
Memory
41 MB
Beats
33.75%
```

### **문제 풀이 해석:**

양수를 담을 cnt1 변수, 음수를 담을 cnt2 변수를 설정한 후 , nums 배열을 순회하면서 조건에 맞게 분류한 뒤, 리턴했다.