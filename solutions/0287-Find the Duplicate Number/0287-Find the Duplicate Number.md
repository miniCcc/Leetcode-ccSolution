### 题目地址：https://leetcode-cn.com/problems/find-the-duplicate-number/

先看解释：
1. 注意题目限定条件：<br>
    1.1 不能更改原数组（假设数组是只读的）:不能使用排序等操作<br>
    1.2 只能使用额外的 O(1) 的空间:不能开辟数组之类的新空间<br>
    1.3 时间复杂度小于 O(n2):不能暴力
    
2. 两个参考地址：https://leetcode-cn.com/problems/find-the-duplicate-number/solution/287xun-zhao-zhong-fu-shu-by-kirsche/  和   https://blog.csdn.net/plokmju88/article/details/103675872
3. 本题主要是利用数组转链表，通过快慢指针找到环的入口处
<img src="1593053280.622183.jpg?raw=true" width="80%" height="80%">

### Java
``` java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0, fast = 0;
        slow = nums[slow];
        fast = nums[nums[fast]];
        // 相遇与c
        while(slow != fast){
            // 步长
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        int p1 = 0, p2 = slow;
        // 这里是c到b,a到b
        while(p1 != p2){
            p1 = nums[p1];
            p2 = nums[p2];
        }
        return p1;
    }
}
```
