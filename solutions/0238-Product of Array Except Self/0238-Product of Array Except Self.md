### 题目地址：https://leetcode-cn.com/problems/product-of-array-except-self/
### Java
``` java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] a = new int[nums.length];
        int[] b = new int[nums.length];
        int temp = nums[0];
        a[0] = 1;
        b[nums.length - 1] = 1;
        for(int i = 1; i < nums.length; i++){
            a[i] = temp;
            temp *= nums[i];
        }
        temp = nums[nums.length - 1];
        for(int j = nums.length - 2; j >=0; j--){
            b[j] = temp;
            temp *= nums[j];
        }
        for(int i = 0; i < nums.length; i++){
            a[i] *= b[i];
        }
        return a;
    }
}
```
解释：
1. 题目要求不能使用**除法**,因此常规方法行不通
2. a数组用来记录该位置左边乘积，b数组用来记录该位置右边乘积
3. a,b相应位置相乘即可
4. 注：a[0]和b[len - 1]直接设置成1，因为没有左边或者右边的乘积，直接赋值为1，在a,b相乘的时候不会改变结果

<img src="1593009258.05205.jpg?raw=true" width="50%" height="50%">