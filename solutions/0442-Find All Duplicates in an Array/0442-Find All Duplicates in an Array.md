### 题目地址：https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/

解释：
1. 数组长度为n,数据的范围是1-n
2. 因此，让nums[i] - 1 作为index，将nums[index]上面的值 * (-1)
3. 如果是由负-> 正，则说明该数出现两次（因为有重复的数映射过来想 * (-1) 改变符号）
<img src="1593152121.297684.jpg?raw=true" width="70%" height="70%">

### Java
``` java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> res = new ArrayList<>();
        for(int i = 0; i < nums.length; i++){
            // 注意Math.abs，因为可能该数为负
            if(nums[Math.abs(nums[i]) - 1] > 0) nums[Math.abs(nums[i]) - 1] *= -1;
            else res.add(Math.abs(nums[i]));
        }
        return res;
    }
}
```

