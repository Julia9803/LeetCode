### 383. Ransom Note

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false. 

Each letter in the magazine string can only be used once in your ransom note.

**Note:**
You may assume that both strings contain only lowercase letters.

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

#### Solution:

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int t = 0;
        for(char c: ransomNote.toCharArray()) {
            t = magazine.indexOf(c);
            if(t != -1) {
                magazine = magazine.substring(0,t) + magazine.substring(t+1);
            } else 
                return false;
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] map = new int[26];
        for(char c: magazine.toCharArray()) {
            map[c-'a']++;
        }
        for(char r: ransomNote.toCharArray()) {
            if(--map[r-'a'] < 0) return false;
        }
        return true;
    }
}
```

##### Date 2020.5.3