### 213. House Robber II

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```

**Example 2:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

#### Solution:

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1) return nums[0];
        return Math.max(rob(nums, 0, nums.length-2),rob(nums, 1, nums.length-1));
    }
    
    public int rob(int[] nums, int lo, int hi) {
        int a = 0, b = 0;
        for(int i = lo; i <= hi;i++) {
            int p = a, q = b;
            a = nums[i] + q;
            b = Math.max(p, q);
        }
        return Math.max(a, b);
    }
}
```

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1) return nums[0];
        return Math.max(rob(nums, 0, nums.length-2),rob(nums, 1, nums.length-1));
    }
    public int rob(int[] nums, int lo, int hi) {
        int pre = 0, curr = 0;
        for(int i = lo; i <= hi;i++) {
            int t = curr;
            curr = Math.max(pre + nums[i], curr);
            pre = t;
        }
        return curr;
    }
}
```



##### Date 2020.2.29