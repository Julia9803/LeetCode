### 1. Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly\*** one solution, and you may not use the *same*element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

#### Solution:

```java
class Solution {
    // brute force
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0;i < nums.length-1;i++) {
            for(int j = i + 1;j < nums.length;j++) {
                if(nums[i] + nums[j] == target)
                    return new int[]{i,j};
            }
        }
        return null;
    }
}
```

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map = new HashMap<>();
        for(int i = 0;i<nums.length;i++) {
            if(map.containsKey(target-nums[i]))
                return new int[]{map.get(target-nums[i]), i};
            map.put(nums[i],i);
        }
        return null;
    }
}
```

##### Date 2020.4.12