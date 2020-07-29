### 题目地址：https://leetcode-cn.com/problems/palindromic-substrings/

给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被计为是不同的子串。

**示例 1:**<br>
输入: "abc"<br>
输出: 3<br>
解释: 三个回文子串: "a", "b", "c".

**示例 2:**<br>
输入: "aaa"<br>
输出: 6<br>
说明: 6个回文子串: "a", "a", "a", "aa", "aa", "aaa".

**注意:**<br>
输入的字符串长度不会超过1000。

### 中心扩展法：
1. 什么是中心扩展法？
  - 选择一个中心点，作为回文串的对称轴，left和right以该轴为中心向两边扩散，如果扩散过程中还是回文，则结果+1
2. 轴怎么选？
  - 需要注意的是，`aba`和`abba`是不同的，回文串可能以一个字符对称，也可能以两个字符对称
3. 有多少个中心点？
  - `2 * len - 1`个，首先有len个单字符的中心点，然后计算有多少个相邻的2个字符，有`len - 1`个挨着的两个字符，共`2 * len - 1`个
4. `int left = i / 2; int right = left + i % 2;`公式怎么来的？
  - 不知道，记住这就是中心扩展公式就好...
5. 在下列代码中，体现不出来两个字符为中心和一个字符为中心的区别？为什么都是用的是一个公式，不应该分类讨论吗？
  - 找个例子手动推一次就可以知道，有时候是`left=right`的,只能说公式真的牛
---

### Java
``` java
class Solution {
    public int countSubstrings(String s) {
        int res = 0;
        for(int i = 0; i < s.length() * 2 - 1; i++){
            int left = i / 2;
            int right = left + i % 2;
            while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)){
                res++;
                left--;
                right++;
            }
        }
        return res;
    }
}
```
