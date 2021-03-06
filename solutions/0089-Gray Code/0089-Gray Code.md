### 题目地址：https://leetcode-cn.com/problems/gray-code/

格雷编码是一个二进制数字系统，在该系统中，两个连续的数值仅有一个位数的差异。

给定一个代表编码总位数的非负整数 n，打印其格雷编码序列。即使有多个不同答案，你也只需要返回其中一种。

格雷编码序列必须以 0 开头。

**示例 1:**

``` java
输入: 2
输出: [0,1,3,2]
解释:
00 - 0
01 - 1
11 - 3
10 - 2

对于给定的 n，其格雷编码序列并不唯一。
例如，[0,2,3,1] 也是一个有效的格雷编码序列。

00 - 0
10 - 2
11 - 3
01 - 1
```

**示例 2:**

``` java
输入: 0
输出: [0]
解释: 我们定义格雷编码序列必须以 0 开头。
     给定编码总位数为 n 的格雷编码序列，其长度为 2n。当 n = 0 时，长度为 20 = 1。
     因此，当 n = 0 时，其格雷编码序列为 [0]。
```

---

详细解释地址：https://leetcode-cn.com/problems/gray-code/solution/gray-code-jing-xiang-fan-she-fa-by-jyd/

**Java**

``` java
class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> res = new ArrayList<>();
        res.add(0);
        int head = 1;
        // 总位数为n，则需要外循环迭代计算n次
        for(int i = 0; i < n; i++){
            // 前面+0并不会改变原来的数值，只需要倒序遍历并且在二进制首位加上1就行
            // 使用位运算来实现二进制首位+1,eg. 01 -> 101 = 100 + 001
            // 而100是2的倍数，可以通过head << = 1实现不断放大
            for(int j = res.size() - 1; j >= 0; j--){
                res.add(head + res.get(j));
            }
            head <<= 1;
        }
        return res;
    }
}
```



