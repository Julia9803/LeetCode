### 231. Power of Two

Given an integer, write a function to determine if it is a power of two.

**Example 1:**

```
Input: 1
Output: true 
Explanation: 20 = 1
```

**Example 2:**

```
Input: 16
Output: true
Explanation: 24 = 16
```

**Example 3:**

```
Input: 218
Output: false
```

#### Solution:

//注释掉的解法是TLE的。

```java
// class Solution {
//     public boolean isPowerOfTwo(int n) {
//         if(n < 1) return false;
//         int m = 1;
//         while(m < n) {
//             m <<= 1;
//         }
//         if(m == n) return true;
//         return false;
//     }
// }
class Solution {
    public boolean isPowerOfTwo(int n) {
        return (n >= 1) && ((n & (n - 1)) == 0);
    }
}
```

