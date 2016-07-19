# Problem 165: Compare Version Numbers

> https://leetcode.com/problems/compare-version-numbers/

-----------------------------------
## 思路
1. 把version string parse成两个```String[]```,然后比较对应的数组的值
2. 一个问题是：1.1 和 1.1.3.4 怎么比？

  我们可以首先把他们补齐，取两者长的为他们的长度
-------------------------
```java
public class Solution {
	public int compareVersion(String version1, String version2) {
		String[] arr1 = version1.split("\\.");
		String[] arr2 = version2.split("\\.");
		int length = arr1.length > arr2.length ? arr1.length : arr2.length;

		for (int i = 0; i < length; i++) {
			Integer v1 = i < arr1.length ? Integer.parseInt(arr1[i]) : 0;
			Integer v2 = i < arr2.length ? Integer.parseInt(arr2[i]) : 0;
			if (v1 > v2) {
				return 1;
			} else if (v1 < v2) {
				return -1;
			} else {
				continue;
			}
		}

		return 0;
	}
}
```

--------------------------------------------
##易错点

1. split字符串
  
   对于普通的字符，我们可以通过简单的```String[] arr = s.split(",");```来parse; 但是对于特殊字符
   我们需要有特别的方法```String[] str1 = version1.split("\\.");```和"."一样的字符还有"|",
   ```String[] str1 = version1.split("\\|");```
   > http://javadevnotes.com/java-string-split-tutorial-and-examples
2. String转数字
   ```java
   int a = Integer.parseInt(str);
   Double b = Double.parseDouble(str);
   ```


  

