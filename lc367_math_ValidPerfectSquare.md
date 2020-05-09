### 367. Valid Perfect Square

Given a positive integer *num*, write a function which returns True if *num* is a perfect square else False.

**Note:** **Do not** use any built-in library function such as `sqrt`.

**Example 1:**

```
Input: 16
Output: true
```

**Example 2:**

```
Input: 14
Output: false
```

#### Solution:

```java
// the square root of num < num/2 + 1
// 532ms
class Solution {
    public boolean isPerfectSquare(int num) {
        int tmp = num / 2 + 1;
        for(int i = 0;i <= tmp;i++) {
            if(i * i == num) return true;
        }
        return false;
    }
}
```

```java
// 1ms
class Solution {
    public boolean isPerfectSquare(int num) {
        double tmp = 0;
        if(num == 0 || num == 1) return true;
        if(num == 2) return false;
        for(double i = 2;i < num;i++) {
            tmp = num / i;
            if(tmp == i) return true;
            else if(tmp < i) return false;
        }
        return false;
    }
}
```

```java
/**
This is a math problem：
1 = 1
4 = 1 + 3
9 = 1 + 3 + 5
16 = 1 + 3 + 5 + 7
25 = 1 + 3 + 5 + 7 + 9
36 = 1 + 3 + 5 + 7 + 9 + 11
....
so 1+3+...+(2n-1) = (2n-1 + 1)n/2 = nn
*/
// 0ms
class Solution {
    public boolean isPerfectSquare(int num) {
        int i = 1;
        while(num > 0) {
            num -= i;
            i += 2;
        }
        return num == 0;
    }
}
```

```java
// binary search
// 0ms
class Solution {
    public boolean isPerfectSquare(int num) {
        long lo = 0;
        long hi = num / 2 + 1;
        long mid = 0, tmp = 0;
        while(lo < hi) {
            mid = lo + ((hi - lo + 1) >>> 1);
            tmp = mid * mid;
            if(tmp > num) {
                hi = mid - 1;
            } else {
                lo = mid;
            }  
        }
        return (int) lo * lo == num;
    }
}
```

##### Date 2020.5.10