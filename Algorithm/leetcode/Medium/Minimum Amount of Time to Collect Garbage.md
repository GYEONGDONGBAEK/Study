# [leetcode] 2391. Minimum Amount of Time to Collect Garbage

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage/description/)

## 문제 설명:

You are given a **0-indexed** array of strings `garbage` where `garbage[i]` represents the assortment of garbage at the `ith` house. `garbage[i]` consists only of the characters `'M'`, `'P'` and `'G'` representing one unit of metal, paper and glass garbage respectively. Picking up **one** unit of any type of garbage takes `1` minute.

You are also given a **0-indexed** integer array `travel` where `travel[i]` is the number of minutes needed to go from house `i` to house `i + 1`.

There are three garbage trucks in the city, each responsible for picking up one type of garbage. Each garbage truck starts at house `0` and must visit each house **in order**; however, they do **not** need to visit every house.

Only **one** garbage truck may be used at any given moment. While one truck is driving or picking up garbage, the other two trucks **cannot** do anything.

Return *the **minimum** number of minutes needed to pick up all the garbage.*

**Example 1:**

```
Input: garbage = ["G","P","GP","GG"], travel = [2,4,3]
Output: 21
Explanation:
The paper garbage truck:
1. Travels from house 0 to house 1
2. Collects the paper garbage at house 1
3. Travels from house 1 to house 2
4. Collects the paper garbage at house 2
Altogether, it takes 8 minutes to pick up all the paper garbage.
The glass garbage truck:
1. Collects the glass garbage at house 0
2. Travels from house 0 to house 1
3. Travels from house 1 to house 2
4. Collects the glass garbage at house 2
5. Travels from house 2 to house 3
6. Collects the glass garbage at house 3
Altogether, it takes 13 minutes to pick up all the glass garbage.
Since there is no metal garbage, we do not need to consider the metal garbage truck.
Therefore, it takes a total of 8 + 13 = 21 minutes to collect all the garbage.

```

**Example 2:**

```
Input: garbage = ["MMM","PGM","GP"], travel = [3,10]
Output: 37
Explanation:
The metal garbage truck takes 7 minutes to pick up all the metal garbage.
The paper garbage truck takes 15 minutes to pick up all the paper garbage.
The glass garbage truck takes 15 minutes to pick up all the glass garbage.
It takes a total of 7 + 15 + 15 = 37 minutes to collect all the garbage.

```

**Constraints:**

- `2 <= garbage.length <= 105`
- `garbage[i]` consists of only the letters `'M'`, `'P'`, and `'G'`.
- `1 <= garbage[i].length <= 10`
- `travel.length == garbage.length - 1`
- `1 <= travel[i] <= 100`

## 문제 풀이:

```java
class Solution {
    public int garbageCollection(String[] garbage, int[] travel) {
        int ans=0;
        int m=0;
        int p=0;
        int g=0;
        for (int i=0;i<garbage.length;i++) {
            for (int j=0;j<garbage[i].length();j++){
                char c=garbage[i].charAt(j);
                if(c=='M') m++;
                if(c=='P') p++;
                if(c=='G') g++;
            }
            if(m>0&&i>0) ans+=travel[i-1];
            if(p>0&&i>0) ans+=travel[i-1];
            if(g>0&&i>0) ans+=travel[i-1];
        }
        return ans+m+p+g;
    }
}
----------------------------------------------------------
Runtime
49 ms
Beats
28.20%
Memory
68.5 MB
Beats
14.47%
```

### **문제 풀이 해석:**

garbage를 돌면서 M,P,G를 만나면 m,p,g의 값을 증가시켰다. 이 후 m,p,g >0 && i>0 조건은 쓰레기 차가 다른곳으로 갈때 필요한 값이다. 만약 둘 다 0보다 크다면 그 차가 다른곳으로 이동했다는 뜻이 되므로, 그 값을 ans에 더해주었다.