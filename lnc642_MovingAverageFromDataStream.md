### 642. Moving Average from Data Stream

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

### Example

**Example 1:**

```
MovingAverage m = new MovingAverage(3);
m.next(1) = 1 // return 1.00000
m.next(10) = (1 + 10) / 2 // return 5.50000
m.next(3) = (1 + 10 + 3) / 3 // return 4.66667
m.next(5) = (10 + 3 + 5) / 3 // return 6.00000
```

#### Solution:

```java
public class MovingAverage {
    double[] sum;
    int size;
    int ptr;
    /*
    * @param size: An integer
    */public MovingAverage(int size) {
        // do intialization if necessary
        sum = new double[100000]; // 存前n个数的和
        sum[0] = 0;
        this.size = size;
        ptr = 0;
    }

    /*
     * @param val: An integer
     * @return:  
     */
    public double next(int val) {
        // write your code here
        ptr++;
        sum[ptr] = sum[ptr-1] + val;
        if(ptr > size)
            return (sum[ptr] - sum[ptr-size])/size;
        else
            return sum[ptr]/ptr;
    }
}
```

```java
public class MovingAverage {
    double[] sum;
    int size;
    int ptr;
    /*
    * @param size: An integer
    */public MovingAverage(int size) {
        // do intialization if necessary
        sum = new double[size+1]; // 存前n个数的和
        sum[0] = 0;
        this.size = size;
        ptr = 0;
    }
    
    // 滚动数组
    public int mod(int i) {
        return i % (size + 1);
    }

    /*
     * @param val: An integer
     * @return:  
     */
    public double next(int val) {
        // write your code here
        ptr++;
        sum[mod(ptr)] = sum[mod(ptr-1)] + val;
        if(ptr > size)
            return (sum[mod(ptr)] - sum[mod(ptr-size)])/size;
        else
            return sum[mod(ptr)]/ptr;
    }
}
```

##### Date 2020.8.23