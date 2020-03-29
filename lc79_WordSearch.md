### 79. Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

 

**Constraints:**

- `board` and `word` consists only of lowercase and uppercase English letters.
- `1 <= board.length <= 200`
- `1 <= board[i].length <= 200`
- `1 <= word.length <= 10^3`

#### Solution:

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length, n = board[0].length;
        char[] w = word.toCharArray();
        for(int i = 0;i < m;i++) {
            for(int j = 0;j < n;j++) {
                if(dfs(board, w, 0, i, j))
                    return true;
            }
        }
        return false;
    }
    
    private boolean dfs(char[][] board, char[] w, int d, int i, int j) {
        if(i < 0 || j < 0 || i == board.length || j == board[0].length || board[i][j] != w[d])
            return false;
        if(d == w.length - 1) return true;
        char tmp = board[i][j];
        board[i][j] = 0;
        boolean find = dfs(board, w, d + 1, i + 1, j)
            || dfs(board, w, d + 1, i - 1, j)
            || dfs(board, w, d + 1, i, j + 1)
            || dfs(board, w, d + 1, i, j - 1);
        board[i][j] = tmp;
        return find;
    }
}
```

##### Date 2020.3.29