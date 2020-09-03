### 648. Unique Word Abbreviation(Google)

n abbreviation of a word follows the form`<first letter><number><last letter>`. Below are some examples of word abbreviations:

```
a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
```

Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if **no other word** from the dictionary has the same abbreviation.

### Example

**Example1**

```
Input:
[ "deer", "door", "cake", "card" ]
isUnique("dear")
isUnique("cart")
Output:
false
true
Explanation:
Dictionary's abbreviation is ["d2r", "d2r", "c2e", "c2d"].
"dear" 's abbreviation is "d2r" , in dictionary.
"cart" 's abbreviation is "c2t" , not in dictionary.
```

**Example2**

```
Input:
[ "deer", "door", "cake", "card" ]
isUnique("cane")
isUnique("make")
Output:
false
true
Explanation:
Dictionary's abbreviation is ["d2r", "d2r", "c2e", "c2d"].
"cane" 's abbreviation is "c2e" , in dictionary.
"make" 's abbreviation is "m2e" , not in dictionary.
```

Input test data (one parameter per line)How to understand a testcase?

#### Solution:

```java
public class ValidWordAbbr {
    Map<String, Integer> map;
    Map<String, Integer> strs;
    /*
    * @param dictionary: a list of words
    */public ValidWordAbbr(String[] dictionary) {
        // do intialization if necessary
        map = new HashMap<String, Integer>(); // store abbr, times
        strs = new HashMap<String, Integer>(); // store Strings, times
        for(String s: dictionary) {
            // store string times
            if(!strs.containsKey(s)) {
                strs.put(s,1);
            } else {
                strs.put(s, strs.get(s) + 1);
            }
            
            // get abbr
            String abbr = getAbbr(s);
            
            // store abbr times
            if(!map.containsKey(abbr)) {
                map.put(abbr,1);
            } else {
                map.put(abbr, map.get(abbr) + 1);
            }
        }
    }

    /*
     * @param word: a string
     * @return: true if its abbreviation is unique or false
     */
    public boolean isUnique(String word) {
        // write your code here
        String abbr = getAbbr(word);
        if(map.get(abbr) == strs.get(word)) return true;
        return false;
    }
    
    public String getAbbr(String s) {
        String abbr;
        int len = s.length();
        if(len <= 2) abbr = s;
        else {
            abbr = s.charAt(0) + "" + (len-2) + "" + s.charAt(len-1);
        }
        return abbr;
    }
}

/**
 * Your ValidWordAbbr object will be instantiated and called as such:
 * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
 * boolean param = obj.isUnique(word);
 */
```

##### Date 2020.8.26