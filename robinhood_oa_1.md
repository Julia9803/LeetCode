### 1.

![img](https://oss.1point3acres.cn/forum/202108/20/160831akkvxidazxikq5b8.jpeg)

#### Solution:

```java
package com.company;

public class Main {

    private static final int num1 = 123456;
    private static final int num2 = 72328;
    public static void main(String[] args) {
        String str = String.valueOf(num2);
        String res = "";
        for (int i = 0; i < str.length(); i+=2) {
            if (i == str.length() - 1) {
                res += str.charAt(i);
                break;
            }
            res += str.charAt(i+1);
            res += str.charAt(i);
        }
        System.out.println(res);
    }
}
```

##### Date 2021.8.23