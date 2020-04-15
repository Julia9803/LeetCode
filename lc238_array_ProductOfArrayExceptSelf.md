### 238. Product of Array Except Self

Given an array `nums` of *n* integers where *n* > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

**Constraint:** It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.

**Note:** Please solve it **without division** and in O(*n*).

**Follow up:**
Could you solve it with constant space complexity? (The output array **does not** count as extra space for the purpose of space complexity analysis.)

#### Solution:

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] res = new int[len];
        int[] left = new int[len];
        left[0] = 1;
        for(int i = 1;i < len;i++) {
            left[i] = nums[i-1] * left[i-1];
        }
        int right = 1;
        for(int i = len - 1;i >= 0;i--) {
            res[i] = left[i] * right;
            right *= nums[i];
        }
        return res;
    }
}
```

##### Date 2020.4.15