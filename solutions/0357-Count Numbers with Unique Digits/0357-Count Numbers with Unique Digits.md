### 题目地址：https://leetcode-cn.com/problems/count-numbers-with-unique-digits/

解释：
1. 公式：
```
f(0)=1              0 <= x < 1
f(1)=10             0 <= x < 10
f(2)=9*9+f(1)       0 <= x < 100
f(3)=9*9*8+f(2)     0 <= x < 1000
f(4)=9*9*8*7+f(3)   0 <= x < 10000
```
2. 这题本质上是一个排列组合问题，在`n >= 2`的时候，每次都要加上`dp(n - 1)`，举个例子（**重点**）：
```
f(1)的x属于[0, 10),而f(2) = 9 * 9 * 8 + f(1)，f(2)的x属于[0, 100)，也就是说9 * 9 * 8计算的是[10, 100)的各位都不相同的数
细想9 * 9 * 8代表着什么？
每一位数取值有10个:[0, 9]，但是现在寻找的是[10, 100)，是个两位数，在计算组合数时A（十位的个数）* B（个位的个数）
这第一位不能为0，因此A有9个数备选，然后B除了A选过的这个数，还有9个数备选（这里包括0），以此类推，形成了9 * 9 * 8 * 7...的公式
```

### Java
``` java
class Solution {
    /*
    f(0)=1 
    f(1)=10
    f(2)=9*9+f(1)
    f(3)=9*9*8+f(2)
    f(4)=9*9*8*7+f(3)
    */
    public int countNumbersWithUniqueDigits(int n) {
        return dp(n);
    }
    public int dp(int n){
        if(n == 0) return 1;
        if(n == 1) return 10;
        int temp = 9 * 9;
        for(int i = 8; i > 10 - n; i--){
            temp *= i;
        }
        return temp + dp(n - 1);
    }
}
```
