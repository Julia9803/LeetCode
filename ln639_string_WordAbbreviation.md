###  639. Word Abbreviation

Given an array of n distinct non-empty strings, you need to generate **minimal** possible abbreviations for every word following rules below.

1. Begin with the first character and then the number of characters abbreviated, which followed by the last character.
2. If there are any conflict, that is more than one words share the same abbreviation, a longer prefix is used instead of only the first character until making the map from word to abbreviation become unique. In other words, a final abbreviation cannot map to more than one original words.
3. If the abbreviation doesn't make the word shorter, then keep it as original.

### Example

**Example 1:**

```
Input:
["like","god","internal","me","internet","interval","intension","face","intrusion"]
Output:
["l2e","god","internal","me","i6t","interval","inte4n","f2e","intr4n"]
```

**Example 2:**

```
Input:
["where","there","is","beautiful","way"]
Output:
["w3e","t3e","is","b7l","way"]
```

### Notice

1. Both n and the length of each word will not exceed 400.
2. The length of each word is greater than 1.
3. The words consist of lowercase English letters only.
4. The return answers should be in the same order as the original array.

#### Solution:

```java
public class Solution {
    /**
     * @param dict: an array of n distinct non-empty strings
     * @return: an array of minimal possible abbreviations for every word
     */
    public String[] wordsAbbreviation(String[] dict) {
        // write your code here
        Map<String, Integer> map = new HashMap<String, Integer>(); // abbr, pos
        String[] res = new String[dict.length];
        for(int i = 0;i < dict.length;i++) {
            res[i] = getAbbr(dict[i], 0);
            map.put(res[i], map.getOrDefault(res[i], 0) + 1);
        }
        int p = 0;
        int status = 0; // 0: no replicate; 1: has replicate
        while(true) {
            p++;
            status = 0;
            for(int i = 0;i < dict.length;i++) {
                if(map.get(res[i]) > 1) {
                    status = 1;
                    res[i] = getAbbr(dict[i], p);
                    map.put(res[i], map.getOrDefault(res[i], 0) + 1);
                }
            }
            if(status == 0) break;
        }
        return res;
    }
    private String getAbbr(String s, int p) {
        int len = s.length();
        if(len <= (3 + p)) return s;
        return s.substring(0, p+1) + "" + (len-2-p) + "" + s.charAt(len-1);
    }
}
```

##### Date 2020.8.23