### 095-不同的二叉搜索树 II

#### 题目地址：https://leetcode-cn.com/problems/unique-binary-search-trees-ii/

给定一个整数 *n*，生成所有由 1 ... *n* 为节点所组成的 **二叉搜索树** 。

 

**示例：**

```
输入：3
输出：
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

**提示：**

- `0 <= n <= 8`

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
    public List<TreeNode> generateTrees(int n) {
        if(n == 0) return new LinkedList<TreeNode>();
        return helper(1, n);
    }
    // helper的含义是返回所有[start, end]数组成的二叉搜索树
    public List<TreeNode> helper(int start, int end){
        LinkedList<TreeNode> res = new LinkedList<>();
        if(start > end){
            // 没有找到结果，null加入结果集
            res.add(null);
            return res;
        }
        for(int i = start; i <= end; i++){
            // 获取i结点左边所有的可能的二叉搜索树
            List<TreeNode> left = helper(start, i - 1);
            // 获取i结点右边所有的可能的二叉搜索树
            List<TreeNode> right = helper(i + 1, end);
            for(TreeNode l : left){
                for(TreeNode r : right){
                    // 拼上去
                    TreeNode node = new TreeNode(i);
                    node.left = l;
                    node.right = r;
                    // 加入结果集
                    res.add(node);
                }
            }
        }
        return res;
    }
}
```

