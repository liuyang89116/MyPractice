# Problem 167: Two Sum II - Input array is sorted

> https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

-----
##思路
* 参考高频题目里面的 Two Sum
* 依然是双指针法，这道题更简单的原因是，他已经把数组 sort 好了

-----
```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] result = new int[2];
        if (numbers == null || numbers.length < 2) {
            return result;
        }
        
        int left = 0;
        int right = numbers.length - 1;
        while (left < right) {
            if (numbers[left] + numbers[right] == target) {
                return new int[] {left + 1, right + 1};
            } else if (numbers[left] + numbers[right] < target) {
                left++;
            } else {
                right--;
            }
        }
        
        return result;
    }
}
```
```java
/*
  HashMap 做法
*/
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < numbers.length; i++) {
            if (map.containsKey(numbers[i])) {
                return new int[] {map.get(numbers[i]), i + 1};
            } else {
                map.put(target - numbers[i], i + 1);
            }
        }
        
        return new int[] {0, 0};
    }
}
```


