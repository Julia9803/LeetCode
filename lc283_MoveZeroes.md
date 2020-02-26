### 283. Move Zeroes

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

#### Solution:

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if(nums == null || nums.length == 0) return;
        // disregard zero
        int index = 0;
        for(int num: nums) {
            if(num != 0) nums[index++] = num;
        }
        // add zero
        while(index < nums.length) {
            nums[index++] = 0;
        }
    }
}
```

##### Date 2020.2.26