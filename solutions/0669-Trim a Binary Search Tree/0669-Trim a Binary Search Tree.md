### 669. 修剪二叉搜索树

#### 题目地址：https://leetcode-cn.com/problems/trim-a-binary-search-tree/

给你二叉搜索树的根节点 `root `，同时给定最小边界`low` 和最大边界 `high`。通过修剪二叉搜索树，使得所有节点的值在`[low, high]`中。修剪树不应该改变保留在树中的元素的相对结构（即，如果没有被移除，原有的父代子代关系都应当保留）。 可以证明，存在唯一的答案。

所以结果应当返回修剪好的二叉搜索树的新的根节点。注意，根节点可能会根据给定的边界发生改变。

**示例 1：**

![img](trim1.jpg)

```
输入：root = [1,0,2], low = 1, high = 2
输出：[1,null,2]
```

**示例 2：**

![img](trim2.jpg)`

```
输入：root = [3,0,4,null,2,null,null,1], low = 1, high = 3
输出：[3,2,null,1]
```

**示例 3：**

```
输入：root = [1], low = 1, high = 2
输出：[1]
```

**示例 4：**

```
输入：root = [1,null,2], low = 1, high = 3
输出：[1,null,2]
```

**示例 5：**

```
输入：root = [1,null,2], low = 2, high = 4
输出：[2]
```

**提示：**

- 树中节点数在范围 [1, 104] 内
- 0 <= Node.val <= 104
- 树中每个节点的值都是唯一的
- 题目数据保证输入是一棵有效的二叉搜索树
- 0 <= low <= high <= 104

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
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) return null;
        // 如果当前结点小于下界，直接将修剪后的右子树替换当前节点并返回
        if (root.val < low) return trimBST(root.right, low, high);
        // 如果当前结点大于上界，直接将修剪后的左子树替换当前节点并返回
        if (root.val > high) return trimBST(root.left, low, high);
        // 如果当前结点不越界，继续往两边扩散寻找第一个越界的结点
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

自己写了一个半成品，只能搞定根节点不变的情况，直接看了官方题解，递归 yyds ! ! ! （黑人问号.jpg）