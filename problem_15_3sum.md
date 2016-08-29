# Problem 15: 3Sum


> https://leetcode.com/problems/3sum/

----------
##思路
* 三个指针一起扫遍整个数组。i 从左到右一直扫一遍（当然它不能都扫完，要留两个位置给 left 和 right）
* left 和 right 其实就是双指针逼近
![](3sum.jpg)

-------------------
```java
public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<Integer> tmp = new ArrayList<Integer>();
        List<List<Integer>> result = new ArrayList(tmp);
        
        if (nums == null || nums.length < 3) {
            return result;    
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
                continue;           // skip duplicate values 
            }
            
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    tmp = new ArrayList<Integer>();
                    tmp.add(nums[i]);
                    tmp.add(nums[left]);
                    tmp.add(nums[right]);
                    result.add(tmp);
                    left++;
                    right--;
                    while (left < right && nums[left] == nums[left - 1]) {
                        left++;
                    }
                    while (left < right && nums[right] == nums[right + 1]) {
                        right--;
                    }
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
            
        }
        
        return result;
    }
}
```
------
##易错点

























