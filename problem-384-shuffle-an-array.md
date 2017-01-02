# Problem 384: Shuffle an Array

> https://leetcode.com/problems/shuffle-an-array/

-----------
##思路
* 同样的思路，克隆一个数组，遍历数组的时候，每次随机生成一个 index，然后与当前的元素交换位置
* 注意 Random 是左开右闭的区间，所以`rand.nextInt(i + 1);`

---------


```java
public class Solution {
    int[] nums;
    Random rand;

    public Solution(int[] nums) {
        this.nums = nums;
        rand = new Random();
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }
    
    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        int[] tmp = nums.clone();
        for (int i = 0; i < tmp.length; i++) {
            int j = rand.nextInt(i + 1);
            swap(tmp, i, j);
        }
        
        return tmp;
    }
    
    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```

