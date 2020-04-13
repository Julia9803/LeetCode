### 525. Contiguous Array

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1. 

**Example 1:**

```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```



**Example 2:**

```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```



**Note:** The length of the given binary array will not exceed 50,000.

#### Solution:

```java
class Solution {
    public int findMaxLength(int[] nums) {
        // change all 0 to -1, save all <sum,index> to a hashmap
        int res = 0, sum = 0;
        Map<Integer,Integer> map = new HashMap<>();
        for(int i = 0;i < nums.length;i++) {
            sum += nums[i] > 0 ? 1: -1;
            if(sum == 0) res = i + 1; // start from index 0
            else if(map.containsKey(sum)) 
                res = Math.max(res, i - map.get(sum));
            else map.put(sum, i);
        }
        return res;
    }
}
```

##### Date 2020.4.13