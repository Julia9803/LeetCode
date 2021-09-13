### 125. Valid Palindrome

Given a string `s`, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

 

**Example 1:**

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**

```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

 

**Constraints:**

- `1 <= s.length <= 2 * 105`
- `s` consists only of printable ASCII characters.

#### Solution:

```java
class Solution {
    public boolean isPalindrome(String s) {
        int start = 0;
        int end = s.length() - 1;
        while(start < end) {
            char a = s.charAt(start);
            char b = s.charAt(end);
            if(!Character.isLetterOrDigit(a)) {
                start++;
            } else
            if(!Character.isLetterOrDigit(b)) {
                end--;
            } else
            if(Character.toLowerCase(a) == Character.toLowerCase(b)) {
                start++;
                end--;
            } else
            return false;
        }
        return true;
    }
}
```

##### Date 2021.9.5