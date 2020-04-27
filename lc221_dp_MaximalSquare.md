### 221. Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

#### Solution:

```java
class Solution {
    // use a int[m+1][n+1] auxiliary matrix dp
    // two for loops to iterate matrix, get min value of left top diagonal and add 1
    // store the max value from dp, it's area is the square of the value
    public int maximalSquare(char[][] matrix) {
        if(matrix.length == 0) return 0;
        int m = matrix.length, n = matrix[0].length;
        int[][] dp = new int[m + 1][n + 1]; //auxiliary matrix
        int res = 0;
        for(int i = 1;i <= m;i++) {
            for(int j = 1;j <= n;j++) {
                if(matrix[i-1][j-1] == '1') {
                    dp[i][j] = Math.min(Math.min(dp[i][j-1],dp[i-1][j-1]), dp[i-1][j]) + 1;
                    res = Math.max(res, dp[i][j]);
                }
            }
        }
        return res*res;
    }
}
```

##### Date 2020.4.27