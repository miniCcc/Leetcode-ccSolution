### 0530-二叉搜索树的最小绝对差

#### 题目地址：https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/

给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。

**示例：**

```
输入：

   1
    \
     3
    /
   2

输出：
1

解释：
最小绝对差为 1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。
```

**提示：**

- 树中至少有 2 个节点。
- 本题与 783 https://leetcode-cn.com/problems/minimum-distance-between-bst-nodes/ 相同

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
    int pre = -1;
    int minres = Integer.MAX_VALUE;
    public int getMinimumDifference(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        inOrder(root);
        return minres;
    }

    // 二叉搜索树中序遍历得到有序序列
    public void inOrder(TreeNode node){
        if(node == null) return;
        inOrder(node.left);
        if(pre == -1) pre = node.val;
        else if((node.val - pre) < minres) minres = node.val - pre;
        pre = node.val;
        inOrder(node.right);
    }
}
```

**解释：**

- 首先需要明确的是**线索二叉树中序遍历是一个有序的序列**，则可以很明确的想到一个思路，先记录下来中序遍历序列，然后遍历序列得到最小的那个差值

- 基于上述思路改进一下，其实可以在中序遍历的时候，使用一个变量记录上个结点的值，再使用一个变量记录之前得到的最小差值，边遍历边更新数值，这样就不需要格外的空间开销，也不再需要重新再去遍历一次中序序列

- 题目说和`783题`一样，去翻看了我之前做的答案，贴一下：

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
      private int min = Integer.MAX_VALUE;
      private TreeNode pre = null; //记录前一个节点
      public int minDiffInBST(TreeNode root) {
          zhongxu(root);
          return min;
      }
  	// 从这个命名我就能看出我当时的青涩.....
      public void zhongxu(TreeNode root){
          if(root == null) return;
          zhongxu(root.left);
          if(pre != null){
              min = Math.min(root.val - pre.val, min);
          }
          pre = root;
          zhongxu(root.right);
      }
  }
  ```

  

