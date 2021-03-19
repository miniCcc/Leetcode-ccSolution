#### 0098. 验证二叉搜索树

#### 题目地址：https://leetcode-cn.com/problems/validate-binary-search-tree/

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含小于当前节点的数。
- 节点的右子树只包含大于当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

**示例 1:**

```
输入:
    2
   / \
  1   3
输出: true
```

**示例 2:**

```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
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
    TreeNode pre = null;
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        if(isValidBST(root.left)){
            if(pre == null || pre.val < root.val){
                pre = root;
                return isValidBST(root.right);
            }
        }
        return false;
    }
}
```

另一种写法：

``` java
class Solution {
    long pre = Long.MIN_VALUE; // 记录上一个节点的值，初始值为Long的最小值

    public boolean isValidBST(TreeNode root) {
        return inorder(root);
    }

    // 中序遍历
    private boolean inorder(TreeNode node) {
        if(node == null) return true;
        // 左
        boolean l = inorder(node.left);
        if(node.val <= pre) return false;
        pre = node.val;
        // 右
        boolean r = inorder(node.right);
        return l && r;
    }
}
```

两种都是利用了，二叉搜索树中序遍历一定是一个有序的序列

