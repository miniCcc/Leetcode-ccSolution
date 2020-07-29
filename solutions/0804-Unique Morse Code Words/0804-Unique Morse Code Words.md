### 题目地址：https://leetcode-cn.com/problems/unique-morse-code-words/
### Java
``` java
class Solution {
    public int uniqueMorseRepresentations(String[] words) {
        String[] code = {".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};
        Set<String> set = new HashSet<>();
        for(String str : words){
            StringBuilder temp = new StringBuilder();
            for(int i = 0; i < str.length(); i++){
                char c = str.charAt(i);
                temp.append(code[c - 'a']);
            }
            set.add(temp.toString());
        }
        return set.size(); // 直接返回set的个数，因为set已自动去重
    }
}
```

---

### Python3
``` python
class Solution:
    def uniqueMorseRepresentations(self, words: List[str]) -> int:
        myset = set()
        code = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
        alpha = "abcdefghijklmnopqrstuvwxyz"
        for strs in words:
            temp = ""
            for ch in strs:
                temp += code[alpha.index(ch)]
            myset.add(temp)
        return len(myset)

```
