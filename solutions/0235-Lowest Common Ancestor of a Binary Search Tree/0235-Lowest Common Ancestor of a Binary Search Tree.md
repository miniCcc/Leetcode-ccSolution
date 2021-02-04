### 题目地址：https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]

![img](binarysearchtree_improved.png)

**示例 1:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

**示例 2:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```

**说明:**

- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉搜索树中。

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
    TreeNode res;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        dfs(p, q, root);
        return res;
    }

    public void dfs(TreeNode p, TreeNode q, TreeNode root){
        // 走到了叶子结点，需要返回
        if(root.left == null && root.right == null) return;
        // 如果p和q分别在当前根节点的两侧，直接返回当前根节点
        if((p.val < root.val && q.val > root.val) || (q.val < root.val && p.val > root.val)){
            res = root;
            return;
        }
        // 如果p和q某一个是root，返回root
        if(p.val == root.val || q.val == root.val){
            res = root;
            return;
        }
        // 排除上面的情况，那么此时就是p和q在同侧了，所以只写了一个的判断条件
        if(p.val < root.val) dfs(p, q, root.left);
        if(p.val > root.val) dfs(p, q, root.right);
    }
}
```

 **解释：**

- 其实有两个if是可以合并的，但是为了阅读方便，写成了2个
- 首先需要明确的是这里给出的是二叉搜索树（并不是那种无序的二叉树），因此我们可以根据值的大小直接确定在右子树还是在左子树

