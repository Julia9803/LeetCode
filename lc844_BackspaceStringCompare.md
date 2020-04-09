### 844. Backspace String Compare

Given two strings `S` and `T`, return if they are equal when both are typed into empty text editors. `#` means a backspace character.

**Example 1:**

```
Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
```

**Example 2:**

```
Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
```

**Example 3:**

```
Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
```

**Example 4:**

```
Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
```

**Note**:

1. `1 <= S.length <= 200`
2. `1 <= T.length <= 200`
3. `S` and `T` only contain lowercase letters and `'#'` characters.

**Follow up:**

- Can you solve it in `O(N)` time and `O(1)` space?

#### Solution:

```java
class Solution {
    // space O(m+n)
    public boolean backspaceCompare(String S, String T) {
        Stack<Character> s = new Stack<>();
        Stack<Character> t = new Stack<>();
        helper(S, s);
        helper(T, t);
        
        // below saves time
        // while(!s.empty()) {
        //     char tmp = s.pop();
        //     if(t.empty() || tmp != t.pop()) return false;
        // }
        // return s.empty() && t.empty(); 
        return String.valueOf(s).equals(String.valueOf(t));
    }
    
    private void helper(String str, Stack<Character> stack) {
        char[] c = str.toCharArray();
        for(int i = 0;i < c.length;i++) {
            if(c[i] != '#') {
                stack.add(c[i]);
            } else if(!stack.empty()) {
                stack.pop();
            }
        }
    }
}
```

```java
class Solution {    
    // space O(1)
    public boolean backspaceCompare(String S, String T) {
        int i = S.length() - 1;
        int j = T.length() - 1;
        int sSkip = 0, tSkip = 0;
        while(i >= 0 || j >= 0) {
            while(i >= 0) {
                if(S.charAt(i) == '#') {sSkip++; i--;}
                else if(sSkip > 0) {sSkip--; i--;}
                else break;
            }
            while(j >= 0) {
                if(T.charAt(j) == '#') {tSkip++; j--;}
                else if(tSkip > 0) {tSkip--; j--;}
                else break;
            }
            if(i >= 0 && j >= 0 && S.charAt(i) != T.charAt(j)) return false; // not equal
            if((i >= 0) != (j >= 0)) return false; // one is -1
            i--;
            j--;
        }
        return true;
    }
}
```

##### Date 2020.4.9