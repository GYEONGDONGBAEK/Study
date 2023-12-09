# [leetcode] 1338. Reduce Array Size to The Half

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/reduce-array-size-to-the-half/description/)

## 문제 설명:

You are given an integer array `arr`. You can choose a set of integers and remove all the occurrences of these integers in the array.

Return *the minimum size of the set so that **at least** half of the integers of the array are removed*.

**Example 1:**

```
Input: arr = [3,3,3,3,5,5,5,2,2,7]
Output: 2
Explanation: Choosing {3,7} will make the new array [5,5,5,2,2] which has size 5 (i.e equal to half of the size of the old array).
Possible sets of size 2 are {3,5},{3,2},{5,2}.
Choosing set {2,7} is not possible as it will make the new array [3,3,3,3,5,5,5] which has a size greater than half of the size of the old array.

```

**Example 2:**

```
Input: arr = [7,7,7,7,7,7]
Output: 1
Explanation: The only possible set you can choose is {7}. This will make the new array empty.

```

**Constraints:**

- `2 <= arr.length <= 105`
- `arr.length` is even.
- `1 <= arr[i] <= 105`

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public int minSetSize(int[] arr) {
        int n = arr.length;
        int targetSize = n / 2;

        Map<Integer, Integer> Map = new HashMap<>();
        for (int num : arr) {
            Map.put(num, Map.getOrDefault(num, 0) + 1);
        }

        int[] frequencies = new int[Map.size()];
        int index = 0;
        for (int frequency : Map.values()) {
            frequencies[index++] = frequency;
        }
        Arrays.sort(frequencies);

        int removedCount = 0;
        int size = 0;

        for (int i = frequencies.length - 1; i >= 0; i--) {
            removedCount += frequencies[i];
            size++;

            if (removedCount >= targetSize) {
                break;
            }
        }

        return size;
    }
}
----------------------------------------------------------
Runtime
29 ms
Beats
88.81%
Memory
58.4 MB
Beats
28.84%
```

### **문제 풀이 해석:**

Map을 이용하여 arr에 있는 원소의 빈도수를 저장한 후, frequencies 배열을 만들어서 빈도수를 넣고 오름차순으로 정렬한 후, 맨 끝 인덱스부터 순회하면서 removedCount를 증가시키고, size를 1씩 증가시켰다. 만약 removedCount가 targetSize보다 크다면 break;를 하고 size를 반환하였다.