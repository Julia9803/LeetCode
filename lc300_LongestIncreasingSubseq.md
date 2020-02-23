### 300. Longest Increasing Subsequence

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:** 

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?

#### Solution:

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        // dp complexity o(n^2)
        if(nums == null || nums.length == 0) return 0;
        int res = 1;
        int[] dp = new int[nums.length]; // store value for max subseq len in each place
        Arrays.fill(dp, 1);
        for(int i = 1;i<nums.length;i++) { // pointer, the largest item
            for(int j = 0;j<i;j++) {
                if(nums[j] <nums[i]) {
                    dp[i] = Math.max(dp[j] + 1, dp[i]); // dp[j] save max subseq len at place nums[j]
                }
            }
            res = Math.max(res, dp[i]);
        }
        return res;
    }
}
```

