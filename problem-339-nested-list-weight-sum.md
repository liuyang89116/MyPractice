# Problem 339: Nested List Weight Sum

> [https://leetcode.com/problems/nested-list-weight-sum/?tab=Description](https://leetcode.com/problems/nested-list-weight-sum/?tab=Description)

-----------------

![](/assets/339.png)

---

## 思路

* 搞清如何递归是非常重要的.这里有两个非常重要的参数:一个是 path,另一个是当前的 element
* 递归的时候一层一层地走下去

---

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        return helper(nestedList, 1);
    }

    private int helper(List<NestedInteger> list, int depth) {
        int sum = 0;
        for (NestedInteger element : list) {
            if (element.isInteger()) {
                sum += element.getInteger() * depth;
            } else{
                sum += helper(element.getList(), depth + 1);
            }
        }   

        return sum;
    }
}
```



