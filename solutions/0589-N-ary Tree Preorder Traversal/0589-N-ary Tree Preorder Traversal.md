### 0589-N叉树的前序遍历

#### 题目地址：https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/

给定一个 N 叉树，返回其节点值的*前序遍历*。

例如，给定一个 `3叉树` :
 

<img src="narytreeexample.png" alt="img" style="zoom:67%;" />

返回其前序遍历: `[1,3,5,6,2,4]`。

 

**说明:** 递归法很简单，你可以使用迭代法完成此题吗?

---

**Java**

``` java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList<>();
        helper(root, list);
        return list;
    }
    public void helper(Node node, List<Integer> list){
        if(node == null) return;
        // 根
        list.add(node.val);
        for(Node n : node.children) helper(n, list);
    }
}
```

这个题和 `0590-N叉树的后序遍历` 是一样的，只是需要更改一下代码的位置即可，可以对比一下

递归实现非常简单，这里可以思考一下如何用迭代法完成：

``` java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList<>();
        Stack<Node> stack = new Stack<>();
        if(root == null) return list;
        stack.push(root);
        while(!stack.isEmpty()){
            Node node = stack.pop();
            list.add(node.val);
            // 注意：这里是倒着入栈的
            for(int i = node.children.size() - 1; i >= 0; i--) stack.push(node.children.get(i));
        }
        return list;
    }

}
```

