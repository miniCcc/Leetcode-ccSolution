### 题目地址：https://leetcode-cn.com/problems/numbers-with-same-consecutive-differences/

返回所有长度为 n 且满足其每两个连续位上的数字之间的差的绝对值为 k 的 **非负整数** 。

请注意，**除了** 数字 0 本身之外，答案中的每个数字都 **不能** 有前导零。例如，01 有一个前导零，所以是无效的；但 0 是有效的。

你可以按 **任何顺序** 返回答案。

 

**示例 1：**

``` java
输入：n = 3, k = 7
输出：[181,292,707,818,929]
解释：注意，070 不是一个有效的数字，因为它有前导零。
```

**示例 2：**

``` java
输入：n = 2, k = 1
输出：[10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```

**示例 3：**

``` java
输入：n = 2, k = 0
输出：[11,22,33,44,55,66,77,88,99]
```

**示例 4：**

``` java
输入：n = 2, k = 1
输出：[10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```

**示例 5：**

``` java
输入：n = 2, k = 2
输出：[13,20,24,31,35,42,46,53,57,64,68,75,79,86,97]
```



**提示：**

- 2 <= n <= 9
- 0 <= k <= 9

---

**Java**

``` java
class Solution {
    List<Integer> list = new ArrayList<>();
    public int[] numsSameConsecDiff(int n, int k) {
        // 长度为1的时候，直接返回结果集
        if(n == 1) return new int[]{0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
        for(int i = 1; i <= 9; i++){
            // 初始len = 1, last为当前i，sum也为i
            dfs(1, i, i, n, k);
        }
 		// 拷贝数据
        int[] res = new int[list.size()];
        for(int i = 0; i < res.length; i++){
            res[i] = list.get(i);
        }
        return res;
    }

    public void dfs(int curlen, int last, int sum, int n, int k){
        if(curlen == n){
            list.add(sum);
            return;
        }
        if(last + k <= 9) dfs(curlen + 1, last + k, sum * 10 + (last + k), n, k);
        // 判断k > 0，避免k == 0重复计算
        if(k > 0 && last - k >= 0) dfs(curlen + 1, last - k, sum * 10 + (last - k), n, k);
    }
}
```

**注意**

- <table><tr><td bgcolor=pink>这里不能调用list.toArray()这个方法，因为这个方法只对字符串String起效，而对int类型的不起作用，只能手动拷贝数据</td></tr></table>

