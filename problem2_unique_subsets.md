# Problem 90: Unique Subsets 


> https://leetcode.com/problems/subsets-ii/

这道题的一个改变是有重复的元素
-----------------------
```java
public class Solution {
    List<Integer> path = new ArrayList<Integer>();
    List<List<Integer>> result = new ArrayList(path);

    public List<List<Integer>> subsetsWithDup(int[] num) {
        Arrays.sort(num);
        subsetsHelper(path, num, 0);
        return result;
    }

    private void subsetsHelper(List<Integer> path, int[] num, int pos) {
        result.add(new ArrayList(path));

        for (int i = pos; i < num.length; i++) {
            if (i > 0 && i > pos && num[i] == num[i - 1]) {
                continue;
            }
            path.add(num[i]);
            subsetsHelper(path, num, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```
----------------------
##易错点
1. 排除重复元素。这道题是在普通的Subsets题目上的延伸，关键的难点在于在之前的模板上稍作调整，去掉重复元素的干扰。
```java 
if (i > 0 && i > pos && num[i] == num[i - 1]) {
         continue;
}
```
```i > 0``` 控制 ```num[i-1]``` 空指针的情况
```i > pos```表示第一个元素不用管
2. 两层嵌套如何初始化
```java
List<List<Integer>> result = new List<List<Integer>>();
```
这是一个典型的错误，首先List是接口，必须找到他的实现类！ 比如ArrayList才可以初始化。所以，

```java
List<Integer> path = new ArrayList<Integer>();
List<List<Integer>> result = new ArrayList(path);
```





