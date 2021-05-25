### 0538. 把二叉搜索树转换为累加树

#### 题目地址：https://leetcode-cn.com/problems/convert-bst-to-greater-tree/

给出二叉 搜索 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 node 的新值等于原树中大于或等于 `node.val `的值之和。

提醒一下，二叉搜索树满足下列约束条件：

- 节点的左子树仅包含键 小于 节点键的节点。
- 节点的右子树仅包含键 大于 节点键的节点。
- 左右子树也必须是二叉搜索树。

**注意：**本题和 1038: https://leetcode-cn.com/problems/binary-search-tree-to-greater-sum-tree/ 相同

**示例 1：**

<img src="tree.png" alt="img" style="zoom: 80%;" />

```
输入：[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
```

**示例 2：**

```
输入：root = [0,null,1]
输出：[1,null,1]
```

**示例 3：**

```
输入：root = [1,0,2]
输出：[3,3,2]
```

**示例 4：**

```
输入：root = [3,2,4,1]
输出：[7,9,4,10]
```

**提示：**

- 树中的节点数介于 `0` 和 `104` 之间。
- 每个节点的值介于 `-104` 和 `104` 之间。
- 树中的所有值 **互不相同** 。
- 给定的树为二叉搜索树。

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
    int sumAll = 0;
    int prevalSum = 0;
    public TreeNode convertBST(TreeNode root) {
        getsumAll(root);
        helper(root);
        return root;
    }
    public void getsumAll(TreeNode node){
        if(node == null) return;
        getsumAll(node.left);
        sumAll += node.val;
        getsumAll(node.right);
    }
    // 中序遍历
    public void helper(TreeNode node){
        if(node == null) return;
        helper(node.left);
        int temp = node.val;
        node.val = sumAll - prevalSum;
        prevalSum += temp;
        helper(node.right);
    }
}
```

思路：先遍历一遍树，得到所有结点值的累加和，因为是二叉搜索树，再按照中序遍历（有序），使用一个变量记录之前的结点的和，用得到的所有节点值累加和减去当前节点之前的累加和即可

还有第二种解法：

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
    int prevalSum = 0;
    public TreeNode convertBST(TreeNode root) {
        if(root != null){
            convertBST(root.right);
            root.val += prevalSum;
            prevalSum = root.val;
            convertBST(root.left);
            return root;
        }
        return null;
    }
}
```

因为BST中序遍历会得到一个从小到大的有序序列，那么其实可以反过来遍历（右中左），那么会得到一个降序的序列，则只需要使用一个变量来不断记录累加，那么 >= 当前节点的和就是我们设定变量的值