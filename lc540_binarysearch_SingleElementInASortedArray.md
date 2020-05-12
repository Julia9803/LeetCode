### 540. Single Element in a Sorted Array

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once. Find this single element that appears only once.

 

**Example 1:**

```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Example 2:**

```
Input: [3,3,7,7,10,11,11]
Output: 10
```

 

**Note:** Your solution should run in O(log n) time and O(1) space.

#### Solution:

```java
// array
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int[] res = new int[nums[nums.length - 1] + 1];
        for(int i = 0;i < nums.length;i++) {
            res[nums[i]] ++;
        }
        for(int i = 0;i < res.length;i++) {
            if(res[i] == 1) return i;
        }
        return -1;
    }
}
```

```java
// binary search
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int lo = 0, hi = nums.length - 1;
        while(lo < hi) {
            int mid = (lo + hi) / 2;
            if(mid % 2 != 0) mid--; // mid always be odd place and even index
            if(nums[mid] == nums[mid + 1]) lo = mid + 2; // target on the right
            else hi = mid;
        }
        return nums[lo];
    }
}
```

##### Date 2020.5.12