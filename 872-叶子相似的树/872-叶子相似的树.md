### 题目地址：https://leetcode-cn.com/problems/leaf-similar-trees/
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
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        String str1 = helper(root1, "");
        String str2 = helper(root2, "");
        return str1.equals(str2);
    }
    public String helper(TreeNode root, String str){
        if(root == null) return str;
        // 判断当前是否是叶节点，需要判断左右两侧
        if(root.right == null && root.left == null) str += root.val;
        // A + B， A B的顺序不能反
        return helper(root.left, str) + helper(root.right, str);
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
    def leafSimilar(self, root1: TreeNode, root2: TreeNode) -> bool:
        str1 = self.helper(root1, '')
        str2 = self.helper(root2, '')
        return str1 == str2

    def helper(self, root: TreeNode, mystr: str) -> str:
        if root == None:
            return mystr
        if root.left == None and root.right == None:
            mystr += str(root.val)
        return self.helper(root.left, mystr) + self.helper(root.right, mystr)
```
