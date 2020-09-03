### 205. Isomorphic Strings

Given two strings ***s\*** and ***t\***, determine if they are isomorphic.

Two strings are isomorphic if the characters in ***s\*** can be replaced to get ***t\***.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true
```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false
```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true
```

**Note:**
You may assume both ***s\*** and ***t\*** have the same length.

#### Solution:

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        // left to right
        for(int i = 0;i < s.length();i++) {
            if(!map.containsKey(s.charAt(i))) {
                map.put(s.charAt(i), t.charAt(i));
            }
            if(map.get(s.charAt(i)) != t.charAt(i)) return false;
        }
        HashMap<Character, Character> map1 = new HashMap<Character, Character>();
        // right to left
        for(int i = 0;i < t.length();i++) {
            if(!map1.containsKey(t.charAt(i))) {
                map1.put(t.charAt(i), s.charAt(i));
            }
            if(map1.get(t.charAt(i)) != s.charAt(i)) return false;
        }
        return true;
    }
}
```

##### Date 2020.8.22