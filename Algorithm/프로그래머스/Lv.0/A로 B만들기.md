# [프로그래머스] A로 B 만들기

---

## 문제 링크:

[문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/120886)

## 문제 설명:

문자열 `before`와 `after`가 매개변수로 주어질 때, `before`의 순서를 바꾸어 `after`를 만들 수 있으면 1을, 만들 수 없으면 0을 return 하도록 solution 함수를 완성해보세요.

---

### 제한사항

- 0 < `before`의 길이 == `after`의 길이 < 1,000
- `before`와 `after`는 모두 소문자로 이루어져 있습니다.

---

### 입출력 예

| before | after | result |
| --- | --- | --- |
| "olleh" | "hello" | 1 |
| "allpe" | "apple" | 0 |

---

### 입출력 예 설명

입출력 예 #1

- "olleh"의 순서를 바꾸면 "hello"를 만들 수 있습니다.

입출력 예 #2

- "allpe"의 순서를 바꿔도 "apple"을 만들 수 없습니다.

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public int solution(String before, String after) {
        int[] charCount = new int[26];
        for (char c : before.toCharArray()) {
            charCount[c-'a']++;
        }
        for (char c : after.toCharArray()) {
            charCount[c-'a']--;
            if (charCount[c-'a'] < 0) {
                return 0;
            }
        }
        return 1;
    }
}
-----------------------------------------------------------
정확성  테스트
테스트 1 〉	통과 (0.03ms, 77.2MB)
테스트 2 〉	통과 (0.02ms, 74.1MB)
테스트 3 〉	통과 (0.02ms, 73.5MB)
테스트 4 〉	통과 (0.05ms, 75MB)
테스트 5 〉	통과 (0.22ms, 79.2MB)
테스트 6 〉	통과 (0.03ms, 81.9MB)
테스트 7 〉	통과 (0.03ms, 76.5MB)
테스트 8 〉	통과 (0.07ms, 79.6MB)
테스트 9 〉	통과 (0.04ms, 74.4MB)
테스트 10 〉	통과 (0.07ms, 78MB)
테스트 11 〉	통과 (0.10ms, 78.4MB)
테스트 12 〉	통과 (0.11ms, 77.7MB)
테스트 13 〉	통과 (0.03ms, 71.4MB)
테스트 14 〉	통과 (0.04ms, 79.2MB)
테스트 15 〉	통과 (0.07ms, 69.9MB)
테스트 16 〉	통과 (0.06ms, 76.7MB)
테스트 17 〉	통과 (0.06ms, 78MB)
테스트 18 〉	통과 (0.15ms, 79.8MB)
테스트 19 〉	통과 (0.12ms, 74.8MB)
테스트 20 〉	통과 (0.10ms, 65.2MB)
테스트 21 〉	통과 (0.16ms, 76.9MB)
테스트 22 〉	통과 (0.03ms, 83.9MB)
테스트 23 〉	통과 (0.02ms, 73.9MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```

### **문제 풀이 해석:**

알파벳의 카운트를 담을 배열을 하나 설정하고 before를 순회하면서 카운트를 증가시키고 after를 순회하면서 카운트를 감소시킨다. 만약 after를 순회하고 난 뒤 배열의 카운트에 음수가 있다면 after에 있는 알파벳이 before에 없기때문에 아무리 before 의 순서를 바꿔도 after가 될 수 없으므로 0을 반환한다. 그 경우가 아니라면 1을 반환한다.