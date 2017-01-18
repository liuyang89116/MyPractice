# Window Sum

* 两个版本

```java
package WindowSum;

import java.util.ArrayList;
import java.util.List;

/**
 * Created by yang on 1/17/17.
 */
public class Solution {
    public List<Integer> getSum(List<Integer> A, int k) {
        List<Integer> rst = new ArrayList<>();
        if (A == null || A.size() == 0) {
            return rst;
        }
        if (k <= 0) {
            return rst;
        }

        int count = 0;
        for (int i = 0; i < A.size(); i++) {
            count++;
            if (count >= k) {
                int sum = 0;
                for (int j = i; j >= i - k + 1; j--) {
                    sum += A.get(j);
                }
                rst.add(sum);
            }
        }

        return rst;
    }

    public int[] getSum(int[] array, int k) {
        if (array == null || array.length == 0) {
            return null;
        }
        if (k <= 0) {
            return null;
        }

        int[] rst = new int[array.length - k + 1];
        for (int i = 0; i < k; i++) {
            rst[0] += array[i];
        }
        for (int i = 1; i < rst.length; i++) {
            rst[i] = rst[i - 1] - array[i - 1] + array[i + k - 1];
        }

        return rst;
    }

}



















```

