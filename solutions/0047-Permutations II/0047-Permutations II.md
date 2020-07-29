### 题目地址：https://leetcode-cn.com/problems/permutations-ii/


给定一个可包含重复数字的序列，返回所有不重复的全排列。

**示例**:

输入: [1,1,2] <br>
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

---

### Java
``` java
class Solution {
    // 这里是采用set去重，虽然可行，但是看到打败多少人的时候我眼泪掉下来....（set真的太慢了）
    private Set<List<Integer>> res = new HashSet<>();

    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        List<Integer> list = new ArrayList<>();
        boolean[] used = new boolean[nums.length];
        backtrack(nums, list, used);
        return new ArrayList<>(res);
    }
    public void backtrack(int[] nums, List<Integer> list, boolean[] used){
        if(list.size() == nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = 0; i < nums.length; i++){
            if(used[i]) continue;
            list.add(nums[i]);
            used[i] = true;
            backtrack(nums, list, used);
            used[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```

### 优化

> 先看问题所在：因为存在重复的元素，例如[1, 1, 2]这样的，有两种结果[2, 1, 1]和[2, 1, 1]，注意这里结果看起来是一样的，但是第一个结果的两个1互换后就形成了第二个结果，因此我们需要去重

1. used数组和nums数组等长，用来记录这个位置上nums[i]是否被使用过，使用过：true，没有使用：false
2. 这里进行了两次if判断<br>
  2.1 第一次是判断该位置是否使用，如果已经使用，那么直接continue; <br>
  2.2 如果没有被使用过，但是！！！<br>
  重点解释一下这句话：**如果这个数和之前的数一样(先排序，相同的数会挨在一起)，并且之前的数还未使用过（说明已经回溯过）**，我们反着来想，如果挨着一样并且前面那个数已经被使用过，那么我就可以放心大胆的使用现在这个数（证明不在第二个重复的循环里，仔细体会），那么需要第二次剪枝`if(i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) continue;`
3. 提供一个写的很好的题解参考链接：[点我](https://leetcode-cn.com/problems/permutations-ii/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liwe-2/)

``` java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        List<Integer> list = new ArrayList<>();
        boolean[] used = new boolean[nums.length];
        backtrack(nums, list, used);
        return res;
    }
    public void backtrack(int[] nums, List<Integer> list, boolean[] used){
        if(list.size() == nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = 0; i < nums.length; i++){
            // 两个if，划重点要考的！！！
            if(used[i]) continue;
            if(i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) continue;
            list.add(nums[i]);
            used[i] = true;
            backtrack(nums, list, used);
            used[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```
