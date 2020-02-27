### 169. Majority Element

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋`times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

**Example 2:**

```
Input: [2,2,1,1,1,2,2]
Output: 2
```

#### Solution:

```java
class Solution {
    public int majorityElement(int[] nums) {
        // O(nlogn)
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```

```java
class Solution {
    public int majorityElement(int[] nums) {
        // O(n)
        int major = nums[0];
        int times = 1;
        for(int i = 1;i<nums.length;i++) {
            if(times == 0) {
                major = nums[i];
                times++;
            } else if(nums[i] == major) times++;
            else times--;
        }
        return major;
    }
}
```

##### Date 2020.2.27