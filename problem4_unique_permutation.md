# Problem4: Unique Permutation


> https://leetcode.com/problems/permutations-ii/

这道题最主要的就是去重复。
-----------------------------
```java
public class Solution {
    List<Integer> list = new ArrayList<Integer>();
    List<List<Integer>> result = new ArrayList(list);

    public List<List<Integer>> permuteUnique(int[] nums) {
        int[] visited = new int[nums.length];
        Arrays.sort(nums);
        helper(list, nums, visited);
        return result;
    }

    private void helper(List<Integer> list, int[] nums, int[] visited) {
        if (list.size() == nums.length) {
            result.add(new ArrayList<Integer>(list));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (visited[i] == 1 || (i > 0 && nums[i] == nums[i - 1] && visited[i - 1] == 0)) {
                continue;
            }

            visited[i] = 1;
            list.add(nums[i]);
            helper(list, nums, visited);
            list.remove(list.size() - 1);
            visited[i] = 0;
        }
    }
}
```
-------------------------

## 易错点
1. 



