### 0338. 比特位计数

#### 题目地址：https://leetcode-cn.com/problems/counting-bits/

给定一个非负整数 **num**。对于 **0 ≤ i ≤ num** 范围中的每个数字 **i** ，计算其二进制数中的 1 的数目并将它们作为数组返回。

**示例 1:**

```
输入: 2
输出: [0,1,1]
```

**示例 2:**

```
输入: 5
输出: [0,1,1,2,1,2]
```

**进阶:**

- 给出时间复杂度为O(n*sizeof(integer))的解答非常容易。但你可以在线性时间O(n)内用一趟扫描做到吗？
- 要求算法的空间复杂度为O(n)。
- 你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 __builtin_popcount）来执行此操作。

---

**Java第一版**

``` java
class Solution {
    public int[] countBits(int n) {
        int[] cost = new int[n + 1];
        cost[0] = 0;
        for(int i = 1; i <= n; i++){
            if(i % 2 == 1) cost[i] = cost[i - 1] + 1;
            else{
                int num = i;
                int count = 0;
                while(num > 0){
                    count += (num & 1);
                    num >>= 1;
                }
                cost[i] = count;
            }
        }
        return cost;
    }
}
```

该方式比较慢，是分为了这个位置是否是2的倍数来算的，如果是2的倍数，那么按正常方式来算1的个数，如果不是（则是奇数），是`cost[i - 1] + 1`，是因为二进制的最后以为代表1

**第二版**

``` java
class Solution {
    public int[] countBits(int n) {
        int[] cost = new int[n + 1];
        cost[0] = 0;
        for(int i = 1; i <= n; i++){
            cost[i] = cost[i >> 1] + (i & 1);
        }
        return cost;
    }
}
```

解释一下`cost[i] = cost[i >> 1] + (i & 1);`：

- `cost[i >> 1]`相当于把这个数除以2，因为二进制的表示，可以看成是他的一半*2+余数，而这个余数属于0或者1，所以`(i & 1)`用于取最后一位