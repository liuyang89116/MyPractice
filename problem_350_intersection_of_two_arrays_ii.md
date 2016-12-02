# Problem 350: Intersection of Two Arrays II
> https://leetcode.com/problems/intersection-of-two-arrays-ii/

-------
##思路
* 这道题和上一题的区别就在于，有重复的元素，并且重复几次就打印几次
* 那么就把 HashSet 改成 HashMap，用来记录出现的次数

-----------
```java
public class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums1.length; i++) {
            int num = nums1[i];
            if (map.containsKey(num)) {
                map.put(num, map.get(num) + 1);
            } else {
                map.put(num, 1);
            }
        }
        
        List<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < nums2.length; i++) {
            int num = nums2[i];
            if (map.containsKey(num) && map.get(num) > 0) { // 如果 map 里有该元素，
                                                            // 那么减到 0 的时候，重复元素
                                                            //也被记录了
                list.add(num);
                map.put(num, map.get(num) - 1);
            } 
        }
        
        int[] rst = new int[list.size()];
        for (int i = 0; i < rst.length; i++) {
            rst[i] = list.get(i);
        }
        
        return rst;
    }
}
```