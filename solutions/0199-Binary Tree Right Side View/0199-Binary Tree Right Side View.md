### 0199. 二叉树的右视图

#### 题目地址：https://leetcode-cn.com/problems/binary-tree-right-side-view/

给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

**示例:**

```
输入: [1,2,3,null,5,null,4]
输出: [1, 3, 4]
解释:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
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
    List<Integer> res = new ArrayList<>();
    Queue<TreeNode> queue = new LinkedList<>();
    public List<Integer> rightSideView(TreeNode root) {
        if(root == null) return res;
        queue.offer(root);
        helper();
        return res;
    }
    public void helper(){
        while(!queue.isEmpty()){
            int len = queue.size();
            // 找层次遍历的最后一个
            for(int i = 0; i < len; i++){
                TreeNode temp = queue.poll();
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                if(i == len - 1) res.add(temp.val);
            }
        }
    }
}
```

