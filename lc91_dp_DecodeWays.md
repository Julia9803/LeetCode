### 91. Decode Ways

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a **non-empty** string containing only digits, determine the total number of ways to decode it.

**Example 1:**

```
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**

```
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

#### Solution:

```java
class Solution {
    public int numDecodings(String s) {
        char[] arr = s.toCharArray();
        int len = arr.length;
        int[] list = new int[len + 1];// 记录前n个数的和
        list[0] = 1;
        
        if(len == 1) return arr[0] == '0' ? 0: 1;
        for(int i = 1;i <= len;i++) {
            list[i] = 0;
            // 最后一个是1-9
            if(arr[i-1] >= '1') {
                list[i] += list[i-1];
            }
            // 最后一个是两位数 10-26
            if(i > 1) {
                int num = 10 * (arr[i-2] - '0') + arr[i-1] - '0';
                if(num >= 10 && num <= 26) {
                    list[i] += list[i-2];
                }
            }
        }
        return list[len];
    }
}
```

##### Date 2020.8.22