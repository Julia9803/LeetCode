### 33. Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

#### Solution:

```java
class Solution {
    public int search(int[] nums, int target) {
        // 1. find the rotate point
        int lo = 0, hi = nums.length - 1;
        while(lo < hi) {
            int mid = (lo+hi)/2;
            if(nums[mid] > nums[hi]) lo = mid + 1;
            else hi = mid;
        }
        int rot = lo;
        // 2. binary search
        lo = 0;
        hi = nums.length - 1;
        
        while(lo <= hi) {
            int mid = (lo+hi)/2;
            int realmid = (mid + rot) % nums.length;
            if(nums[realmid] == target) return realmid;
            if(nums[realmid] < target) lo = mid + 1;
            if(nums[realmid] > target) hi = mid - 1;
        }
        return -1;
    }
}
```

##### Date 2020.3.14