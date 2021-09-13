### 42. Trapping Rain Water

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

 

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

#### Solution:

```java
class Solution {
    // 1. brute force to find left and right max, O(n^2)
    // 2. more space, less time -> get left and right max prefix sum
    // 3. best, written below. water height depend on lower side of wall
    public int trap(int[] height) {
        int leftMax = 0;
        int rightMax = 0;
        int i = 0;
        int j = height.length - 1;
        int res = 0;
        while(i <= j) {
            leftMax = Math.max(leftMax, height[i]);
            rightMax = Math.max(rightMax, height[j]);
            if(leftMax < rightMax) {
                res += leftMax - height[i];
                i++;
            } else {
                res += rightMax - height[j];
                j--;
            }
        }
        return res;
    }
}
```

##### Date 2021.9.12