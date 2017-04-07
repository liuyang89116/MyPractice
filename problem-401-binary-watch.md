# Problem 401: Binary Watch

> https://leetcode.com/problems/binary-watch/\#/description

-------

## 思路

* 我们的目标就是通过排列组合的方式，找出所有的 time 组合。

---------

```java
public class Solution {
    public List<String> readBinaryWatch(int num) {
        List<String> rst = new ArrayList<String>();
        
        int[] nums1 = new int[]{8, 4, 2, 1};
        int[] nums2 = new int[]{32, 16, 8, 4, 2, 1};
        for (int i = 0; i <= num; i++) {
            for (Integer h : getSumList(nums1, i)) {
                if (h > 11) continue;
                for (Integer m : getSumList(nums2, num - i)) {
                    if (m > 59) continue;
                    String time = h + ":" + (m > 9 ? m : "0" + m); 
                    rst.add(time);
                }
            }
        }
        
        return rst;
    }
    
    private List<Integer> getSumList(int[] nums, int count) {
        List<Integer> list = new ArrayList<>();
        getSumListHelper(nums, count, 0, 0, list);
        
        return list;
    }
    
    private void getSumListHelper(int[] nums, int count, int pos, int sum, List<Integer> list) {
        if (count == 0) {
            list.add(sum);
            return;
        }
        
        for (int i = pos; i < nums.length; i++) {
            getSumListHelper(nums, count - 1, i + 1, sum + nums[i], list);
        }
    }
}


```



