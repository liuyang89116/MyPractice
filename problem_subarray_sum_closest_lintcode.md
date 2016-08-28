# Problem: Subarray Sum Closest (LintCode)


> http://www.lintcode.com/en/problem/subarray-sum-closest/

------------------
##思路
* 这道题的思路就是把不同的元素的 index 组成 Pair，这样做的好处就是，将来 sort 这些 Pair 的和，找到最相近的两个，然后他们就是 closest 了。

----------
```java
public class Solution {
    public class Pair {
        int sum;
        int index;
        public Pair(int sum, int index) {
            this.sum = sum;
            this.index = index;
        }
    }

    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number 
     *          and the index of the last number
     */
    public int[] subarraySumClosest(int[] nums) {
        int[] res = new int[2];
        if (nums == null || nums.length == 0) {
            return res;
        }
        
        int len = nums.length;
        if (len == 1) {
            res[0] = res[1] = 0;
            return res;
        }
        Pair[] sums = new Pair[len + 1];
        int prev = 0;
        sums[0] = new Pair(0, 0);
        for (int i = 1; i <= len; i++) {
            sums[i] = new Pair(prev + nums[i - 1], i);
            prev = sums[i].sum;
        }
        Arrays.sort(sums, new Comparator<Pair>() {
            public int compare(Pair a, Pair b) {
                return a.sum - b.sum;
            }
        });
        
        int ans = Integer.MAX_VALUE;
        for (int i = 1; i <= len; i++) {
            if (ans > sums[i].sum - sums[i - 1].sum) {
                ans = sums[i].sum - sums[i - 1].sum;
                int[] temp = new int[] {sums[i].index - 1, sums[i - 1].index - 1};
                Arrays.sort(temp);
                res[0] = temp[0] + 1;
                res[1] = temp[1];
            }
        }
        
        return res;
    }
}
```
--------
##易错点

1. 设置 len + 1 个 Pair 对
```java
Pair[] sums = new Pair[len + 1];
int prev = 0;
sums[0] = new Pair(0, 0);
```
2. 当有 len + 1 个元素的时候，循环到 "<="
```java
for (int i = 1; i <= len; i++) {
        sums[i] = new Pair(prev + nums[i - 1], i);
        prev = sums[i].sum;
}
```
3. comparator 的写法
```java
Arrays.sort(sums, new Comparator<Pair>() {
         public int compare(Pair a, Pair b) {
              return a.sum - b.sum;
         }
});
```
4. 当两个数组大小不一样，一个大小是 len + 1，另一个是 len 的时候，A[i - 1] 对应的是 B[i] (他有 len + 1 个元素)
```java
sums[i] = new Pair(prev + nums[i - 1], i);
```
```java
int[] temp = new int[] {sums[i].index - 1, sums[i - 1].index - 1};
Arrays.sort(temp);
res[0] = temp[0] + 1;
res[1] = temp[1];
```
**sums[i] 的 index 是比 nums[i] 的 index 是要大 1 的**。































