### 题目地址：https://leetcode-cn.com/problems/balanced-binary-tree/

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

**示例 1：**

![img](balance_1.jpg)

``` 
输入：root = [3,9,20,null,null,15,7]
输出：true
```

**示例 2：**

![img](balance_2.jpg)

```
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
```

**示例 3：**

```
输入：root = []
输出：true
```

**提示：**

- 树中的节点数在范围 [0, 5000] 内
- -104 <= Node.val <= 104

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
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        if(root.left == null && root.right == null) return true;
        // 先判断根节点的左右子节点是不是平衡的
        if(Math.abs(dfs(root.left) - dfs(root.right)) > 1) return false;
        // 然后判断每个结点是不是平衡的
        return isBalanced(root.left) && isBalanced(root.right);
    }

    public int dfs(TreeNode node){
        if(node == null) return 0;
        int leftlen = dfs(node.left) + 1;
        int rightlen = dfs(node.right) + 1;
        // 返回最深的高度
        return leftlen > rightlen ? leftlen : rightlen;
    }
    
}
```

但是这样的话有一个很大的缺点，也就是会重复得计算（自顶向下），建议直接看https://leetcode-cn.com/problems/balanced-binary-tree/solution/ping-heng-er-cha-shu-by-leetcode-solution/的动图，非常的直观，采用的是自底向下

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
    public boolean isBalanced(TreeNode root) {
        return height(root) >= 0;
    }

    public int height(TreeNode node){
        if(node == null) return 0;
        int leftlen = height(node.left);
        int rightlen = height(node.right);
        // 注意
        if(leftlen == -1 || rightlen == -1 || Math.abs(leftlen - rightlen) > 1) return -1;
        return Math.max(leftlen, rightlen) + 1;
    }
    
}
```

注意：

- 为什么要判断`leftlen == -1 || rightlen == -1`，因为只要发现不平衡，那么整棵树就不可能是平衡的，只需要一直把这个-1传回去即可