### 题目地址：https://leetcode-cn.com/problems/univalued-binary-tree/
### Java
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
    public boolean isUnivalTree(TreeNode root) {
        // 走到了最底层，代表中途没有false，直接return true
        if(root == null) return true;
        // 以当前节点为参考点，只要有左右孩子，就比较值，false从这里产生
        if(root.left != null && root.left.val != root.val) return false;
        if(root.right != null && root.right.val != root.val) return false;
        // 判断左右子树
        return isUnivalTree(root.right) && isUnivalTree(root.left);
    }
}
```
---

### Python3
``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isUnivalTree(self, root: TreeNode) -> bool:
        if root == None: 
            return True
        if root.left != None and root.left.val != root.val:
            return False
        if root.right != None and root.right.val != root.val:
            return False
        return self.isUnivalTree(root.left) and self.isUnivalTree(root.right)
```
