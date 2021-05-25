### 1305. 两棵二叉搜索树中的所有元素

#### 题目地址:https://leetcode-cn.com/problems/all-elements-in-two-binary-search-trees/

给你 `root1` 和 `root2` 这两棵二叉搜索树。

请你返回一个列表，其中包含 **两棵树** 中的所有整数并按 **升序** 排序。.

 

**示例 1：**

![img](q2-e1.png)

```
输入：root1 = [2,1,4], root2 = [1,0,3]
输出：[0,1,1,2,3,4]
```

**示例 2：**

```
输入：root1 = [0,-10,10], root2 = [5,1,7,0,2]
输出：[-10,0,0,1,2,5,7,10]
```

**示例 3：**

```
输入：root1 = [], root2 = [5,1,7,0,2]
输出：[0,1,2,5,7]
```

**示例 4：**

```
输入：root1 = [0,-10,10], root2 = []
输出：[-10,0,10]
```

**示例 5：**

![img](q2-e5-.png)

```
输入：root1 = [1,null,8], root2 = [8,1]
输出：[1,1,8,8]
```

**提示：**

- 每棵树最多有 `5000` 个节点。
- 每个节点的值在 `[-10^5, 10^5]` 之间。

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
    List<Integer> list = new ArrayList<>();
    Stack<TreeNode> stack1 = new Stack<>();
    Stack<TreeNode> stack2 = new Stack<>();
    public List<Integer> getAllElements(TreeNode root1, TreeNode root2) {
        inOrder1(root1);
        inOrder2(root2);
        while(!stack1.isEmpty() && !stack2.isEmpty()) {
            // 谁小就添加谁，并pop掉
            if(stack1.peek().val < stack2.peek().val) list.add(stack1.pop().val);
            else if(stack2.peek().val < stack1.peek().val) list.add(stack2.pop().val);
            // 值相等，都加入结果集并pop
            else {
                list.add(stack1.pop().val);
                list.add(stack2.pop().val);  
            }  
        }
        // 处理剩下的
        if(!stack1.isEmpty()) helper(stack1);
        else helper(stack2);

        return list;
    }
    // 左根右
    public void inOrder1(TreeNode root1){
        if(root1 == null) return;
        inOrder1(root1.right);
        stack1.push(root1);
        inOrder1(root1.left);
    }
    public void inOrder2(TreeNode root2){
        if(root2 == null) return;
        inOrder2(root2.right);
        stack2.push(root2);
        inOrder2(root2.left);
    }
    public void helper(Stack<TreeNode> stack){
        while(!stack.isEmpty()){
            list.add(stack.pop().val);
        }
    }
}
```

