###  637. Valid Word Abbreviation

Given a **non-empty** string `word` and an abbreviation `abbr`, return whether the string matches with the given abbreviation.

A string such as `"word"` contains only the following valid abbreviations:

```
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```

### Example

**Example 1:**

```
Input : s = "internationalization", abbr = "i12iz4n"
Output : true
```

**Example 2:**

```
Input : s = "apple", abbr = "a2e"
Output : false
```

### Notice

Notice that only the above abbreviations are valid abbreviations of the string `word`. Any other string is not a valid abbreviation of `word`.

#### Solution:

```java
public class Solution {
    /**
     * @param word: a non-empty string
     * @param abbr: an abbreviation
     * @return: true if string matches with the given abbr or false
     */
    public boolean validWordAbbreviation(String word, String abbr) {
        // write your code here
        int p = 0; // word pointer
        int lenw = word.length();
        int lena = abbr.length();
        char[] arrw = word.toCharArray();
        char[] arra = abbr.toCharArray();
        for(int i = 0;i < lena;i++) {
            int num = 0;
            if(arra[i] == '0') return false;
            while(arra[i] >= '0' && arra[i] <= '9') {
                num = 10 * num + arra[i] - '0';
                i++;
                if(i >= lena) break;
            }
            if(num != 0) {
                p += num;
                if(p > lenw) return false;
            }
            if(i == lena && p == lenw) return true;
            if(arra[i] != arrw[p]) return false;
            p++;
        }
        return true;
    }
}
```

##### Date 2020.8.22