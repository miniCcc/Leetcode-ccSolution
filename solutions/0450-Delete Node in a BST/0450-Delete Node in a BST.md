### 0450. 删除二叉搜索树中的节点

#### 题目地址：https://leetcode-cn.com/problems/delete-node-in-a-bst/

给定一个二叉搜索树的根节点 root 和一个值 key，删除二叉搜索树中的 key 对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

- 首先找到需要删除的节点；

- 如果找到了，删除它。

说明： 要求算法时间复杂度为 O(h)，h 为树的高度。

**示例:**

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

给定需要删除的节点值是 3，所以我们首先找到 3 这个节点，然后删除它。

一个正确的答案是 [5,4,6,2,null,null,7], 如下图所示。

    5
   / \
  4   6
 /     \
2       7

另一个正确答案是 [5,2,6,null,4,null,7]。

    5
   / \
  2   6
   \   \
    4   7
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
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root == null) return null;
        // 找到
        if(root.val == key){
            // 欲删除的节点没有左子树，删除结点，使用右孩子补位
            if(root.left == null) return root.right;
            // 欲删除的节点没有右子树，删除结点，使用左孩子补位
            if(root.right == null) return root.left;
            if(root.left != null && root.right != null){
                // 找到右侧最小结点，但是其实也可以找左孩子的最大值
                TreeNode node = getMin(root.right);
                // 交换值
                root.val = node.val;
                // 删除结点
                root.right = deleteNode(root.right, node.val);
            }
        }else if(root.val < key){
            root.right = deleteNode(root.right, key);
        }else{
            root.left = deleteNode(root.left, key);
        }
        return root;
    }
    // 找最小值的节点，因为是搜索树，则一直往左走就行
    public TreeNode getMin(TreeNode node){
        while(node.left != null){
            node = node.left;
        }
        return node;
    }
}
```

题目已经给出明示：先找到需要删除的节点，然后执行删除操作（也就是找到需要顶替它的节点，交换值，然后把顶替它的节点删除）