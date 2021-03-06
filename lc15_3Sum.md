### 15. 3Sum

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

#### Solution:

1st sort the list, then iterate each one, except for duplicate ones. 

Then add up nums[i+1] and nums[nums.length-1], if equals target, save, else if smaller lower point +1, else higher point - 1. low++, high--

Then low++, high--, compare while low < high.

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> list = new LinkedList<>();
        Arrays.sort(nums);
        int sum;
        for(int i = 0;i<nums.length-2;i++) {
            if(i == 0 || (i > 0 && nums[i] != nums[i-1])) { //avoid duplicate
                sum = 0 - nums[i];
                int j = i+1;
                int k = nums.length-1;
                while(j < k) {
                    if(nums[j] + nums[k] == sum) {
                        list.add(Arrays.asList(nums[i],nums[j],nums[k]));
                        while(j < k && nums[j] == nums[j+1]) j++;
                        while(j < k && nums[k] == nums[k-1]) k--;
                        j++;
                        k--;
                    }
                    else if(nums[j] + nums[k] < sum) j++;
                    else k--;
                }
            }
        }
        return list;
    }
}
```

##### Date 2020.2.14

