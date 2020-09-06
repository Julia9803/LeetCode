### Max Consecutive Product

![img](https://oss.1point3acres.cn/forum/202008/18/060818rru8rmplq3dykllu.jpg)

```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
    public double solution(double[] A) {
        // write your code in Java SE 8
        int len = A.length;
        if(len == 0) return 0.0;
        double[] min = new double[len];
        double[] max = new double[len];
        min[0] = max[0] = A[0];
        double res = A[0];
        for(int i = 1;i < len;i++) {
            min[i] = Math.min(A[i], Math.min(A[i]*min[i-1], A[i]*max[i-1]));
            max[i] = Math.max(A[i], Math.max(A[i]*min[i-1], A[i]*max[i-1]));
            res = Math.max(res, Math.max(min[i], max[i]));
        }
        return res;
    }
}
```

##### Date 2020.9.6