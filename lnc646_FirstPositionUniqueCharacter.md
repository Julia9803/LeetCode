### 646. First Position Unique Character(Amazon)

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return `-1`.

### Example

**Example 1:**

```
Input : s = "lintcode"
Output : 0
```

**Example 2:**

```
Input : s = "lovelintcode"
Output : 2
```

#### Solution:

```java
public class Solution {
    /**
     * @param s: a string
     * @return: it's index
     */
    public int firstUniqChar(String s) {
        // write your code here
        char[] arr = s.toCharArray();
        int[] times = new int[256];
        for(int i = 0;i < arr.length;i++) {
            times[arr[i]]++;
        }
        for(int i = 0;i < arr.length;i++) {
            if(times[arr[i]] == 1) return i;
        }
        return -1;
    }
}
```

##### Date 2020.8.25