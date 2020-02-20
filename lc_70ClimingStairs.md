### 70. Climbing Stairs

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given *n* will be a positive integer.

**Example 1:**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

#### Solution:

```java
class Solution {
    public int climbStairs(int n) {
        // recursive
        int[] list = new int[n+1];
        return climbStairs(n, list);
    }
    public int climbStairs(int i, int[] list) {
        if(i == 0 || i == 1) return 1;
        if(i < 0) return 0;
        if(list[i] > 0) return list[i];
        list[i] = climbStairs(i-1, list) + climbStairs(i-2, list);
        return list[i];
    }
}
```

```java
class Solution {
    public int climbStairs(int n) {
        //fibonacci bottom up dp
        int[] dp = new int[n+1];
        if(n == 1) return 1;
        if(n == 2) return 2;
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2;i<=n;i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

