### 438. Find All Anagrams in a String(Amazon)

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```



**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

#### Solution:

```java
// slide window use hashmap
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        int left = 0, right = 0;
        int meet = p.length();
        Map<Character,Integer> map = new HashMap<>(); // char, frequency
        List<Integer> res = new ArrayList<>();
        
        for(char c: p.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        
        while(right < s.length()) {
            char r = s.charAt(right);
            char l = s.charAt(left);
            if(map.containsKey(r)) {
                map.put(r, map.get(r) - 1);
                if(map.get(r) >= 0) meet--;
            }
            
            if(right - left == p.length() - 1) {
                if(meet == 0) res.add(left);
                if(map.containsKey(l)) {
                    map.put(l, map.get(l) + 1);
                    if(map.get(l) > 0) meet++;
                }
                left++;
            }
            right++;
        }
        return res;
    }
}
```

```java
// slide window use array
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        int left = 0, right = 0;
        int meet = p.length();
        int[] map = new int[256]; // char, frequency
        List<Integer> res = new ArrayList<>();
        
        for(char c: p.toCharArray()) {
            map[c]++;
        }
        
        while(right < s.length()) {
            char r = s.charAt(right);
            char l = s.charAt(left);
            if(map[r] > 0) meet--;
            map[r]--;
            
            if(right - left == p.length() - 1) {
                if(meet == 0) res.add(left);
                if(map[l] >= 0) meet++;
                map[l]++;
                left++;
            }
            right++;
        }
        return res;
    }
}
```

##### Date 2020.5.18

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        char[] arr1 = s.toCharArray();
        char[] arr2 = p.toCharArray();
        int len1 = arr1.length;
        int len2 = arr2.length;
        if(len1 < len2) return res;
        
        char[] count1 = new char[256];
        char[] count2 = new char[256];
        int i;
        for(i = 0;i < len2;i++) {
            count1[arr1[i]]++;
            count2[arr2[i]]++;
        }
        if(Arrays.equals(count1, count2)) {
            res.add(i-len2);
        }
        // slide window
        for(i = len2;i < len1;i++) {
            count1[arr1[i]]++;
            count1[arr1[i-len2]]--;
            if(Arrays.equals(count1, count2)) {
                res.add(i-len2+1);
            }
        }
        return res;
    }
}
```

##### Date 2020.8.25