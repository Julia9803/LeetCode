### 1. Low Keypress

![Image for post](https://miro.medium.com/max/2480/1*jYYknPqHEcf5DWpPNif2kg.png)

![Image for post](https://miro.medium.com/max/2460/1*8jwLyoOnHMv4H_Kkza389A.png)

#### Solution:

```java
/*package whatever //do not write package name here */

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {
	public static void main (String[] args) {
		//code
		int[][] list = {{0,2}, {1,3} ,{0,7}};
		int max = list[0][1];
		int index = 0;
		for(int i = 1;i < list.length;i++) {
		    if((list[i][1] - list[i-1][1]) > max) {
		        max = list[i][1] - list[i-1][1];
		        index = i;
		    }
		}
		System.out.println(index);
		System.out.println(getRes(index));
	}
	public static char getRes(int index) {
	    return (char)(index + 'a');
	}
}
```

##### Date 2020.8.27