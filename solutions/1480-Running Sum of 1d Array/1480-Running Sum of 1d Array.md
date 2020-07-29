### 题目地址：https://leetcode-cn.com/problems/running-sum-of-1d-array/
### Java
``` java
class Solution {
    public int[] runningSum(int[] nums) {
        int count = nums[0];
        for(int i = 1; i < nums.length; i++){
            nums[i] += count;
            count = nums[i];
        }
        return nums;
    }
}
```
