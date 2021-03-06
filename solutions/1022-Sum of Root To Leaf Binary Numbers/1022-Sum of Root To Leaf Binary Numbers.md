### 题目地址：https://leetcode-cn.com/problems/sum-of-root-to-leaf-binary-numbers/
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
    public int sumRootToLeaf(TreeNode root) {
        if(root == null) return 0;
        // 每一次递归到这里都 % 一次
        int mod = root.val % 1000_000_007;
        if(root.left == null && root.right == null) return mod;
        // 其实是同一层的叶子，权重相等
        // << 1代表每次扩大2倍，不断扩大这个数
        // 会不断改变节点中的值
        if(root.left != null) root.left.val += mod << 1;
        if(root.right != null) root.right.val += mod << 1;

        // 最终返回的是相加的结果
        return (sumRootToLeaf(root.left) + sumRootToLeaf(root.right)) % 1000_000_007;
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
    def sumRootToLeaf(self, root: TreeNode) -> int:
        if root == None:
            return 0
        mod = root.val % 1000_000_007
        if root.left == None and root.right == None:
            return mod
        if root.left != None:
            root.left.val += mod << 1
        if root.right != None:
            root.right.val += mod << 1
        return (self.sumRootToLeaf(root.left) + self.sumRootToLeaf(root.right)) % 1000_000_007
```
