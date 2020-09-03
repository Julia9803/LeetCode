### 0. Number Complement

Find a number's binary complement.

E.g. 5 -> 2

8->7

#### Solution:

```java
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
	public static void main (String[] args) {
		int n = 50;
		int t = 0;
		int i = n;
		while(i > 0) {
		    i /= 2;
		    t++;
		}
		int res = ((1 << t) - 1) ^ n;
		System.out.println(res);
	}
}
```

##### Date 2020.8.27