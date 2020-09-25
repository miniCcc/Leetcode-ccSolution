### 题目地址：https://leetcode-cn.com/problems/maximum-binary-tree/

给定一个不含重复元素的整数数组。一个以此数组构建的最大二叉树定义如下：

二叉树的根是数组中的最大元素。
左子树是通过数组中最大值左边部分构造出的最大二叉树。
右子树是通过数组中最大值右边部分构造出的最大二叉树。
通过给定的数组构建最大二叉树，并且输出这个树的根节点。

 

**示例 ：**

输入：[3,2,1,6,0,5]
输出：返回下面这棵树的根节点：

          6
        /   \
      3       5
       \     / 
        2   0   
         \
          1
 提示：给定的数组的大小在 [1, 1000] 之间。

---

**思路：**

1. 只思考当前这个结点在做什么，不能跳进递归
2. 拿到一个数组，不管是子数组还是原来的一整个数组，都需要找到最大值maxval，作为当前的根节点root
3. 此时需要找root.left，root.right
4. root.left是当前这个值左边的最大值，root.right是当前这个值右边的最大值
5. 对左边和右边循环调用函数（注意：需要用新变量left和right记录子数组的遍历的范围，所以还需要index记录我当前这个值的位置）

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
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return build(nums, 0, nums.length - 1);
    }

    public TreeNode build(int[] nums, int left, int right){
        // 结束条件
        if(left > right) return null;
        
        int max = Integer.MIN_VALUE;
        int index = -1;
        // 遍历数组，找到最大值和最大值的位置
        for(int i = left; i <= right; i++){
            if(nums[i] > max){
                max = nums[i];
                index = i;
            }
        }
        // 构建这个结点与该结点的left和right
        TreeNode root = new TreeNode(max);
        root.left = build(nums, left, index - 1);
        root.right = build(nums, index + 1, right);

        return root;
    }
}
```

