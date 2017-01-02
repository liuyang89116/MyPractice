# Problem 398: Random Pick Index

---------
> https://leetcode.com/problems/random-pick-index/

--------
##思路
* 水塘抽样问题，要保证的是第 1 个选中的概率是 1；第 2 个，1/2，第 3 个元素 1 / 3 ……下面是维基的解释
> https://en.wikipedia.org/wiki/Reservoir_sampling
* `Random.nextInt(int n)` 方法返回的是 `[0, n)` 的左闭右开的区间
```
举例说明：
第一个：nextInt(1): [0, 1)，只能返回 0，百分百选中；
第二个：nextInt(2): [0, 2)，返回 0, 1, 选中的概率 1 / 2;
第三个：nextInt(3): [0, 1, 2)，返回 0，1，2，选中的概率 1 / 3
...
```

----------


```java
public class Solution {
    int[] nums;
    Random rand;
    
    public Solution(int[] nums) {
        this.nums = nums;
        rand = new Random();
    }
    
    public int pick(int target) {
        int rst = -1;
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                int x = rand.nextInt(++count);
                if (x == 0) {
                    rst = i;
                }
            }
        }
        
        return rst;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
```


