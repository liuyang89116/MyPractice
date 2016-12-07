# Problem: Previous Permutation

> http://www.lintcode.com/en/problem/previous-permutation/

---------
##思路
* 这道题和 Next Permutation 的思路是类似的，不过在操作的时候，正好相反。
* Next Permutation 寻求的是从左到右的一个递减的序列，从右向左找到违反的 pivot 然后进行交换；而 Previous Permutation 寻求的是一个递增数列，找到 pivot 然后交换。

---------
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers that's previous permuation
     */
    public ArrayList<Integer> previousPermuation(ArrayList<Integer> nums) {
		if (nums == null || nums.size() == 0) {
		    return nums;
		}
		
		int len = nums.size();
		for (int i = len - 2; i >= 0; i--) {
		    if (nums.get(i + 1) < nums.get(i)) {
		        int j;
		        for (j = len - 1; j > i; j--) {
		            if (nums.get(j) < nums.get(i)) {
		                break;
		            }
		        }
		        swap(nums, i, j);
		        reverse(nums, i + 1, len - 1);
		        
		        return nums;
		    }
		}
		reverse(nums, 0, len - 1);
		return nums;
    }
    
    private void swap(ArrayList<Integer> nums, int i, int j) {
        int tmp = nums.get(i);
        nums.set(i, nums.get(j));
        nums.set(j, tmp);
    }
    
    private void reverse(ArrayList<Integer> nums, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            swap(nums, i, j);
        }
    }

}

```

