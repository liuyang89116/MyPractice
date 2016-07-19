# Problem3: Permutations


> https://leetcode.com/problems/permutations

这道题是排列的基本类型
--------------------------------
```java
public class Solution {
    List<Integer> list = new ArrayList<Integer>();
    List<List<Integer>> result = new ArrayList(list);

    public List<List<Integer>> permute(int[] nums) {
        if (nums.length == 0 || nums == null) {
            return result;
        }

        helper(list, nums);
        return result;
    }

    private void helper(List<Integer> list, int[] nums) {
        if (list.size() == nums.length) {
            result.add(new ArrayList(list));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (list.contains(nums[i])) {
                continue;
            }
            list.add(nums[i]);
            helper(list, nums);
            list.remove(list.size() - 1);
        }
    }
}
```
--------------------------------

**易错点**

1. **首先要搞清楚排列和组合的区别：** 组合类的问题，每个组合，可能的元素个数是不一样的。可能为空，可能有一个，可能有多个。但是，排列问题，每个都是这么多的元素，看他有多少中可能。
2. 所以我们只需要在组合的模板基础上稍作修改即可
```java
if (list.contains(nums[i])) {
         continue;
}
```
这样思路变为：如果list里面已经包含有这个元素就不再往里加了