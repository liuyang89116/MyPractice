# Problem 119: Pascal's Triangle II


> https://leetcode.com/problems/pascals-triangle-ii/

--------
##思路
* 这道题更简单了，就是上一题只需要找到 row 就可以了

--------
```java
public class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> row = new ArrayList<Integer>();
        if (rowIndex < 0) {
            return row;
        }
        
        for (int i = 0; i <= rowIndex; i++) {
            row.add(0, 1);
            for (int j = 1; j < row.size() - 1; j++) {
                row.set(j, row.get(j) + row.get(j + 1));
            }
        } 
        
        return row;
    }
}
```

