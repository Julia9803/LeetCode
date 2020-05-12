### 279. Perfect Squares

Given a positive integer *n*, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to *n*.

**Example 1:**

```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

**Example 2:**

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

#### Solution:

```java
/**
dp[0] = 0
dp[1] = dp[1 - 1 * 1] + 1 = 1
dp[2] = dp[2 - 1 * 1] + 1 = 2
dp[3] = dp[3 - 1 * 1] + 1 = 3
dp[4] = min {dp[4 - 1 * 1] + 1, dp[4 - 2 * 2] + 1} = 1
...
dp[9] = min {dp[9 - 1 * 1] + 1, dp[9 - 2 * 2] + 1, dp[9 - 3 * 3] + 1} = 1
...
dp[n] = min {dp[n - i * i] + 1} i * i <= n
*/
// dp[i] = Math.min(dp[i], dp[i - j * j] + 1); frequently access dp[i] would cause more runtime so replace it with a temporary integer
class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for(int i = 1;i < n + 1;i++) {
            int min = Integer.MAX_VALUE;
            int j = 1;
            while(j * j <= i) {
                min = Math.min(min, dp[i - j * j] + 1);
                j++;
            }
            dp[i] = min;
        }
        return dp[n];
    }
}
```

```java
// a Time limit exceeded solution
class Solution {
    int res = Integer.MAX_VALUE;
    public int numSquares(int n) {
        dfs(n, 0);
        return res;
    }
    private void dfs(int n, int tmp) {
        if(n == 0) {
            res = Math.min(res, tmp);
            return;
        } else if(n < 0) return;
        
        // int sq = (int)Math.sqrt(n);
        // for(int i = 1; i <= sq;i++) {
        //     dfs(n - i * i, tmp + 1);
        // }
        for(int i = 1; i < n / 2 + 1;i++) {
            dfs(n - i * i, tmp + 1);
        }
    }
}
```

##### Date 2020.5.12