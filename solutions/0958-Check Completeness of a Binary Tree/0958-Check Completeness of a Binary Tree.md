### 0958. 二叉树的完全性检验

#### https://leetcode-cn.com/problems/check-completeness-of-a-binary-tree/

给定一个二叉树，确定它是否是一个完全二叉树。

百度百科中对完全二叉树的定义如下：

若设二叉树的深度为 h，除第 h 层外，其它各层 (1～h-1) 的结点数都达到最大个数，第 h 层所有的结点都连续集中在最左边，这就是完全二叉树。（注：第 h 层可能包含 1~ 2h 个节点。）

 

**示例 1：**

![img](complete-binary-tree-1.png)

```
输入：[1,2,3,4,5,6]
输出：true
解释：最后一层前的每一层都是满的（即，结点值为 {1} 和 {2,3} 的两层），且最后一层中的所有结点（{4,5,6}）都尽可能地向左。
```

**示例 2：**

![img](complete-binary-tree-2.png)

```
输入：[1,2,3,4,5,null,7]
输出：false
解释：值为 7 的结点没有尽可能靠向左侧。
```

**提示：**

1.  树中将会有 1 到 100 个结点。

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
    Queue<TreeNode> queue = new LinkedList<>();
    public boolean isCompleteTree(TreeNode root) {
        queue.offer(root);
        return dfs(root);
    }
    // 层序遍历
    public boolean dfs(TreeNode node){
        // 这是停止标志
        int sign = 0;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode temp = queue.poll();
                if(temp.left == null) sign = -1;
                else{
                    if(sign == -1) return false;
                    else queue.offer(temp.left);
                }
                if(temp.right == null) sign = -1;
                else{
                   if(sign == -1) return false; 
                   else queue.offer(temp.right);
                } 
            }
        }
        return true;
    }
}
```

解释：

- 思路很简单：使用层次遍历，当遇到空节点时，设置停止标志，只要以后再遇到非空结点，那么就不是完全二叉树