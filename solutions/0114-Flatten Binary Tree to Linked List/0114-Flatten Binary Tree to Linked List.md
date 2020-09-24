### 题目地址：https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/

给定一个二叉树，原地将它展开为一个单链表。

例如，给定二叉树

      1
     / \
      2   5
     / \   \
    3   4   6
将其展开为：

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

---

**思路：**

1. 先将左右子树拉成一条线
2. 断开左右子树，左子树接在中间结点的右边，原来右子树接在现在右子树的末尾
3. 接在末尾的时候，需要循环找到原来左子树的末尾结点

### Java

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
    public void flatten(TreeNode root) {
        if(root == null) return;

        flatten(root.left);
        flatten(root.right);
        // 后序遍历
        //1. 此时左右已经被拉成一个链条（不用管为什么，问就是递归）
        TreeNode left = root.left;
        TreeNode right = root.right;

        //2. 将左子树作为右子树
        root.left = null;
        root.right = left;

        //3. 将原来的右子树挂在当前右子树的末端
        TreeNode p = root;
        while(p.right != null){
            p = p.right;
        }
        p.right = right;
    }
}
```

<img src="1600936497193031.jpg?raw=true" width="40%" height="40%">