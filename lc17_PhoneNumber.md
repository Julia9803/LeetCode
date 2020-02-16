### 17. Letter Combinations of a Phone Number

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example:**

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

#### Solution:

```java
/**
Think of n nums has each output String in n length, so iterate result list,
if peek String's length equals iterator num, (first round 0), pop the item in result list,
then combine each string in new phonenumber mapping with it.

point1: set a mapping list of Strings for each integer in input String.
point2: FIFO LinkedList BFS
point3: judge if String length in result list equals iterate number
**/
class Solution {
    public List<String> letterCombinations(String digits) {
        LinkedList<String> res = new LinkedList<>();
        if(digits.length() == 0) return res;
        String[] mapping = {"0","1","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        res.add("");
        for(int i = 0;i<digits.length();i++) {
            int t = Character.getNumericValue(digits.charAt(i));
            while(res.peek().length() == i) {
                String s = res.remove();
                for(char c: mapping[t].toCharArray()) {
                    res.add(s+c);
                }
            }
        }
        return res;
    }
}
```

##### Date 2020.2.16