### 题目地址：https://leetcode-cn.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/

给定一个字符串数组 arr，字符串 s 是将 arr 某一子序列字符串连接所得的字符串，如果 s 中的每一个字符都只出现过一次，那么它就是一个可行解。

请返回所有可行解 s 中最长长度。

**示例 1：**

``` java
输入：arr = ["un","iq","ue"]
输出：4
解释：所有可能的串联组合是 "","un","iq","ue","uniq" 和 "ique"，最大长度为 4。
```

**示例 2：**

``` java
输入：arr = ["cha","r","act","ers"]
输出：6
解释：可能的解答有 "chaers" 和 "acters"。
```

**示例 3：**

``` java
输入：arr = ["abcdefghijklmnopqrstuvwxyz"]
输出：26
```

**提示：**

- 1 <= arr.length <= 16
- 1 <= arr[i].length <= 26
- arr[i] 中只含有小写英文字母

---

**Java**

### 第一个版本

``` java
class Solution {
    int maxlen = 0;
    //boolean[] used = new boolean[26];
    public int maxLength(List<String> arr) {
        StringBuilder str = new StringBuilder();
        dfs(arr, 0, str);
        return maxlen;
    }
    public void dfs(List<String> arr, int index, StringBuilder str){
        if(index == arr.size())  return;  
        
        for(int i = index; i < arr.size(); i++){
            // 判断字母是否被重复使用过
            if(usedCheck(str.toString(), arr.get(i))){
                // 做选择
                str.append(arr.get(i));
                maxlen = Math.max(str.length(), maxlen);
                dfs(arr, i + 1, str);
                // 撤销选择
                str.delete(str.length() - arr.get(i).length(), str.length());
                // i+2就代表跳过了当前这个
            }else dfs(arr, i + 2, str);
        }

    }
    // 检测是否被使用过
    public boolean usedCheck(String str1, String str2){
        String temp = str1 + str2;
        int[] count = new int[26];
        for(int i = 0; i < temp.length(); i++){
            char c = temp.charAt(i);
            count[c - 97]++;
            if(count[c - 97] > 1) return false;
        }
        return true;
    }
}
```

对于这个解法，一定要注意的是：

	1. ·`maxlen = Math.max(str.length(), maxlen);`一定不要写在if判断条件里，比如：

``` java
if(index == arr.size()){
    maxlen = Math.max(str.length(), maxlen);
    return; 
}   
```

如果这样写的话那就是错误的，比如测试用例`["jnfbyktlrqumowxd","mvhgcpxnjzrdei"]`就会过不去，因为第一个和第二个有重复的在，没有及时保存第一个的长度，就执行了撤销选择，str为空，然后最后会返回14，没有返回16

2. 在`usedCheck`里，一定要写成双String，而不要写成`(StringBuilder str1, String str2)`，因为这样有`append`操作的话会直接改变str的值！！！
3. 这个解法没有什么速度，通常在25ms，击败的人很少，优可以在判断是否有重复处优化

### 第二个版本

``` java
class Solution {
    int maxlen = 0;
    //boolean[] used = new boolean[26];
    public int maxLength(List<String> arr) {
        StringBuilder str = new StringBuilder();
        dfs(arr, 0, str);
        return maxlen;
    }
    public void dfs(List<String> arr, int index, StringBuilder str){
         // 判断字母是否被重复使用过
        if(!usedCheck(str.toString())) return;
  
        maxlen = Math.max(str.length(), maxlen);  
        for(int i = index; i < arr.size(); i++){
            str.append(arr.get(i));
            dfs(arr, i+1, str);    
            str.delete(str.length() - arr.get(i).length(), str.length());
        }
    }
    // 检测是否被使用过
    public boolean usedCheck(String temp){
        int[] count = new int[26];
        for(int i = 0; i < temp.length(); i++){
            char c = temp.charAt(i);
            count[c - 97]++;
            if(count[c - 97] > 1) return false;
        }
        return true;
    }
}
```

这个解法应该更好懂而且速度更快：10ms，还是有几点需要注意：

1. 上一个解法是先判断，再append，这里是不管有没有重复都执行append，然后调用dfs进入一层，在函数首部判断`if(!usedCheck(str.toString())) return;`，也就是如果有重复的字母，利用函数去检验，有的话直接return回来了，然后执行撤销操作（毕竟重复了，不要了），需要注意的是这里`usedCheck`也变化了，与上个版本的不同了

 	2. `maxlen = Math.max(str.length(), maxlen);  `写在了for循环的外面，为什么不写成这样？

``` java
  
for(int i = index; i < arr.size(); i++){
    str.append(arr.get(i));
    maxlen = Math.max(str.length(), maxlen);
    dfs(arr, i+1, str);    
    str.delete(str.length() - arr.get(i).length(), str.length());
}
```

因为可能有重复的，此时还没撤销操作呢，所以这样得到的长度是不可靠的，写在外面的话，只要执行到这一句，那么str一定是没有重复的字母的，毕竟有个if条件监管，只要有重复直接return了

### 第三个版本

``` java
class Solution {
    int maxlen = 0;
    //boolean[] used = new boolean[26];
    public int maxLength(List<String> arr) {
        StringBuilder str = new StringBuilder();
        dfs(arr, 0, str);
        return maxlen;
    }
    public void dfs(List<String> arr, int index, StringBuilder str){
         // 判断字母是否被重复使用过
        if(!usedCheck(str.toString())) return;
  
        maxlen = Math.max(str.length(), maxlen);  
        for(int i = index; i < arr.size(); i++){
            str.append(arr.get(i));
            dfs(arr, i+1, str);    
            str.delete(str.length() - arr.get(i).length(), str.length());
        }

    }
    // 检测是否被使用过
    public boolean usedCheck(String temp){
        char[] strtrmp = temp.toCharArray();
        int t = 0;
        for(char c : strtrmp){
            // 看到底是第几个
            int i = c - 'a';
            // 同1则1
            if((t & (1 << i)) != 0){
                return false;
            }
            // 有1则1
            t |= 1 << i;
        }
       return true;
    }
}
```

这里主要是针对判断是否有重复的字母进行优化，使用位运算来实现，给定一个`int t = 0`，因为我们都是小写，则有26个字母，那么0-25就代表了a~z，一共26位，相应位置代表了这个字母是否出现过（1代表出现了，0代表没有出现）。

- 首先`int i = c - 'a';`用来计算当前字符到底是第几个，如果是a则为0，如果是c则为2，`if((t & (1 << i)) != 0)`这里的1 << i的1代表了这个数出现了，现在需要对应到具体的位置上去，则使用`1 << i`，然后和t进行与操作（同1则1），也就是不管t和1<<i的位数一不一样，那t上面和1相应位置上的那个值只要是1，同1则1之后结果还是1，那最后得到的二进制串化为10进制之后一定不为0
- 再来看`t |= 1 << i;`，如果执行到这一句证明至少到现在是没有重复字母的，那么把当前这个字符的对应位置上置1代表遍历过了，那就是对应位置上`0 | 1 = 1`，即通过这种方式来实现
- 这样运行的结果是9ms