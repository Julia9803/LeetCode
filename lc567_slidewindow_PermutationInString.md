#### 567. Permutation in String

Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

 

**Example 1:**

```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

 

**Constraints:**

- The input strings only contain lower case letters.
- The length of both given strings is in range [1, 10,000].

#### Solution:

```java
// slide window same as 438
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] map = new int[256];
        int len1 = s1.length();
        int len2 = s2.length();
        int start = 0, end = 0;
        int meet = len1;
        for(char c: s1.toCharArray()) 
            map[c]++;
        
        while(end < len2) {
            char startc = s2.charAt(start);
            char endc = s2.charAt(end);
            if(map[endc] > 0) meet--;
            map[endc]--;
            
            if(end - start + 1 == len1) {
                if(meet == 0) return true;
                if(map[startc] >= 0) meet++;
                map[startc]++;
                start++;
            } 
            end++;
        }
        return false;
    }
}
```

```java
// runtime too long
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] map = new int[256];
        int len = s2.length();
        copy(map, s1);
        for(int i = 0;i < len;i++) {
            if(map[s2.charAt(i)] > 0) {
                int j = 0;
                while(j < len && (i + j) < len) {
                    if(map[s2.charAt(i + j)] > 0) {
                        // System.out.println(s2.charAt(i + j));
                        map[s2.charAt(i + j)]--;
                    } else break;
                    j++;
                }
                if(j == s1.length()) return true;
                map = new int[256];
                copy(map, s1);
            }
        }
        return false;
    }
    
    private void copy(int[] map, String s1) {
        for(char c: s1.toCharArray()) 
            map[c]++;
    }
}
```

##### Date 2020.5.22