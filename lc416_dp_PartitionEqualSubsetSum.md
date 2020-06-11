### 416. Partition Equal Subset Sum

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

 

**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

 

**Example 2:**

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

####  Solution:

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int num: nums) sum += num;
        int[] dp = new int[sum+1];
        dp[0] = 1;
        
        if(sum%2 != 0) return false;
        for(int num: nums) {
            for(int i = sum/2;i >= num;i--) {
                dp[i] |= dp[i - num];
            }
            if(dp[sum/2] != 0) return true;
        }
        return false;
    }
}
```

##### Date 2020.6.11