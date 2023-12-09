# [프로그래머스] JadenCase 문자열 만들기

## 문제 링크:

[문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/12951)

## 문제 설명:

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)

문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

### 제한 조건

- s는 길이 1 이상 200 이하인 문자열입니다.
- s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
    - 숫자는 단어의 첫 문자로만 나옵니다.
    - 숫자로만 이루어진 단어는 없습니다.
    - 공백문자가 연속해서 나올 수 있습니다.

### 입출력 예

| s | return |
| --- | --- |
| "3people unFollowed me" | "3people Unfollowed Me" |
| "for the last week" | "For The Last Week" |

---

※ 공지 - 2022년 1월 14일 제한 조건과 테스트 케이스가 추가되었습니다.

## 문제 풀이:

```java
class Solution {
    public String solution(String s) {
        StringBuilder sb = new StringBuilder();
        String[] words = s.split(" ");

        for (int i = 0; i < words.length; i++) {
            if (words[i].isEmpty()) {
                sb.append(" ");
            } else {
                sb.append(words[i].substring(0, 1).toUpperCase());
                sb.append(words[i].substring(1).toLowerCase());
                sb.append(" ");
            }
        }

        if (s.endsWith(" ")) {
            return sb.toString();
        }
        return sb.toString().trim();
    }
}
----------------------------------------------------------
정확성  테스트
테스트 1 〉	통과 (0.14ms, 75.6MB)
테스트 2 〉	통과 (0.13ms, 75.2MB)
테스트 3 〉	통과 (0.17ms, 89.4MB)
테스트 4 〉	통과 (0.12ms, 71.2MB)
테스트 5 〉	통과 (0.19ms, 75.2MB)
테스트 6 〉	통과 (0.13ms, 78.5MB)
테스트 7 〉	통과 (0.16ms, 78.1MB)
테스트 8 〉	통과 (0.09ms, 74.4MB)
테스트 9 〉	통과 (0.12ms, 72.7MB)
테스트 10 〉	통과 (0.06ms, 72.6MB)
테스트 11 〉	통과 (0.14ms, 76.1MB)
테스트 12 〉	통과 (0.12ms, 69.1MB)
테스트 13 〉	통과 (0.12ms, 74MB)
테스트 14 〉	통과 (0.14ms, 73.5MB)
테스트 15 〉	통과 (0.14ms, 83.5MB)
테스트 16 〉	통과 (0.17ms, 78.5MB)
테스트 17 〉	통과 (0.13ms, 77.4MB)
테스트 18 〉	통과 (0.05ms, 71.2MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```

### **문제 풀이 해석:**

주어진 문자열을 공백을 이용해 split 해준 후, 배열을 순회하면서 isEmpty 메서드를 활용해 공백을 체크하여 공백이라면 공백을 append 해주고, 그렇지 않다면 substring 메서드를 사용해 맨 앞의 글자만 대문자로 바꿔주고, 나머지는 소문자로 바꾸는 방법을 사용하였다. 마지막에 공백으로 끝날수도 있기 때문에 공백으로 끝나는지 확인한 후 공백으로 끝난다면 그대로 리턴하고 아니라면 trim 해서 리턴하는 방법을 사용하였다.