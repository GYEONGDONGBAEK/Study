# [leetcode] 500. Keyboard Row

---

## 문제 링크:

[문제 바로가기](https://leetcode.com/problems/keyboard-row/)

## 문제 설명:

Given an array of strings `words`, return *the words that can be typed using letters of the alphabet on only one row of American keyboard like the image below*.

In the **American keyboard**:

- the first row consists of the characters `"qwertyuiop"`,
- the second row consists of the characters `"asdfghjkl"`, and
- the third row consists of the characters `"zxcvbnm"`.

![https://assets.leetcode.com/uploads/2018/10/12/keyboard.png](https://assets.leetcode.com/uploads/2018/10/12/keyboard.png)

**Example 1:**

```
Input: words = ["Hello","Alaska","Dad","Peace"]
Output: ["Alaska","Dad"]

```

**Example 2:**

```
Input: words = ["omk"]
Output: []

```

**Example 3:**

```
Input: words = ["adsdf","sfd"]
Output: ["adsdf","sfd"]

```

**Constraints:**

- `1 <= words.length <= 20`
- `1 <= words[i].length <= 100`
- `words[i]` consists of English letters (both lowercase and uppercase).

## 문제 풀이:

```java
class Solution {
    public String[] findWords(String[] words) {
        List<String> ans = new ArrayList<>();
        String no1="qwertyuiopQWERTYUIOP";
        String no2="asdfghjklASDFGHJKL";
        String no3="zxcvbnmZXCVBNM";
        HashSet<Character> set1=new HashSet<>();
        HashSet<Character> set2=new HashSet<>();
        HashSet<Character> set3=new HashSet<>();

        for (char c : no1.toCharArray()) {
            set1.add(c);
        }
        for (char c : no2.toCharArray()) {
            set2.add(c);
        }
        for (char c : no3.toCharArray()) {
            set3.add(c);
        }
        for(String word : words){
            boolean flag1 = false;
            boolean flag2 = false;
            boolean flag3 = false;
            for(char c : word.toCharArray()){
                if(set1.contains(c)) flag1=true;
                else if(set2.contains(c)) flag2=true;
                else flag3=true;
            }
            if (flag1) {
                if (!flag2 && !flag3) {
                    ans.add(word);
                }
            }
            
            if (flag2) {
                if (!flag1 && !flag3) {
                    ans.add(word);
                }
            }
            
            if (flag3) {
                if (!flag1 && !flag2) {
                    ans.add(word);
                }
            }
        }
        return ans.toArray(new String[0]);
    }
}
----------------------------------------------------------
Runtime
18 ms
Beats
71.12%
Memory
44.6 MB
Beats
32.32%
```

### **문제 풀이 해석:**

Set 을 사용해서 풀었다. 일단 Set에 그 줄에 있는 알파벳을 모두 집어넣고 난 후 , boolean 변수인 flag를 사용해 set에 contains가 되어있다면 flag를 true로 바꿔준 후 , 만약 한개의 flag만 true라면 그 값을 ans에 add 하는 방식으로 풀었다.