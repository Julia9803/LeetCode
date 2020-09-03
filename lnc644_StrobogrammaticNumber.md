### 644. Strobogrammatic Number (Google)

A mirror number is a number that looks the same when rotated 180 degrees (looked at upside down).For example, the numbers "69", "88", and "818" are all mirror numbers.

Write a function to determine if a number is mirror. The number is represented as a string.

### Example

**Example 1:**

```
Input : "69"
Output : true
```

**Example 2:**

```
Input : "68"
Output : false
```

#### Solution:

```java
public class Solution {
    /**
     * @param num: a string
     * @return: true if a number is strobogrammatic or false
     */
    public boolean isStrobogrammatic(String num) {
        // write your code here
        char[] list = new char[256];
        list['0'] = '0';
        list['1'] = '1';
        list['6'] = '9';
        list['8'] = '8';
        list['9'] = '6';
        for(int i = 0;i < num.length();i++) {
            int j = num.length() - 1 - i; // 对称位置
            if(num.charAt(i) != list[num.charAt(j)])
                return false;
        }
        return true;
    }
}
```

##### Date 2020.8.23