# Problem 47: Unique Permutations 


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
1. 这道题是普通permutation的加强版，题目中有了重复元素。如何handle重复元素？**引入一个额外数组visited标记！**因为i是每一个数组元素的固定的id
当元素被访问过，```visited[i] == 1```，就先不考虑;
当元素和之前元素相同，并且之前元素没有被访问过， ```i > 0 && nums[i] == nums[i-1] && visited[i-1] == 0```,也可以不考虑
2. list的处理，先把刚加进的元素剔除，再把访问value改为0， 缺一不可
```
list.remove(list.size() - 1);
visited[i] = 0;
```



