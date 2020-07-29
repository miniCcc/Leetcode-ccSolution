### 题目地址：https://leetcode-cn.com/problems/binary-gap/
### Java
``` java
class Solution {
    public int binaryGap(int N) {
        // 调用方法直接得到二进制
        String str = Integer.toBinaryString(N);
        // index用于记录上一个1的位置
        int max = 0, index = -1;
        for(int i = 0; i < str.length(); i++){
            char c = str.charAt(i);
            if(c == '1' && index == -1) index = i;
            else if(c == '1' && index >= 0){
                if(max <= i - index) max = i - index;
                index = i;
            }
        }
        return max;
    }
}
```
---

### Python3
``` python
class Solution:
    def binaryGap(self, N: int) -> int:
        num = bin(N)[2 : ]
        index = -1
        resmax = 0
        for i in range(len(num)):
            if num[i] == '1' and index < 0:
                index = i
            if num[i] == '1' and index >= 0:
                if resmax <= i - index:
                    resmax = i - index
                index = i
        return resmax 
```
