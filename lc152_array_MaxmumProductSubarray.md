### 152. Maximum Product Subarray

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

#### Solution:

```java
class Solution {
    public int maxProduct(int[] nums) {
        int l = 0, r = 0, max = nums[0];
        int len = nums.length;
        for(int i = 0;i < len;i++) {
            l = (l == 0 ? 1: l) * nums[i];
            r = (r == 0 ? 1: r) * nums[len - 1 - i];
            max = Math.max(max, Math.max(l, r));
        }
        return max;
    }
}
```

##### Date 2020.4.20

