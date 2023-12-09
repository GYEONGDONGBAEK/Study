# [leetcode] 1637. Widest Vertical Area Between Two Points Containing No Points

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/widest-vertical-area-between-two-points-containing-no-points/)

## 문제 설명:

Given `n` `points` on a 2D plane where `points[i] = [xi, yi]`, Return *the **widest vertical area** between two points such that no points are inside the area.*

A **vertical area** is an area of fixed-width extending infinitely along the y-axis (i.e., infinite height). The **widest vertical area** is the one with the maximum width.

Note that points **on the edge** of a vertical area **are not** considered included in the area.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/19/points3.png](https://assets.leetcode.com/uploads/2020/09/19/points3.png)

```
Input: points = [[8,7],[9,9],[7,4],[9,7]]
Output: 1
Explanation: Both the red and the blue area are optimal.

```

**Example 2:**

```
Input: points = [[3,1],[9,0],[1,0],[1,4],[5,3],[8,8]]
Output: 3

```

**Constraints:**

- `n == points.length`
- `2 <= n <= 105`
- `points[i].length == 2`
- `0 <= xi, yi <= 109`

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
import java.util.*;
class Solution {
    public int maxWidthOfVerticalArea(int[][] points) {
        int ans=Integer.MIN_VALUE;
        int [] arr=new int[points.length];
        for(int i=0;i<arr.length;i++){
            arr[i]=points[i][0];
        }
        Arrays.sort(arr);
        for(int i=1;i<arr.length;i++){
            ans=Math.max(ans,arr[i]-arr[i-1]);
        }

        return ans;
    }
}
----------------------------------------------------------
Runtime
14 ms
Beats
62.42%
Memory
70.7 MB
Beats
18.95%
```

### **문제 풀이 해석:**

수직영역의 의미는 Y축과 평행한 두 직선사이의 영역을 의미하는것 같다, 즉 가장 큰 영역을 가지려면, X좌표의 차이가 가장 큰 값을 찾으면 된다. arr에 points의 x좌표를 복사한 후 , 정렬해주고 Math의 max를 활용하여 가장 큰 값을 찾아주었다.