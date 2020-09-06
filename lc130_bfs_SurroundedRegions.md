### 130. Surrounded Regions

Given a 2D board containing `'X'` and `'O'` (**the letter O**), capture all regions surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example:**

```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:

```
X X X X
X X X X
X X X X
X O X X
```

**Explanation:**

Surrounded regions shouldn’t be on the border, which means that any `'O'` on the border of the board are not flipped to `'X'`. Any `'O'` that is not on the border and it is not connected to an `'O'` on the border will be flipped to `'X'`. Two cells are connected if they are adjacent cells connected horizontally or vertically.

#### Solution:

```
0 0 0 0 
0 1 1 0 
0 0 1 0 
0 2 0 0 
1 true 2 false
```

```java
class Solution {
    int landno, m, n;
    public void solve(char[][] board) {
        m = board.length;
        if(m == 0) return;
        n = board[0].length;
        landno = 0; // number of land
        int[][] mark = new int[m][n]; // judge if region is marked with landno
        boolean[] surrounded = new boolean[m*n+1]; // save if region index is surrouned 
        Arrays.fill(surrounded, true);
        
        for(int i = 0;i < m;i++) {
            for(int j = 0;j < n;j++) {
                if(board[i][j] == 'O' && mark[i][j] == 0) {
                    landno++;
                    bfs(board, i, j, surrounded, mark);
                }
            }
        }
        
        // // print mark
        // for(int i = 0;i < m;i++) {
        //     for(int j = 0;j < n;j++) {
        //         System.out.print(mark[i][j] + " ");
        //     }
        //     System.out.println();
        // }
        // // print surrounded
        // for(int i = 1;i < 3;i++) {
        //     System.out.print(i + " " + surrounded[i] + " ");
        // }
        
        for(int i = 0;i < m;i++) {
            for(int j = 0;j < n;j++) {
                if(board[i][j] == 'O' && surrounded[mark[i][j]]) {
                    board[i][j] = 'X';
                }
            }
        }
    }
    public void bfs(char[][] board, int i, int j, boolean[] surrounded, int[][] mark) {
        int[] ox = {0, 0, 1, -1};
        int[] oy = {1, -1, 0, 0};
        mark[i][j] = landno;
        Stack<Integer> sx = new Stack<Integer>();
        Stack<Integer> sy = new Stack<Integer>();
        sx.push(i);
        sy.push(j);
        while(sx.size() != 0) {
            int x = sx.pop();
            int y = sy.pop();
            // region is on the corner and not surrounded
            if(x == m - 1 || x == 0 || y == n - 1 || y == 0) {
                surrounded[landno] = false;
            }
            for(int k = 0;k < 4;k++) {
                int nx = x + ox[k];
                int ny = y + oy[k];
                if(nx >= 0 && (nx <= m - 1) && ny >= 0 && (ny <= n - 1) 
                   && board[nx][ny] == 'O' && mark[nx][ny] == 0) {
                    mark[nx][ny] = landno;
                    sx.push(nx);
                    sy.push(ny);
                }
            }
        }
    }
}
```

##### Date 2020.9.6