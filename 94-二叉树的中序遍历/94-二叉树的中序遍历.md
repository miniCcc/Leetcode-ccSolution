### 题目地址：https://leetcode-cn.com/problems/binary-tree-inorder-traversal/

给定一个二叉树，返回它的中序 遍历。

**示例:**

输入: [1,null,2,3]<br>
   1<br>
   &nbsp; \ <br>
    &nbsp;&nbsp; 2<br>
    / <br>
  3<br>

输出: [1,3,2] <br>

进阶: 递归算法很简单，你可以通过迭代算法完成吗？

---

### Java

**递归**
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
    List<Integer> res = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        helper(root);
        return res;
    }

    public void helper(TreeNode root){
        if(root == null) return;
        // 中序：左中右
        helper(root.left);
        res.add(root.val);
        helper(root.right);
    }
}
```

**迭代**

中序遍历：左中右，这里没有明显的体现出打印 中 的过程，但是可以看成 左中|右，中间这个结点对于他的父母结点来说，是父母结点的最左边的结点，在第二层while中寻找到


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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        // 注意不是 &&，而是 ||
        while(root != null || !stack.empty()){
            // 使指向最左边的结点
            while(root != null){
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            res.add(root.val);
            root = root.right;
        }
        return res;
    }
}
```


