# [프로그래머스] k의 개수

---

## 문제 링크:

[문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/120887)

## 문제 설명:

1부터 13까지의 수에서, 1은 1, 10, 11, 12, 13 이렇게 총 6번 등장합니다. 정수 `i`, `j`, `k`가 매개변수로 주어질 때, `i`부터 `j`까지 `k`가 몇 번 등장하는지 return 하도록 solution 함수를 완성해주세요.

---

### 제한사항

- 1 ≤ `i` < `j` ≤ 100,000
- 0 ≤ `k` ≤ 9

---

### 입출력 예

| i | j | k | result |
| --- | --- | --- | --- |
| 1 | 13 | 1 | 6 |
| 10 | 50 | 5 | 5 |
| 3 | 10 | 2 | 0 |

---

### 입출력 예 설명

입출력 예 #1

- 본문과 동일합니다.

입출력 예 #2

- 10부터 50까지 5는 15, 25, 35, 45, 50 총 5번 등장합니다. 따라서 5를 return 합니다.

입출력 예 #3

- 3부터 10까지 2는 한 번도 등장하지 않으므로 0을 return 합니다.

## 문제 풀이:

```java
class Solution {
    public int solution(int i, int j, int k) {
        int answer = 0;

        StringBuilder sb = new StringBuilder();
        for(int p = i; p <= j; p++){
            sb.append(p);
        }
        
        String str = sb.toString();
        for(char ch : str.toCharArray()){
            if(ch - '0' == k){
                answer++;
            }
        }
        
        return answer;
    }
}
-----------------------------------------------------------
정확성  테스트
테스트 1 〉	통과 (18.56ms, 95.3MB)
테스트 2 〉	통과 (0.08ms, 74MB)
테스트 3 〉	통과 (0.04ms, 76.4MB)
테스트 4 〉	통과 (2.78ms, 76.1MB)
테스트 5 〉	통과 (2.37ms, 75.2MB)
테스트 6 〉	통과 (0.07ms, 77.4MB)
테스트 7 〉	통과 (0.80ms, 66.7MB)
테스트 8 〉	통과 (6.88ms, 76.6MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```

```java
class Solution {
    public int solution(int i, int j, int k) {
        int answer = 0;
        
        for(int num = i; num <= j; num++) {
            int temp = num;
            while(temp > 0) {
                if(temp % 10 == k) {
                    answer++;
                }
                temp /= 10;
            }
        }
        
        return answer;
    }
}
-----------------------------------------------------------
정확성  테스트
테스트 1 〉	통과 (6.16ms, 85.5MB)
테스트 2 〉	통과 (0.02ms, 73.1MB)
테스트 3 〉	통과 (0.02ms, 84.9MB)
테스트 4 〉	통과 (1.73ms, 72.8MB)
테스트 5 〉	통과 (0.80ms, 75.1MB)
테스트 6 〉	통과 (0.01ms, 71.3MB)
테스트 7 〉	통과 (0.14ms, 81.9MB)
테스트 8 〉	통과 (2.07ms, 74.5MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```

### **문제 풀이 해석:**

첫번째 풀이는 모든 수를 다 Stringbuilder로 만든 후 char 배열로 만들어 k랑 똑같은 수가 있다면 answer를 한개씩 올리는 방법으로 풀었고

두번째 풀이는 while문을 순회하면서 10으로 나눈 값이 k 라면 answer를 한개씩 올리는 방법으로 풀었다.