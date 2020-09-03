### 659. Encode and Decode Strings

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Please implement `encode` and `decode`

### Example

**Example1**

```
Input: ["lint","code","love","you"]
Output: ["lint","code","love","you"]
Explanation:
One possible encode method is: "lint:;code:;love:;you"
```

**Example2**

```
Input: ["we", "say", ":", "yes"]
Output: ["we", "say", ":", "yes"]
Explanation:
One possible encode method is: "we:;say:;:::;yes"
```

#### Solution:

```java
// 如果不用StringBuilder用String，就会造成一个case Memory Overflow
public class Solution {
    /*
     * @param strs: a list of strings
     * @return: encodes a list of strings to a single string.
     */
    public String encode(List<String> strs) {
        // write your code here
        StringBuilder res = new StringBuilder();
        for(int i = 0;i < strs.size();i++) {
            String s = strs.get(i);
            char[] arr = s.toCharArray();
            for(int j = 0;j < arr.length;j++) {
                if(arr[j] == ':') {
                    res.append("::");
                } else {
                    res.append(arr[j]);
                }
            }
            res.append(":;");
        }
        return res.toString();
    }

    /*
     * @param str: A string
     * @return: dcodes a single string to a list of strings
     */
    public List<String> decode(String str) {
        // write your code here
        char[] arr = str.toCharArray();
        List<String> list = new ArrayList<String>();
        StringBuilder s = new StringBuilder(); // each string item of list
        int i = 0;
        while(i < arr.length) {
            if(arr[i] == ':') {
                if(arr[i+1] == ';') {
                    list.add(s.toString());
                    s = new StringBuilder();
                    i += 2;
                } else if(arr[i+1] == ':') {
                    s.append(":");
                    i += 2;
                }
            } else {
                s.append(arr[i]);
                i += 1;
            }
        }
        return list;
    }
}
```

##### Date 2020.8.24