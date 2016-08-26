# Problem: Subarray Sum (LintCode)


> http://www.lintcode.com/en/problem/subarray-sum/

---------------
##思路
* subarray 的题目一定要记住经典的 sum 的结构。
* 如图所示
![](subSum.jpg)
* 用一个 HashMap 来存不同的 sum 值（Key），然后 value 是不同的 index

---------------
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number 
     *          and the index of the last number
     */
    public ArrayList<Integer> subarraySum(int[] nums) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        
        int len = nums.length;
        int sum = 0;
        map.put(0, -1);
        for (int i = 0; i < len; i++) {
            sum += nums[i];
            if (map.containsKey(sum)) {
                result.add(map.get(sum) + 1);
                result.add(i);
                return result;
            }
            map.put(sum, i);
        }
        
        return result;
    }
}
```
-----
##易错点
1. 是从 i + 1 到 j
```java
result.add(map.get(sum) + 1);
```
2. 第一个 index = -1，这样 i + 1 这个 index 才能取到 0
```java
map.put(0, -1);
```
3. 找到一个值立马return
```java
if (map.containsKey(sum)) {
          result.add(map.get(sum) + 1);
          result.add(i);
          return result;
}
```


























