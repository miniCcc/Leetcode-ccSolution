### 题目地址：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/

解释：
1. 使用一个变量记录新数据的下标
2. 一旦发现有数只出现了1次，则证明后面的需要移动
3. 如果超过了2次，则证明只需要截断记录下标即可

### Java
``` java
class Solution {
    public int removeDuplicates(int[] nums) {
        // 注意，count初值不是1，与下面的if判断条件对应
        int count = 0;
        // 注意：j的初值是1，因为不管怎么样第一个数不需要更改
        int j = 1;
        for(int i = 1; i < nums.length; i++){
            if(nums[i] == nums[i - 1]){
                count++;
                // 也就是count = 1,也就是出现两次，第二次赋值
                if(count < 2) nums[j++] = nums[i];
            } 
            else{
                count = 0;
                // 遇到新的值了，第一次赋值
                nums[j++] = nums[i];
            }
        }
        return j;
    }
}
```
