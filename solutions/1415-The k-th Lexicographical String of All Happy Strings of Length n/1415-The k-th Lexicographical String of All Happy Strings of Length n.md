### 题目地址：https://leetcode-cn.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/

一个 「开心字符串」定义为：

仅包含小写字母 ['a', 'b', 'c'].
对所有在 1 到 s.length - 1 之间的 i ，满足 s[i] != s[i + 1] （字符串的下标从 1 开始）。
比方说，字符串 "abc"，"ac"，"b" 和 "abcbabcbcb" 都是开心字符串，但是 "aa"，"baa" 和 "ababbc" 都不是开心字符串。

给你两个整数 n 和 k ，你需要将长度为 n 的所有开心字符串按字典序排序。

请你返回排序后的第 k 个开心字符串，如果长度为 n 的开心字符串少于 k 个，那么请你返回 空字符串 。

**示例 1：**

``` java
输入：n = 1, k = 3
输出："c"
解释：列表 ["a", "b", "c"] 包含了所有长度为 1 的开心字符串。按照字典序排序后第三个字符串为 "c" 。
```

**示例 2：**

``` java
输入：n = 1, k = 4
输出：""
解释：长度为 1 的开心字符串只有 3 个。
```

**示例 3：**

``` java
输入：n = 3, k = 9
输出："cab"
解释：长度为 3 的开心字符串总共有 12 个 ["aba", "abc", "aca", "acb", "bab", "bac", "bca", "bcb", "cab", "cac", "cba", "cbc"] 。第 9 个字符串为 "cab"
```

**示例 4：**

``` java
输入：n = 2, k = 7
输出：""
```

**示例 5：**

``` java
输入：n = 10, k = 100
输出："abacbabacb"
```

**提示：**

- 1 <= n <= 10
- 1 <= k <= 100

---

**Java**

``` java
class Solution {
    List<String> list = new ArrayList<>();
    char[] elements = new char[]{'a', 'b', 'c'};
    
    public String getHappyString(int n, int k) {
        StringBuilder str = new StringBuilder();
        dfs(n, str, -1);                            
        
        for(int i = 0; i < list.size(); i++){
            if(i == k - 1) return list.get(i);
        }
        return "";
    }
    public void dfs(int n, StringBuilder str, int index){
        if(str.length() == n){
            list.add(str.toString());
            //count++;
            return;
        }
        
        for(int i = 0; i < elements.length; i++){
            // 避免'不开心'
            if(i == index) continue;

            char c = elements[i];
            // 做选择
            str.append(c);
            // 注意传的是i，代表了当前这个使用了，下一个在if的时候就避免了'不开心'
            dfs(n, str, i);
            // 撤销选择
            str.delete(str.length() - 1, str.length());
        }
    }
}
```

**解释：**

- 其实根本用不到List来把每次的结果加入结果集，那么只需要用一个变量count来计算这到底是第几个就行，当时第k的时候直接返回
- 改进后的版本：

``` java
class Solution {
    int count = 0;
    String ans;
    char[] elements = new char[]{'a', 'b', 'c'};
    
    public String getHappyString(int n, int k) {
        StringBuilder str = new StringBuilder();
        dfs(n, str, -1, k);                            
 
        return count == k ? ans : "";
    }
    public void dfs(int n, StringBuilder str, int index, int k){
        if(count == k) return;
        if(str.length() == n){
            count++;
            ans = str.toString();
            return;
        }
        
        for(int i = 0; i < elements.length; i++){
            // 避免'不开心'
            if(i == index) continue;

            char c = elements[i];
            str.append(c);
            dfs(n, str, i, k);
            str.delete(str.length() - 1, str.length());
        }
    }
}
```

