# Problem 67: Add Binary

>https://leetcode.com/problems/add-binary/

--------
##思路
* 逐位加法
* 配合两根指针从后往前扫，最后检查有没有剩下的

---------------
```java
public class Solution {
    public String addBinary(String a, String b) {
        if (a.length() < b.length()) {
            String tmp = a;
            a = b;
            b = tmp;
        }
        
        int pa = a.length() - 1, pb = b.length() - 1;
        int carrier = 0;
        String rst = "";
        while (pb >= 0) {
            int sum = carrier + (int)(a.charAt(pa) - '0') + (int)(b.charAt(pb) - '0');
            rst = String.valueOf(sum % 2) + rst;
            carrier = sum / 2;
            pa--;
            pb--;
        }
        while (pa >= 0) {
            int sum = carrier + (int)(a.charAt(pa) - '0');
            rst = String.valueOf(sum % 2) + rst;
            carrier = sum / 2;
            pa--;
        }
        
        if (carrier == 1) {
            rst = "1" + rst;
        }
        
        return rst;
    }
}
```
-----
##易错点
1. char 转 int
```java
int sum = carrier + (int)(a.charAt(pa) - '0') + (int)(b.charAt(pb) - '0');
```
2. String 转 int
```java
rst = String.valueOf(sum % 2) + rst;
```
3. 开头交换数字，保证长短的顺序
```java
if (a.length() < b.length()) {
         String tmp = a;
         a = b;
         b = tmp;
}
```



























