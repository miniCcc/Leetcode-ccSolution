### 题目地址：https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

**示例:**

``` java
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**说明:**
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。

---

**Java**

``` java
class Solution {
    char[][] elements = new char[][]{{'a','b','c'}, {'d','e','f'}, {'g','h','i'}, {'j','k','l'}, {'m','n','o'}, {'p','q','r','s'}, {'t','u','v'}, {'w','x','y','z'}};
    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if(digits.length() == 0) return res;
        StringBuilder str = new StringBuilder();
        backtrace(res, str, digits, 0);
        return res;
    }
    // index代表的是指向digits的哪个位置
    public void backtrace(List<String> res, StringBuilder str, String digits, int index){
        if(str.length() == digits.length()){
            res.add(str.toString());
            return;
        }
        // 计算这是哪个数字
        int num = Integer.valueOf(digits.charAt(index) + "");
        // 注意这里是num-2
        for(int i = 0; i < elements[num-2].length; i++){
            // 做选择
            str.append(elements[num-2][i]);
            backtrace(res, str, digits, index + 1);
            // 撤销选择
            str.delete(str.length() - 1, str.length());
        }

    }
}
```

**解释：**

- 算是标准的回溯模板，使用`elements`定义了对应的字母，在计算num的时候，进入循环写的是`num-2`，因为假若是2的话，那么就应该对应第一个，以此类推

