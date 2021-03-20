### 0513. 找树左下角的值

#### 题目地址：https://leetcode-cn.com/problems/find-bottom-left-tree-value/

给定一个二叉树，在树的最后一行找到最左边的值。

**示例 1:**

```
输入:

    2
   / \
  1   3

输出:
1
```

**示例 2:**

```
输入:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

输出:
7
```

**注意:** 您可以假设树（即给定的根节点）不为 **NULL**。

---

**Java**

``` java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int maxHeight = -1;
    TreeNode res = null;
    public int findBottomLeftValue(TreeNode root) {
        dfs(root, 0);
        return res.val;
    }
    // 中序遍历
    public void dfs(TreeNode node, int height){
        if(node == null)  return;
        dfs(node.left, height + 1);
        // 用height代表层数，不断更新res节点
        if(height > maxHeight){
            maxHeight = height;
            res = node;
        }
        dfs(node.right, height + 1);
    }
}
```



