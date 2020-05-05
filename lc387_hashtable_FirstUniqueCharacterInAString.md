### 387. First Unique Character in a String

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```



**Note:** You may assume the string contain only lowercase letters.

#### Solution:

```java
class Solution {
    public int firstUniqChar(String s) {
        int[] freq = new int[26];
        for(char c: s.toCharArray()) {
            freq[c-'a']++;
        }
        for(int i = 0;i < s.length();i++) {
            if(freq[s.charAt(i) - 'a'] == 1) return i;
        }
        return -1;
    }
}
```

```java
class Solution {
    public int firstUniqChar(String s) {
        Map<Character,Integer> map = new HashMap<>();
        // for(char c: s.toCharArray()) {
        //     if(!map.containsKey(c))
        //         map.put(c,1);
        //     else
        //         map.put(c,map.get(c) + 1);
        // }
        
        // code less and run faster
        for(char c: s.toCharArray()) {
            map.put(c, map.getOrDefault(c,0) + 1); // get(n) if not exist return 0
        }
        for(int i = 0;i < s.length();i++) {
            if(map.get(s.charAt(i)) == 1) return i;
        }
        return -1;
    }
}
```

##### Date 2020.5.5