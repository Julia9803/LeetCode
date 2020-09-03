### 640. One Edit Distance

Given two strings S and T, determine if they are both one edit distance apart.
One ediit distance means doing one of these operation:

- insert one character in any position of S
- delete one character in S
- change one character in S to other character

### Example

Example 1:

```
Input: s = "aDb", t = "adb" 
Output: true
```

Example 2:

```
Input: s = "ab", t = "ab" 
Output: false
Explanation:
s=t ,so they aren't one edit distance apart
```

#### Solution:

```java
public class Solution {
    /**
     * @param s: a string
     * @param t: a string
     * @return: true if they are both one edit distance apart or false
     */
    public boolean isOneEditDistance(String s, String t) {
        // write your code here
        String tmp = null;
        if(s.length() < t.length()) {
            tmp = s;
            s = t;
            t = tmp;
        }
        char[] arr1 = s.toCharArray();
        char[] arr2 = t.toCharArray();
        // more than 1 bit length difference
        if(arr1.length > arr2.length + 1) return false;
        // 1 bit length difference
        if(arr1.length == arr2.length + 1) {
            int ptr = 0, i = 0; // string t ptr, s i
            int diff = 1;
            while(i < arr2.length) {
                if(arr1[ptr] != arr2[i]) {
                    ptr++;
                    if(--diff < 0) return false;
                } else {
                    ptr++;
                    i++;
                }
            }
            return true;
        }
        // same length
        if(arr1.length == arr2.length) {
            for(int i = 0;i < arr1.length;i++) {
                if(arr1[i] != arr2[i]) {
                    arr2[i] = arr1[i];
                    if(String.valueOf(arr1).equals(String.valueOf(arr2))) return true;
                    return false;
                }
            }
            return false;
        }
        return false;
    }
}
```

##### Date 2020.8.23