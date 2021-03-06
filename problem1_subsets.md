# Problem 78: Subsets

> https://leetcode.com/problems/subsets/


----------
##思路
* 这道题是集合的基本题目
* 确定待排列的字母，数组，和位置
* 每次把不同的元素加到 result 里面去
* 加新元素- call 自己的方法-最后再把这个元素踢出去 

---------------------
##复杂度
* Time  
如果真的要细扣的话，Subset 总共产生 $$2^n$$ 个 Subset，但是每个 Subset 的长度是 n 数量级的，所以 Subset 的复杂度应该是 $$O(n*2^n)$$ （你可以自行验证一下，所有subset中的元素个数总数是$$n*2^(n-1)$$）。这个式子严格来说不能写成 $$O(2^n)$$。不过为了突出这个式子中的最大头部分 2^n，很多人还是简单地说这个算法是“指数运行时间”的，并把 n 略去不写，只是咱们自己还是要清楚那里其实有个 n 在那里。
$$T(n) = T(n - 1) + T(n - 2) + ... + T(1) + T(0)$$，which solves to $$T(n) = O(2^n)$$  
So the time complexity is $$O(n2^n)$$

----

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        
        if (nums == null || nums.length == 0) {
            return rst;
        }
        
        // 这道题里是否 sort 数组不重要
        // Arrays.sort(nums);
        helper(nums, path, 0, rst);
        return rst;
    }
    
    private void helper(int[] nums, List<Integer> path, int pos, List<List<Integer>> rst) {
        rst.add(new ArrayList(path));
        
        for (int i = pos; i < nums.length; i++) {
            path.add(nums[i]);
            helper(nums, path, i + 1, rst);
            path.remove(path.size() - 1);
        }
    }
}
```
-----------------------

##易错点
1. 加result中的元素是 ```rst.add(new ArrayList(path));``` rst 本质上加的是和他同类的元素，我开始写的是```rst.add(path);```
2. 去掉最后一个元素 ```path.remove(path.size() - 1);```
3. 引申一点：数组的length不是方法，后面没有括号;但是size()是一个方法，记得要加括号
4. 这个方法体四个变量，把 path 和 rst 加进去是因为他俩得先初始化，在第一个方法体里初始化好了，第二个方法调用的时候使用方便
5. 加 pos 这个参数的原因是每次循环的时候从 i + 1 下一个元素循环起。
6. 一定记得要 sort

##补充
1. recursion 的时候，是 i + 1，而不是 pos + 1
