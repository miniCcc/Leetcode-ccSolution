### 0501. 二叉搜索树中的众数

#### 题目地址：https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/

给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

- 结点左子树中所含结点的值小于等于当前结点的值
- 结点右子树中所含结点的值大于等于当前结点的值
- 左子树和右子树都是二叉搜索树

**例如：**
给定 BST [1,null,2,2],

```
   1
    \
     2
    /
   2
```

返回[2].   

**提示：**如果众数超过1个，不需考虑输出顺序

**进阶：**你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）

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
    // pre记录上一个值，用来和当前的值进行判断是否相等
    // count记录当前这个值的出现次数
    // maxcount记录之前的众数出现的次数
    int pre = 0;
    int count = 0;
    int maxcount = 0;
    List<Integer> list = new ArrayList<>();
    public int[] findMode(TreeNode root) {
        InOrder(root);
        // 转换为int[]
        int[] res = new int[list.size()];
        for(int i = 0; i < res.length; i++){
            res[i] = list.get(i);
        }
        return res;
    }
    // 中序遍历可以得到一个有序的序列
    public void InOrder(TreeNode node){
        if(node == null) return;
        // 左
        InOrder(node.left);
        // 根
        if(pre != node.val) count = 1;
        else count +=1;
        // 和之前的众数出现次数一样，加入结果集
        if(count == maxcount) list.add(node.val);
        // 如果有出现次数更多的出现了，则摒弃之前的结果集（new ArrayList<>()），将当前值加入进去
        if(count > maxcount){
            list = new ArrayList<>();
            list.add(node.val);
            maxcount = count;
        }
        pre = node.val;
        // 右
        InOrder(node.right);
    }
}
```

