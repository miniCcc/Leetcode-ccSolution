### 题目地址：https://leetcode-cn.com/problems/rotated-digits/

### Java
``` java
class Solution {
    public int rotatedDigits(int N) {
        int res = 0;
        for(int i = 1; i <= N; i++){
            if(helper(i)) res++;
        }
        return res;
    }
    public boolean helper(int n){
        int count = 0;
        int num2 = 0, num = n; // count记录现在是10的多少位数
        while(num > 0){ //取出每一位的数
            int temp = num % 10;
            if(!(temp == 0 || temp == 1 || temp== 8 || temp == 2 || temp == 5 || temp == 6 || temp == 9)) return false;
            num2 += Math.pow(10, count++) * reverse(temp); 
            num /= 10; // num >>= 2一样的
        }
        if(num2 == n) return false;
        return true;
    }
    public int reverse(int n){ // 进行旋转
        if(n == 1 || n == 0 || n == 8) return n;
        if(n == 2) return 5;
        if(n == 5) return 2;
        if(n == 6) return 9;
        return 6;
    }
}
```

**思路：**
1. 从1开始遍历，直到N，对每一个数进行判别
2. 假定当前述为n，直接取出每一位上面的数字，如果不可以翻转直接返回false
3. 如果都可以翻转，在取出的过程中，边取边翻转，并且重新计数num2,
4. 判断num和num2的值（n的值以更改）
