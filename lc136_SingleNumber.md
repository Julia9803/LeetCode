### 136. Single Number

Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```

#### Solution:

we use bitwise XOR to solve this problem :

first , we have to know the bitwise XOR in java

1. **0 ^ N = N**
2. **N ^ N = 0**

So..... if N is the single number

N1 ^ N1 ^ N2 ^ N2 ^..............^ Nx ^ Nx ^ N

= (N1^N1) ^ (N2^N2) ^..............^ (Nx^Nx) ^ N

= 0 ^ 0 ^ ..........^ 0 ^ N

= N

```java
class Solution {
    public int singleNumber(int[] nums) {
        int num = 0;
        for(int i = 0;i<nums.length;i++) {
            num ^= nums[i];
        }
        return num;
    }
}
```

##### Date 2020.2.26