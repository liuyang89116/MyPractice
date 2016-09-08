# Problem 46: Permutations 


> https://leetcode.com/problems/permutations

------------------
##思路
* 这道题是排列的基本类型
* 排列和组合不同的就是：
* 1）添加进 rst 的时间，上面题我们每添加一个数字到 path 里，就可以往 rst 里面添加，而这次，我们要生成完整的序列，所以需要当 path.size()＝＝ 序列长度的时候再往 rst 里面添加；
* 2）每次不能从pos开始往数组尾巴扫了，因为我们要求的不是Subset而是完整序列，所以要从第一个数字开始往数组尾巴扫，问题又来了，我们怎么知道取没取过这个元素呢，那么我们就创建一个boolean[] visit 每此添加的时候给相对应位置置True，删去的时候置False


--------------------------------
```java
public class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        if (nums == null || nums.length == 0) {
            return rst;
        }
        
        boolean[] visited = new boolean[nums.length];
        Arrays.sort(nums);
        helper(nums, path, visited, rst);
        
        return rst;
    }
    
    private void helper(int[] nums, List<Integer> path, boolean[] visited, List<List<Integer>> rst) {
        if (path.size() == nums.length) {
            rst.add(new ArrayList(path));
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i] == false) {
                path.add(nums[i]);
                visited[i] = true;
                helper(nums, path, visited, rst);
                path.remove(path.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```
------------------------

##易错点

1. **首先要搞清楚排列和组合的区别：** 组合类的问题，每个组合，可能的元素个数是不一样的。可能为空，可能有一个，可能有多个。但是，排列问题，每个都是这么多的元素，看他有多少中可能。
2. 对 visited[] 的操作，思路要清楚
```java
if (visited[i] == false) {
           path.add(nums[i]);
           visited[i] = true;
           helper(nums, path, visited, rst);
           path.remove(path.size() - 1);
           visited[i] = false;
}
```
3. 同样也是四个参数，不过把 pos 换成了 visited[]。因为我们需要记录的不是上次循环的 index，而是这个元素之前访问过没有