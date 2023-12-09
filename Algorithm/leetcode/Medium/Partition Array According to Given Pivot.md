# [leetcode] 2161. Partition Array According to Given Pivot

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/partition-array-according-to-given-pivot/description/)

## 문제 설명:

You are given a **0-indexed** integer array `nums` and an integer `pivot`. Rearrange `nums` such that the following conditions are satisfied:

- Every element less than `pivot` appears **before** every element greater than `pivot`.
- Every element equal to `pivot` appears **in between** the elements less than and greater than `pivot`.
- The **relative order** of the elements less than `pivot` and the elements greater than `pivot` is maintained.
    - More formally, consider every `pi`, `pj` where `pi` is the new position of the `ith` element and `pj` is the new position of the `jth` element. For elements less than `pivot`, if `i < j` and `nums[i] < pivot` and `nums[j] < pivot`, then `pi < pj`. Similarly for elements greater than `pivot`, if `i < j` and `nums[i] > pivot` and `nums[j] > pivot`, then `pi < pj`.

Return `nums` *after the rearrangement.*

**Example 1:**

```
Input: nums = [9,12,5,10,14,3,10], pivot = 10
Output: [9,5,3,10,10,12,14]
Explanation:
The elements 9, 5, and 3 are less than the pivot so they are on the left side of the array.
The elements 12 and 14 are greater than the pivot so they are on the right side of the array.
The relative ordering of the elements less than and greater than pivot is also maintained. [9, 5, 3] and [12, 14] are the respective orderings.

```

**Example 2:**

```
Input: nums = [-3,4,3,2], pivot = 2
Output: [-3,2,4,3]
Explanation:
The element -3 is less than the pivot so it is on the left side of the array.
The elements 4 and 3 are greater than the pivot so they are on the right side of the array.
The relative ordering of the elements less than and greater than pivot is also maintained. [-3] and [4, 3] are the respective orderings.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `106 <= nums[i] <= 106`
- `pivot` equals to an element of `nums`.

## 문제 풀이:

```java
class Solution {
    public int[] pivotArray(int[] nums, int pivot) {
        int n=nums.length; int cnt=0;
        int [] ans=new int[n];
        
        for(int i=0;i<n;i++){
            if(nums[i]<pivot){
                ans[cnt++]=nums[i];
            }
        }
        for(int i=0;i<n;i++){
            if(nums[i]==pivot){
                ans[cnt++]=nums[i];
            }
        }
        for(int i=0;i<n;i++){
            if(nums[i]>pivot){
                ans[cnt++]=nums[i];
            }
        }
        return ans;
    }
}
----------------------------------------------------------
Runtime
6 ms
Beats
38.18%
Memory
54.2 MB
Beats
100%
```

### **문제 풀이 해석:**

배열을 순회하면서 pivot보다 작은값, pivot과 같은값, pivot보다 큰 값으로 범위를 나누어서 정답 배열에 추가하였다.