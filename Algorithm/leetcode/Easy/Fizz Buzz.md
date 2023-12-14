# [leetcode] 412. Fizz Buzz

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/fizz-buzz/description/)

## 문제 설명:

Given an integer `n`, return *a string array* `answer` *(**1-indexed**) where*:

- `answer[i] == "FizzBuzz"` if `i` is divisible by `3` and `5`.
- `answer[i] == "Fizz"` if `i` is divisible by `3`.
- `answer[i] == "Buzz"` if `i` is divisible by `5`.
- `answer[i] == i` (as a string) if none of the above conditions are true.

**Example 1:**

```
Input: n = 3
Output: ["1","2","Fizz"]

```

**Example 2:**

```
Input: n = 5
Output: ["1","2","Fizz","4","Buzz"]

```

**Example 3:**

```
Input: n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]

```

**Constraints:**

- `1 <= n <= 104`

## 문제 풀이:

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> ans=new ArrayList<>();
        for(int i=1;i<=n;i++){
            if(i%3==0 && i%5==0) ans.add("FizzBuzz");
            else if(i%3==0) ans.add("Fizz");
            else if(i%5==0) ans.add("Buzz");
            else ans.add(String.valueOf(i));
        }
        return ans;
    }
}
----------------------------------------------------------
Runtime
1 ms
Beats
99.66%
Memory
44.8 MB
Beats
49.78%
```

### **문제 풀이 해석:**

쉬운 문제였다. i가 3이랑 5로 나누어 지면 FizzBuzz, 3으로만 나누어 진다면 Fizz, 5로만 나누어 진다면 Buzz를 리턴하고 3과 5로 나누어지지 않는다면 그 인덱스 자체로 값을 리턴한다.