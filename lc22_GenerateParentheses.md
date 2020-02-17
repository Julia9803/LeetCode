### 22. Generate Parentheses

Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given *n* = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

#### Solution:

```java
/**
point: recursive way, recursive function input value design
*/
class Solution {
    public List<String> generateParenthesis(int n) {
        ArrayList<String> list = new ArrayList<>();
        backtracing(list, "", 0, 0, n);
        return list;
    }
    
    public void backtracing(ArrayList<String> list, String str, int left, int right, int max) {
        if(str.length() == max*2) {
            list.add(str);
            return;
        }
        
        if(left < max) {
            backtracing(list, str+"(", left+1, right, max);
        }
        if(left > right) {
            backtracing(list, str+")", left, right+1, max);
        }
    }
}
```

