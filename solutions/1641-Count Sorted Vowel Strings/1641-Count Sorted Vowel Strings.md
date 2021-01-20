### 题目地址：https://leetcode-cn.com/problems/count-sorted-vowel-strings/

给你一个整数 n，请返回长度为 n 、仅由元音 (a, e, i, o, u) 组成且按 字典序排列 的字符串数量。

字符串 s 按 字典序排列 需要满足：对于所有有效的 i，s[i] 在字母表中的位置总是与 s[i+1] 相同或在 s[i+1] 之前。

**示例 1：**

``` java
输入：n = 1
输出：5
解释：仅由元音组成的 5 个字典序字符串为 ["a","e","i","o","u"]
```

**示例 2：**

``` java
输入：n = 2
输出：15
解释：仅由元音组成的 15 个字典序字符串为
["aa","ae","ai","ao","au","ee","ei","eo","eu","ii","io","iu","oo","ou","uu"]
注意，"ea" 不是符合题意的字符串，因为 'e' 在字母表中的位置比 'a' 靠后
```

**示例 3：**

``` java
输入：n = 33
输出：66045
```

**提示：**

- `1 <= n <= 50 `

---

**Java**

``` java
class Solution {
    char[] elements = new char[]{'a', 'e', 'i', 'o', 'u'};
    int count = 0;
    public int countVowelStrings(int n) {
        StringBuilder str = new StringBuilder();
        dfs(n, 0, str);
        return count;
    }
    public void dfs(int n, int index, StringBuilder str){
        if(str.length() == n){
            count++;
            return;
        }
        for(int i = index; i < elements.length; i++){
            str.append(elements[i]);
            // 注意这里传的是i，因为可以有aa这种形式，所以不是i+1
            dfs(n, i, str);
            str.delete(str.length() - 1, str.length());
        }
    }
}
```

这里用到了StringBuilder，但是我们发现其实只用返回的是count，而不用返回字符串，而StringBuilder存在的目的在于让我们获取长度，那么我们可以专门用一个变量来记录长度即可

``` java
class Solution {
    char[] elements = new char[]{'a', 'e', 'i', 'o', 'u'};
    int count = 0;
    public int countVowelStrings(int n) {
        //StringBuilder str = new StringBuilder();
        dfs(n, 0, 0);
        return count;
    }
    public void dfs(int n, int index, int len){
        if(len == n){
            count++;
            return;
        }
        for(int i = index; i < elements.length; i++){
            len++;
            dfs(n, i, len);
            len--;
        }
    }
}
```



