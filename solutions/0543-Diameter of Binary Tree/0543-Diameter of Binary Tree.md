### 0543-二叉树的直径

#### 题目地址：https://leetcode-cn.com/problems/diameter-of-binary-tree/

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。



**示例 :**
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。



**注意：**两结点之间的路径长度是以它们之间边的数目表示。

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
    int max = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        dfs(root);
        return max;
    }
    public int dfs(TreeNode node){
        // 这里为什么不返回 -1 ?  因为这个放回值是左右子树最大高度，这个空节点没有左右子树
        if(node == null) return 0;
        int leftheight = dfs(node.left);
        int rightheight = dfs(node.right);
        // 是否更新最大值
        if(leftheight + rightheight > max) max = leftheight + rightheight;
        // 返回值是当前这个结点的左右最大的高度，注意需要+1
        return Math.max(leftheight, rightheight) + 1;
    }
}
```

**解释：**

- 因为这个路径可以不穿过根节点，所以本题可以转换为计算每个结点的左右最大高度之和，求最大值

