### 287. Find the Duplicate Number

Given an array *nums* containing *n* + 1 integers where each integer is between 1 and *n* (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example 1:**

```
Input: [1,3,4,2,2]
Output: 2
```

**Example 2:**

```
Input: [3,1,3,4,2]
Output: 3
```

**Note:**

1. You **must not** modify the array (assume the array is read only).
2. You must use only constant, *O*(1) extra space.
3. Your runtime complexity should be less than *O*(*n*2).
4. There is only one duplicate number in the array, but it could be repeated more than once.

#### Solution:

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int[] arr = new int[nums.length];
        for(int num: nums) {
            arr[num]++;
            if(arr[num] > 1) return num;
        }
        return 0;
    }
}
```

```java
// find loop in a linkedlist
class Solution {
    public int findDuplicate(int[] nums) {
        // each item in nums is the index of next node
        // nums can be a linkedlist with loop
        // find duplicate means find loop entrance
        // when slow and fast meet, len(fast) - len(slow) = len(slow);
        // so length from 0 to meet point is equal to meet point to meet point
        int slow = 0;
        int fast = 0;
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while(slow != fast);
        slow = 0;
        while(slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
}
```

##### Date 2020.5.8