# Random Non-Empty Slots

> 给定一个数字 n, 代表从 1 -> n  n 个 slots，再给一个数组存着空 slot 的 id. 让你同概率下 randomly 返回一个非空的 slot.



```
example:
n = 8, slots: 1,2,3,4,5,6,7,8
emptycells = {3, 5}
non empty cells: 1,2,4,6,7,8
return one of non empty cells randomly with equal probability.
```
----
##思路
* 用双指针把 non-empty 的元素 merge 到一个数组里，然后 randomly 返回数组的 index。

--------


```java
import java.util.Random;

/**
 * Created by yang on 1/3/17.
 */
public class Solution {
    public static int randomSlot(int n, int[] empty) {
        if (empty.length > n) return 0;
        Random rand = new Random();
        int[] left = new int[n - empty.length];
        int i = 0, j = 0, index = 0;
        while (index < left.length) {
            if (j < empty.length) {
                if (empty[j] == i + 1) {
                    j++;
                    i++;
                    continue;
                }
            }

            left[index] = ++i;
            index++;
        }

        /*for (int num : left) {
            System.out.print(num + " ");
        }*/

        return left[rand.nextInt(left.length)];
    }

    public static void main(String[] args) {
        int[] empty = new int[]{3, 5};
        for (int i = 0; i < 15; i++) {
            int rst = randomSlot(8, empty);
            System.out.println(rst);
        }
    }
}

```

