### 题目地址：https://leetcode-cn.com/problems/search-in-a-binary-search-tree/
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
    public TreeNode searchBST(TreeNode root, int val) {
        // 当到了最下层或者找到时返回
        if(root == null || root.val == val) return root;
        // 注意题目是二叉搜索树
        return root.val > val ? searchBST(root.left, val) : searchBST(root.right, val);
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
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        if root == None or root.val == val:
            return root
        if root.val > val:
            return self.searchBST(root.left, val)
        else:
            return self.searchBST(root.right, val)
```
