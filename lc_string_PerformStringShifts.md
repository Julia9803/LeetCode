### Perform String Shifts

You are given a string `s` containing lowercase English letters, and a matrix `shift`, where `shift[i] = [direction, amount]`:

- `direction` can be `0` (for left shift) or `1` (for right shift). 
- `amount` is the amount by which string `s` is to be shifted.
- A left shift by 1 means remove the first character of `s` and append it to the end.
- Similarly, a right shift by 1 means remove the last character of `s` and add it to the beginning.

Return the final string after all operations.

 

**Example 1:**

```
Input: s = "abc", shift = [[0,1],[1,2]]
Output: "cab"
Explanation: 
[0,1] means shift to left by 1. "abc" -> "bca"
[1,2] means shift to right by 2. "bca" -> "cab"
```

**Example 2:**

```
Input: s = "abcdefg", shift = [[1,1],[1,1],[0,2],[1,3]]
Output: "efgabcd"
Explanation:  
[1,1] means shift to right by 1. "abcdefg" -> "gabcdef"
[1,1] means shift to right by 1. "gabcdef" -> "fgabcde"
[0,2] means shift to left by 2. "fgabcde" -> "abcdefg"
[1,3] means shift to right by 3. "abcdefg" -> "efgabcd"
```

####  Solution:

```java
class Solution {
    public String stringShift(String s, int[][] shift) {
        int dir = 0;
        String res = null;
        int len = s.length();
        for(int[] i: shift) {
            dir += i[0] == 1? i[1]: -i[1];
        }
        dir %= len;
        System.out.println(dir);
        if(dir > 0) {
            res = s.substring(len - dir, len) + "" + s.substring(0, len - dir);
        } else {
            dir = -dir;
            res = s.substring(dir, len) + "" + s.substring(0, dir);
        }
        return res;
    }
}
```

##### Date 2020.4.14