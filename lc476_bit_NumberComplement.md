### 476. Number Complement

Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

 

**Example 1:**

```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
```

 

**Example 2:**

```
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```

 

**Note:**

1. The given integer is guaranteed to fit within the range of a 32-bit signed integer.
2. You could assume no leading zero bit in the integer’s binary representation.
3. This question is the same as 1009: https://leetcode.com/problems/complement-of-base-10-integer/

#### Solution:

```java
/**
1 2  3  4   5   6   7   8
1 10 11 100 101 110 111 1000
0 01 00 011 010 001 000 0111
0 1  0  3   2   1   0   7

pattern: 0, 1 0, 3 2 1 0, 7 6 5 4 3 2 1 0
res = (nearest 2^n - 1) - (num - nearest 2^n)
*/
class Solution {
    public int findComplement(int num) {
        if(num == 1) return 0;
        int tmp = num;
        int t = 0; // find nearest 2^n
        while(tmp >= 2) {
            tmp /= 2;
            t ++;
        }
        t = (int)Math.pow(2,t);
        return t - 1 - (num - t);
    }
}
```

##### Date 2020.5.4