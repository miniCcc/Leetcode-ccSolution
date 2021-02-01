### 题目地址：https://leetcode-cn.com/problems/sum-of-left-leaves/

计算给定二叉树的所有左叶子之和。

示例：

      3
     / \
      9  20
        /  \
       15   7
  在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24

---

**Java**

``` java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int sum = 0;
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null) return 0;
        // 这里初值要给1,因为只有根节点的时候不能算
        dfs(root, 1);
        return sum;
    }
    // 这个sign来表示是左孩子还是右孩子
    public void dfs(TreeNode node, int sign){
        if(node.left == null && node.right == null){
             if(sign == 0){
                 sum += node.val;
                 return;
             }
        }
        if(node.left != null) dfs(node.left, 0);
        if(node.right != null) dfs(node.right, 1);
    }
}
```

果然如评论区所说，美好的一天从弱智题开始....，这个题主要是怎么判断是左叶子结点，我用的是sign来实现的，还有如下方式

``` java
class Solution {
    private int sum = 0;
    public int sumOfLeftLeaves(TreeNode root) {
        if(root==null) return 0;
        if(root.left!=null && (root.left.left == null && root.left.right == null)){
            sum += root.left.val;
        }
        sumOfLeftLeaves(root.left);
        sumOfLeftLeaves(root.right);
        return sum;
    }
}
```

