### 题目地址：https://leetcode-cn.com/problems/binary-tree-paths/

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

```
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

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
    List<String> res = new ArrayList<>();
    public List<String> binaryTreePaths(TreeNode root) {
        StringBuilder str = new StringBuilder();
        dfs(root, str);
        return res;
    }
    public void dfs(TreeNode node, StringBuilder str){
        if(node == null) return;
        // 注意这个是写在下面这个if前面的
        str.append(node.val);
        if(node.left == null && node.right == null){
            res.add(str.toString());
            return;
        }
        dfs(node.left, new StringBuilder(str).append("->"));
        dfs(node.right, new StringBuilder(str).append("->"));
    }
}
```
