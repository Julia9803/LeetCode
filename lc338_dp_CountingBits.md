### 338. Counting Bits

Given a non negative integer number **num**. For every numbers **i** in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.

**Example 1:**

```
Input: 2
Output: [0,1,1]
```

**Example 2:**

```
Input: 5
Output: [0,1,1,2,1,2]
```

**Follow up:**

- It is very easy to come up with a solution with run time **O(n\*sizeof(integer))**. But can you do it in linear time **O(n)** /possibly in a single pass?
- Space complexity should be **O(n)**.
- Can you do it like a boss? Do it without using any builtin function like **__builtin_popcount** in c++ or in any other language.

#### Solution:

```java
/**
dp[0] = 0;
dp[1] = dp[1-1] + 1 = 1;
dp[2] = dp[2-2] + 1 = 1;
dp[3] = dp[3-2] + 1 = 2;
dp[4] = dp[4-4] + 1 = 1;
dp[5] = dp[5-4] + 1 = 2;
dp[6] = dp[6-4] + 1 = 2;
dp[7] = dp[7-4] + 1 = 3;
dp[8] = dp[8-8] + 1 = 1;
dp[n] = dp[n-offset] + 1;
*/
class Solution {
    public int[] countBits(int num) {
        int offset = 1;
        int[] res = new int[num + 1];
        res[0] = 0;
        for(int i = 1;i < num + 1;i++) {
            if(offset * 2 == i)
                offset *= 2;
            res[i] = res[i - offset] + 1;
        }
        return res;
    }
}
```

##### Date 2020.5.3