# Problem: Sort Letters by Case (LintCode)

> http://www.lintcode.com/en/problem/sort-letters-by-case/

---------
##思路
* 这就是 Partition Array 的变种题目，用到的思路也是 Quick Sort

--------
```java
public class Solution {
    /** 
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] chars) {
        int left = 0;
        int right = chars.length - 1;
        while (left <= right) {
            while (left <= right && Character.isLowerCase(chars[left])) {
                left++;
            }
            while (left <= right && Character.isUpperCase(chars[right])) {
                right--;
            }
            if (left <= right) {
                char tmp = chars[right];
                chars[right] = chars[left];
                chars[left] = tmp;
                left++;
                right--;
            }
        }
        
        return;
    }
}
```
--------
##易错点
1. 因为上一步骤有移动指针的情况，所以再下一步条件判断之前，要带上上一步的条件，判断是否符合
```java
while (left <= right) {
         while (left <= right && Character.isLowerCase(chars[left])) {
               left++;

         }
         ...
}
```
2. 用 while 判断而不是 if，因为有可能连着几个都是 lowercase
```java
while (left <= right && Character.isLowerCase(chars[left])) {
         left++;
}
``` 


































