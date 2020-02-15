### 6. ZigZag Conversion

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

#### Solution:

Use numRows String to save char. divide into two parts: vertical and oblique. A little trick in oblique char adding, see second for loop, decrease from numRows-2 to 1, then append char to the certain String.

```java
class Solution {
    public String convert(String s, int numRows) {
        StringBuffer[] sb = new StringBuffer[numRows];
        for(int n = 0;n < numRows;n++) sb[n] = new StringBuffer();
        char[] arr = s.toCharArray();
        int len = s.length();
        int i = 0;
        
        while(i < len) {
            for(int j = 0;j < numRows && i < len;j++) // vertical
                sb[j].append(arr[i++]);
            for(int k = numRows - 2;k >= 1 && i < len;k--) // oblique
                sb[k].append(arr[i++]);
        }
        
        for(int t = 1;t < numRows;t++)
            sb[0].append(sb[t]);
        
        return sb[0].toString();
    }
}
```

##### Date 2020.2.15