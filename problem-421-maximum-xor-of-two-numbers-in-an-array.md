# Problem 421: Maximum XOR of Two Numbers in an Array

> https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/?tab=Description

-----

## 思路

* 看了答案还是有些不太明白，下面这个讲解比较清楚

> https://discuss.leetcode.com/topic/63213/java-o-n-solution-using-bit-manipulation-and-hashmap

-----

```java
public class Solution {
    public int findMaximumXOR(int[] nums) {
        int mask = 0, max = 0;
        for (int i = 31; i >= 0; i--) {
            mask |= (1 << i);
            HashSet<Integer> set = new HashSet<Integer>();
            for (int num : nums) {
                set.add(num & mask);
            }
            
            int tmp = (max | (1 << i));
            for (int prefix : set) {
                if (set.contains(tmp ^ prefix)) {
                    max = tmp;
                }
            }
        }
        
        return max;
    }
}
```



