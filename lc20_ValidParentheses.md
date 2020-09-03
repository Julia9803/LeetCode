### 20. Valid Parentheses(Google)

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```

#### Solution:

My solution:

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        char[] arr = s.toCharArray();
        if(s == null) return true;
        HashMap<Character,Character> map = new HashMap<>();
        map.put('(',')');
        map.put('{','}');
        map.put('[',']');
        
        for(char c: arr) {
            if((!stack.empty()) && map.get(stack.peek()) == c) {
                stack.pop();
            } else if(c == '(' || c == '{' || c == '['){
                stack.push(c);
            } else return false;
        }
        return stack.empty();
    }
}
```

Better solution:

```java
class Solution {
    public boolean isValid(String s) {        
        Stack<Character> stack = new Stack<>();
        char[] arr = s.toCharArray();
        for(char c: arr) {
            if(c == '(') stack.push(')');
            else if(c == '{') stack.push('}');
            else if(c == '[') stack.push(']');
            else if(!stack.empty() && c == stack.peek()) stack.pop();
            else return false;  
        }
        return stack.empty();
    }
}
```

##### Date 2020.2.17

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        char[] arr = s.toCharArray();
        for(int i = 0;i < arr.length;i++) {
            if((arr[i] == '(') || (arr[i] == '{') || (arr[i] == '[')) {
                stack.push(arr[i]);
            }
            else if(stack.empty()) return false;
            else if(arr[i] == ')') {
                if(stack.pop() != '(') return false;
            }
            else if(arr[i] == ']') {
                if(stack.pop() != '[') return false;
            }
            else if(arr[i] == '}') {
                if(stack.pop() != '{') return false;
            }
        }
        if(!stack.empty()) return false;
        return true;
    }
}
```

##### Date 2020.8.27