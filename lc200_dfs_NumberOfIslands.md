### 200. Number of Islands

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```

#### Solution:

```java
class Solution {
    private int x = 0, y = 0;
    private char[][] g;
    
    public int numIslands(char[][] grid) {
        int res = 0;
        x = grid.length;
        if(x == 0) return 0;
        y = grid[0].length;
        g = grid;
        for(int i = 0;i < x;i++) {
            for(int j = 0;j < y;j++) {
                if(g[i][j] == '1') {
                    dfs(i,j);
                    res++;
                }
            }
        }
        return res;
    }
    
    public void dfs(int i, int j) {
        if(i < 0 || i >= x || j < 0 || j >= y || g[i][j] != '1') return;
        g[i][j] = 0;
        dfs(i + 1, j);
        dfs(i - 1, j);
        dfs(i, j + 1);
        dfs(i, j - 1);
    }
}
```

##### Date 2020.4.17