### 题目地址：https://leetcode-cn.com/problems/word-search/

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

**示例:**

``` java
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```



**提示：**

- board 和 word 中只包含大写和小写英文字母。
- 1 <= board.length <= 200
- 1 <= board[i].length <= 200
- 1 <= word.length <= 10^3

---

**Java**

``` java
class Solution {
    // 分别代表上、下、左、右
    int[][] direction = new int[][]{{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    public boolean exist(char[][] board, String word) {
        // 初始默认全为false
        boolean[][] visited = new boolean[board.length][board[0].length];
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                if(board[i][j] == word.charAt(0)){
                    visited[i][j] = true;
                    // 及时返回，只要有一个true就应该返回了
                    if(backtrace(board, i, j, word.toCharArray(), 0, visited) == true) return true;
                    visited[i][j] = false;
                }
            }
        }    
        return false;
    }
    public boolean backtrace(char[][] board, int rowidx, int colidx, char[] word, int wordidx, boolean[][] visited){
        // 只要发现不对，立即结束本分支
        if(board[rowidx][colidx] != word[wordidx]) return false;
        if(wordidx == word.length - 1) return true;
        // 不断对4个方向遍历前进
        for(int i = 0; i < 4; i++){
            // 新的row
            int new_rowidx = direction[i][0] + rowidx;
            // 新的col
            int new_colidx = direction[i][1] + colidx;
            // 边界判断和未被访问过判断
            if(new_colidx >=0 && new_colidx < board[0].length && new_rowidx >= 0 && new_rowidx < board.length && !visited[new_rowidx][new_colidx]){
                // 做选择
                visited[new_rowidx][new_colidx] = true;
                // 再次回溯，wordidx+1去匹配下一个，需要及时返回true
                if(backtrace(board, new_rowidx, new_colidx, word, wordidx+1, visited)) return true;
                // 撤销选择
                visited[new_rowidx][new_colidx] = false;
            }
        }
        return false;
    }
}
```

**解释：**

1. `int[][] direction = new int[][]{{-1, 0}, {1, 0}, {0, -1}, {0, 1}};`，分别代表了上下左右四个方向的row和col
2. 对于`boolean[][] visited = new boolean[board.length][board[0].length];`，是用来记录这个是否被访问过，如果word是一个回文串，如果不用visited来判断，那么会返回错误的结果
3. 并没有使用StringBuider来拼串，只需要用一个变量去判断word当前这个字符和board对应的字符是否相等即可，所以设置了三个变量，一个用于记录word里的位置，两个用于定位二维数组
4. 在得到新的rol和col的时候，还是需要重新判断是否越界