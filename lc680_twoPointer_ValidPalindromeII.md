### 680. Valid Palindrome II

Given a string `s`, return `true` *if the* `s` *can be palindrome after deleting **at most one** character from it*.

 

**Example 1:**

```
Input: s = "aba"
Output: true
```

**Example 2:**

```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```

**Example 3:**

```
Input: s = "abc"
Output: false
```

 

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of lowercase English letters.

#### Solution:

```java
class Solution {
    public boolean validPalindrome(String s) {
        int i = 0;
        int j = s.length() - 1;
        while(i <= j) {
            if(s.charAt(i) != s.charAt(j)) {
                return isPalindromic(s, i, j - 1) || isPalindromic(s, i + 1, j);
            }
            i++;
            j--;
        }
        return true;
    }
    
    private boolean isPalindromic(String s, int i, int j) {
        while(i <= j) {
            if(s.charAt(i) != s.charAt(j)) return false;
            i++;
            j--;
        }
        return true;
    }
}
```

##### Date 2021.9.12