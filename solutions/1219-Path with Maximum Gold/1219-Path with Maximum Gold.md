### 题目地址：https://leetcode-cn.com/problems/path-with-maximum-gold/

你要开发一座金矿，地质勘测学家已经探明了这座金矿中的资源分布，并用大小为 m * n 的网格 grid 进行了标注。每个单元格中的整数就表示这一单元格中的黄金数量；如果该单元格是空的，那么就是 0。

为了使收益最大化，矿工需要按以下规则来开采黄金：

- 每当矿工进入一个单元，就会收集该单元格中的所有黄金。
- 矿工每次可以从当前位置向上下左右四个方向走。
- 每个单元格只能被开采（进入）一次。
- 不得开采（进入）黄金数目为 0 的单元格。
- 矿工可以从网格中 任意一个 有黄金的单元格出发或者是停止。

**示例 1：**

``` java
输入：grid = [[0,6,0],[5,8,7],[0,9,0]]
输出：24
解释：
[[0,6,0],
 [5,8,7],
 [0,9,0]]
一种收集最多黄金的路线是：9 -> 8 -> 7。
```

**示例 2：**

``` java
输入：grid = [[1,0,7],[2,0,6],[3,4,5],[0,3,0],[9,0,20]]
输出：28
解释：
[[1,0,7],
 [2,0,6],
 [3,4,5],
 [0,3,0],
 [9,0,20]]
一种收集最多黄金的路线是：1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7。
```

**提示：**

- 1 <= grid.length, grid[i].length <= 15
- 0 <= grid[i][j] <= 100
- 最多 25 个单元格中有黄金。

---

**Java**

``` java
class Solution {
    int sum = 0;
    // 定义4个方向：上、下、左、右
    int[][] direction = new int[][]{{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    public int getMaximumGold(int[][] grid) {
        // 定义一个二维数组，来判断是否走过这条路
        boolean[][] visited = new boolean[grid.length][grid[0].length];
         for(int i = 0; i < grid.length; i++){
             for(int j = 0; j < grid[i].length; j++){
                 if(grid[i][j] != 0){
                     // 做选择
                     visited[i][j] = true;
                     dfs(grid, i, j, visited, 0);
                     // 撤销选择
                     visited[i][j] = false;
                 }
             }
         }
         return sum;
    }
    
    public void dfs(int[][] grid, int rowidx, int colidx, boolean[][] visited, int sumtemp){
        // 走到边界时走不动了，则应该返回
        // 注意最后的 grid[rowidx][colidx] == 0,有时候不仅仅是走到边界走不动了，还有可能是遇到0的时候，也走不动了
        if(rowidx < 0 || rowidx >= grid.length || colidx < 0 || colidx >= grid[0].length || grid[rowidx][colidx] == 0){
            return;
        }
        sumtemp += grid[rowidx][colidx];
        // 注意这里，sum不能写在上面if的判断条件里，因为有可能会存在走完每一个格子的情况，比如：
        // [[1,6,1],[5,8,7],[1,9,1]]
        sum = Math.max(sumtemp, sum);
        for(int i = 0; i < 4; i++){
            int new_rowidx = rowidx + direction[i][0];
            int new_colidx = colidx + direction[i][1];
            // 判断是否越界以及是都被走过
            if(new_rowidx >= 0 && new_rowidx < grid.length && new_colidx >= 0 && new_colidx < grid[0].length && !visited[new_rowidx][new_colidx] && grid[new_rowidx][new_colidx] != 0){
                // 做选择
                visited[new_rowidx][new_colidx] = true;
                dfs(grid, new_rowidx, new_colidx, visited, sumtemp);
                // 撤销选择
                visited[new_rowidx][new_colidx] = false;
            }
        }

    }
}
```

**解释：**

- 本题和我昨天刷的题很类似，可以去搜索 0079，标准的一个模板答题