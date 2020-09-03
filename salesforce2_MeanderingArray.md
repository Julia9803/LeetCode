### 2. Meandering Array

![img](https://oss.1point3acres.cn/forum/202008/22/054657n8aatntmkbtkyyao.png)

![img](https://oss.1point3acres.cn/forum/202008/22/054705w8bfpbflj4bf5dgp.png)

```java
/*package whatever //do not write package name here */

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {
	public static void main (String[] args) {
		//code
		int[] list = {5, 2, 7, 8, -2, 25, 25};
		Arrays.sort(list);
		int len = list.length;
		int[] res = new int[len];
		int p = 0, i = len-1, j = 0;
		while(p < len) {
		    res[p++] = list[i--];
		    if(p < len) res[p++] = list[j++];
		}
		
		// check ans
		for(i = 0;i < len;i++) {
		    System.out.println(res[i]);
		}
	}
}
```

##### Date 2020.8.27