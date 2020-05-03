### 494. Target Sum

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols `+` and `-`. For each integer, you should choose one from `+` and `-` as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S. 

**Example 1:**

```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```



**Note:**

1. The length of the given array is positive and will not exceed 20. 
2. The sum of elements in the given array will not exceed 1000.
3. Your output answer is guaranteed to be fitted in a 32-bit integer.

#### Solution:

```java
class Solution {
    int res = 0;
    
    public int findTargetSumWays(int[] nums, int S) {
        dfs(nums, 0, 1, S, 0);
        dfs(nums, 0, -1, S, 0);
        return res;
    }
    
    private void dfs(int[] nums, int i, int tmp, int S, int sum) {
        if(i >= nums.length) return;
        sum += tmp * nums[i];
        if(i == nums.length - 1 && sum == S) {
            res++;
            return;
        }
        dfs(nums, i + 1, 1, S, sum);
        dfs(nums, i + 1, -1, S, sum);
    }
}
```

```java
class Solution {
    
    public int findTargetSumWays(int[] nums, int S) {
        int sum = 0;
        for(int num: nums) {
            sum += num;
        }
        if(sum < S) return 0;
        int len = nums.length;
        int[][] res = new int[len+1][2*sum+1];
        int offset = sum;
        res[0][offset] = 1;
        for(int i = 0;i < len;i++) {
            for(int j = nums[i];j<2*sum+1-nums[i];j++) {
                if(res[i][j] > 0) {
                    res[i+1][j-nums[i]] += res[i][j];
                    res[i+1][j+nums[i]] += res[i][j];
                }
            }
        }
        return res[len][S+offset];
    }
}
```

```java
class Solution {
    int res = 0;
    
    public int findTargetSumWays(int[] nums, int S) {
        int sumarr = 0;
        for(int i: nums) {
            sumarr+=i;
        }
        if(S > sumarr) return 0;
        
        dfs(nums, 0, S, 0);
        return res;
    }
    
    private void dfs(int[] nums, int i, int S, int sum) {
        if(i == nums.length) {
            if(sum == S) res++;
            return;
        }
        dfs(nums, i + 1, S, sum + nums[i]);
        dfs(nums, i + 1, S, sum - nums[i]);
    }
}
```

```java
// pull knapsack problem
class Solution {

    public int findTargetSumWays(int[] nums, int S) {
       int sum = 0;
        for(int num: nums) {
            sum += num;
        }
        if(sum < S || (sum + S) % 2 != 0) return 0;
        int target = (sum + S)/2;
        int[] dp = new int[target + 1];
        dp[0] = 1;
        
        for(int num: nums) {
            for(int j = target;j >= num;j--) {
                dp[j] += dp[j - num];
            }  
        }
        return dp[target];
    }
}
```

##### Date 2020.5.2