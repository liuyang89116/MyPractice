# Problem 78: Subsets


> https://leetcode.com/problems/subsets/

这道题是集合的基本题目
---------------------
```java
class Solution {
    /**
     * @param S: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */

    ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();

    private void subsetsHelper(ArrayList<Integer> path, int[] nums, int pos) {
        result.add(new ArrayList(path));

        for (int i = pos; i < nums.length; i++) {
            path.add(nums[i]);
            subsetsHelper(path, nums, i + 1);
            path.remove(path.size() - 1);
        }
    }

    public ArrayList<ArrayList<Integer>> subsets(int[] nums) {
        // write your code here
        ArrayList<Integer> path = new ArrayList<Integer>();
        Arrays.sort(nums);
        subsetsHelper(path, nums, 0);
        return result;
    }
}
```
-----------------------
##思路
* 确定待排列的字母，数组，和位置
* 每次把不同的元素加到result里面去
* 加新元素-call自己的方法-最后再把这个元素踢出去 

##易错点
1. 加result中的元素是 ```result.add(new ArrayList(path));``` 
2. 去掉最后一个元素 ```path.remove(path.size() - 1);```
3. 引申一点：数组的length不是方法，后面没有括号;但是size()是一个方法，记得要加括号



