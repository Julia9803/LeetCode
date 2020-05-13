### 402. Remove K Digits

Given a non-negative integer *num* represented as a string, remove *k* digits from the number so that the new number is the smallest possible.

**Note:**

- The length of *num* is less than 10002 and will be ≥ *k*.
- The given *num* does not contain any leading zero.



**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```



**Example 2:**

```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```



**Example 3:**

```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

#### Solution:

```java
// 当前一位比后一位大的时候删除
class Solution {
    public String removeKdigits(String num, int k) {
        int len = num.length();
        if(len == k) return "0";
        if(k == 0) return num;
        
        Stack<Character> stack = new Stack<>();
        int index = 0;
        while(index < len) { // delete
            while(k > 0 && !stack.isEmpty() && stack.peek() > num.charAt(index)) {
                stack.pop();
                k--;
            }
            stack.push(num.charAt(index++));
        }
        while(k-- > 0) stack.pop(); // when delete not enough
        
        String res = "";
        while(!stack.isEmpty()) res = stack.pop() + res; // pop stack and store digits
        while(res.charAt(0) == '0' && res.length() > 1) res = res.substring(1); // delete leading zero
        return res;
    }
}
```

##### Date 2020.5.14