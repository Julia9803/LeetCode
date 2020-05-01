### 647. Palindromic Substrings

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**

```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

 

**Example 2:**

```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

 

**Note:**

1. The input string length won't exceed 1000.

####  Solution:

```java
class Solution {
    int res = 0;
    public int countSubstrings(String s) {
        for(int i = 0;i < s.length();i++) {//find palindromic substrs for each char as central spot
            extend(s,i,i);// odd length
            extend(s,i,i+1);// even length
        }
        return res;
    }
    
    private void extend(String s, int start, int end) {
        while(start >= 0 && end < s.length() && s.charAt(start) == s.charAt(end)) {
            res++;
            start--;
            end++;
        }
    }
}
```

##### Date 2020.5.1