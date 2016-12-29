# Arithmetic operation combination

> 给一个string “123456789”， 进行 arithmetic oepration combination.  比如： 123 ＋ 456 ＋ 78 －9 是一种组合， -1+2-3+4+5+6+78+9 也是一种(只用加 ＋ 或 -), 打印出所有结果等于 100 的组合

---------
##思路
* 这道题类似于 LC 282 Expression Add Operators
* DFS 递归

-------


```java
import java.util.ArrayList;
import java.util.List;

/*
 * 给一个string “123456789”， 进行 arithmetic oepration combination.  
 * 比如： 123 ＋ 456 ＋ 78 －9 是一种组合， -1 + 2 -3 ＋4 -5 - 67 ＋ 89 也是一种(只用加 ＋ 或 -), 
 * 打印出所有结果等于 100 的组合
 */
public class Operations {
	public static List<String> addOperation(String num, int target) {
		List<String> rst = new ArrayList<String>();
		if (num == null || num.length() == 0) {
			return rst;
		}

		helper("", rst, num, target, 0, 0);

		return rst;
	}

	private static void helper(String path, List<String> rst, String num, int target, int pos, long calc) {
		if (pos == num.length()) {
			if (calc == target) {
				rst.add(path);
				return;
			}
		}

		for (int i = pos; i < num.length(); i++) {
			if (num.charAt(pos) == '0' && i != pos)
				break;

			long cur = Long.parseLong(num.substring(pos, i + 1));

			helper(path + "+" + cur, rst, num, target, i + 1, calc + cur);
			helper(path + "-" + cur, rst, num, target, i + 1, calc - cur);
		}
	}

	public static void main(String[] args) {
		String s = "123456789";
		List<String> rst = addOperation(s, 100);

		for (String str : rst) {
			System.out.println(str);
		}
	}
}

```

