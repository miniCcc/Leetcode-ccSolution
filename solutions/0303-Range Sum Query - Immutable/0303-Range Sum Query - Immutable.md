### 0303. 区域和检索 - 数组不可变

#### 题目地址：https://leetcode-cn.com/problems/range-sum-query-immutable/

给定一个整数数组  `nums`，求出数组从索引1`i` 到 `j` `（i ≤ j）`范围内元素的总和，包含`i`、`j `两点。

实现 `NumArray` 类：

`NumArray(int[] nums)` 使用数组` nums `初始化对象
`int sumRange(int i, int j)` 返回数组 `nums `从索引 `i` 到 `j` `（i ≤ j）`范围内元素的总和，包含 `i`、`j` 两点（也就是 `sum(nums[i], nums[i + 1], ... , nums[j])）`

**示例**

```
输入：
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
输出：
[null, 1, -1, -3]

解释：
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return 1 ((-2) + 0 + 3)
numArray.sumRange(2, 5); // return -1 (3 + (-5) + 2 + (-1)) 
numArray.sumRange(0, 5); // return -3 ((-2) + 0 + 3 + (-5) + 2 + (-1))
```

**提示：**

- `0 <= nums.length <= 104`
- `-105 <= nums[i] <= 105`
- `0 <= i <= j < nums.length`
- 最多调用 `104 `次 `sumRange `方法

---

**Java**

``` java
class NumArray {
    public int[] nums;
    private int[] sum;

    public NumArray(int[] nums) {
        this.nums = nums;
        sum = new int[nums.length];
        sum[0] = nums[0];
        for(int i = 1; i <  nums.length; i++){
            sum[i] += sum[i - 1] + nums[i];
        }
    }
    
    public int sumRange(int left, int right) {
        if(left == 0) return sum[right];
        // 因为要包含自己
        else return sum[right] - sum[left - 1];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(left,right);
 */
```

本题主要是会调用很多次的`sumRange`，看例子：

```
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
```

后面三个`sumRange`，那么就要调用三次，非常浪费时间，因此添加一个数组`sum[]`，对原数组`nums[]`做预处理，每一`sum[i]`就是`nums`的前`i`个元素的和