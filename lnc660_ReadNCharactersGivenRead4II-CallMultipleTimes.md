### 660. Read N Characters Given Read4 II - Call multiple times(Google, FB)

The API: `int read4(char *buf)` reads `4` characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function `int read(char *buf, int n)` that reads n characters from the file.

### Example

**Example 1**

```plain
Input:
"filetestbuffer"
read(6)
read(5)
read(4)
read(3)
read(2)
read(1)
read(10)
Output:
6, buf = "filete"
5, buf = "stbuf"
3, buf = "fer"
0, buf = ""
0, buf = ""
0, buf = ""
0, buf = ""
```

**Example 2**

```plain
Input:
"abcdef"
read(1)
read(5)
Output:
1, buf = "a"
5, buf = "bcdef"
```

### Notice

The `read` function may be called multiple times.

Input test data (one parameter per line)How to understand a testcase?

#### Solution:

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf destination buffer
     * @param n maximum number of characters to read
     * @return the number of characters read
     */
    int p, bpos = 0, bend = 0;
    char[] buffer = new char[4];
    public int read(char[] buf, int n) {
        // Write your code here
        p = 0;
        while(p < n) {
            // when read buffer to the end, get new buffer
            if(bpos == bend) {
                bend = read4(buffer);
                bpos = 0;
            }
            // if read new buffer size equal to 0, return 0
            if(bend == 0) break;
            // read buffer to buf
            while(p < n && bpos < bend) {
                buf[p++] = buffer[bpos++];
            }
        }
        return p;
    }
}
```

##### Date 2020.8.23