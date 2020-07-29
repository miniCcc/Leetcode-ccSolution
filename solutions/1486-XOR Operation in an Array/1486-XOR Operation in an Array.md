### 题目地址：https://leetcode-cn.com/problems/xor-operation-in-an-array/
### Java
``` java
class Solution {
    public int xorOperation(int n, int start) {
        int res = 0;
        for(int i = 0; i < n; i++){
            res ^= start + 2 * i;
        }
        return res;
    }
}
```
