### 581. Shortest Unsorted Continuous Subarray

Given an integer array, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too. 

You need to find the **shortest** such subarray and output its length.

**Example 1:**

```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```



**Note:**

1. Then length of the input array is in range [1, 10,000].
2. The input array may contain duplicates, so ascending order here means **<=**.

#### Solution:

```java
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        /** 
        end iterate from left to right and save the most right place smaller than value before
        begin iterate from right to left and save the most left place bigger than value after
        **/
        int begin = -1, end = -2, max = Integer.MIN_VALUE, min = Integer.MAX_VALUE, len = nums.length; // when array is ordered, end-begin+1=0.
        for(int i = 0;i < len;i++) {
            max = Math.max(max,nums[i]);
            min = Math.min(min,nums[len-1-i]);
            if(max > nums[i]) end = i;
            if(min < nums[len-1-i]) begin = len-1-i;
        }
        return end - begin + 1;
    }
}
```

##### Date 2020.3.1