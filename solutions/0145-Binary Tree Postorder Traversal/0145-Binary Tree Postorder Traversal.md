### 题目地址：https://leetcode-cn.com/problems/binary-tree-postorder-traversal/

给定一个二叉树，返回它的 **后序** 遍历。

**示例:**

``` java
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
```

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？

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
    List<Integer> res = new ArrayList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        dfs(root);
        return res;
    }

    public void dfs(TreeNode root){
        if(root == null) return;
        // 左
        dfs(root.left);
        // 右
        dfs(root.right);
        // 根
        res.add(root.val);
    }
}
```

**进阶-迭代法：**

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        // 注意这里的栈存的是ThreeNode，而不是Integer
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        // p记录的是前一个节点
        TreeNode p = null;
        while(!stack.isEmpty() || cur != null){
            // 一直往左压栈
            while(cur != null){
                stack.push(cur);
                cur = cur.left;
            }
            // 注意这里是peek
            cur = stack.peek();
            // 这里有两个条件
            if(cur.right == null || cur.right == p){
                res.add(cur.val);
                stack.pop();
                p = cur;
                cur = null;
            // 往右走
            }else cur = cur.right;
        }
        return res;
    }

}
```

**解释：**

1. **p**：记录的是前一个节点，注意这个前一个节点是指**后序遍历序列**的前一个
2. `if(cur.right == null || cur.right == p)`，这里判断的是是否需要回溯（也就是是否右边的都被遍历过了），但是右子树的走过了的状态分为2种类型：
   - 被遍历过，有右子树：也就是左右被走过了，现在只需要操作这个“中”就行了，所以`cur.right == p`，
   - 右边为空：所以是`cur.right == null`
   - 注这里是把`cur.right == null`放在了前面，也就是先判断右子树是否为空，这个小细节需要注意
3. `cur = null;和`while(cur != null)`是搭配使用的
4. `cur = stack.peek();`，这里一定不能是pop，因为如果有右子树没有访问的话，应该把右子树压栈，当前这个作为根应该最后被访问，所以不能出栈

