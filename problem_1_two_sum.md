# Problem 1: Two Sum


> https://leetcode.com/problems/two-sum/

---------------
##思路
* 用 HashMap 把数组里面的数都存起来，格式是 map.(number, index);
* HashMap 这个做法的时间复杂度是 O(n)，诀窍在于，遍历前面的数的时候，把他存在 map 里 map.(target - nums[i], i)，这样下次遇到后面的数，只有能对上，说明就能组成和为 target 的数组。
* 还有一个**双指针**的方法，O(1) 的 space， O(nlogn) 的时间，下次补上

-------------
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return new int[] {-1, -1};
        }
        
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (map.get(nums[i]) != null) {
                int[] result = new int[] {map.get(nums[i]), i};
                return result;
            }
            map.put(target - nums[i], i);
        }
        
        return new int[] {-1, -1};
    }
}
```

--------
##易错点

1. 题目进行了更新，之前比较傻逼，返回的数组 index 和本身的 index 值差 1，需要手动再加 1 在结果上
2. 中间的 if 判断中，只要有结果，立马就返回。
3. 牢记 map 的方法
map 用的是 put() 方法; set 用的是 add() 方法
```java
map.put(target - nums[i], i);
```
```java
set.add(nums[i]);
```
























