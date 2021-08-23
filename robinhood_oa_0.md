### 0. 给一个数，常数k，将数转换为字符串后以k为长分割原字符串，加在一起后形成新的数,当 array length <= k 时停止

 Eg. 1112324432

   ->   [111] [232] [443] [2]                   （将数转换为字符串后以k为长分割原字符串）

   -> [3] [7] [11] [2]                                                 （分割后相加）

   ->37112                                                                                 （新的数， length > k 继续执行）

   ->[3 7 1] [1 2]

   -> [11] [3]

   -> 113  length <= 3 stop

   return 113

#### Solution:

```java
package com.company;

public class Main {

    private static final int num = 1112324432;
    private static final int k = 3;
    public static void main(String[] args) {
        // 1112324432
        String res = String.valueOf(num);
        while (res.length() > k) {
            StringBuilder str = new StringBuilder();
            for (int i = 0; i < res.length(); i+=k) {
                int sum = 0;
                for (int j = i;j < i + k;j++) {
                    if (j >= res.length()) {
                        break;
                    }
                    sum += res.charAt(j) - '0';
                }
                str.append(sum);
            }
            res = str.toString();
        }
        System.out.println(res);
    }
}
```

##### Date 2021.8.23