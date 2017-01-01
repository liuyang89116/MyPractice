# Task Schedule

> 给了一串 tasks，不同的 task 可能属于不同的 type。这些 task 要放到 CPU 里运行，运行同一种 type 是要考虑一个冷却时间。    
举个例子：thread 是 1,2,3,1 不能改顺序， 冷却时间 3，运行起来就是 1, 2, 3, _, 1 时间就是 5.要返回总运行时间 5.

-------
##思路
* 用 HashMap 来存储 `<task, 时间>`，遇到一个 task 就存到 map 里。
* 下次先扫描 map，如果发现之前已经运行过这个 task，就看是否已经超过等待时间，需要继续等待。

-------------
* 复杂度： `O(n)`

```java
public class Solution {
	public static int taskSchedule(int[] tasks, int cooldown) {
		if (tasks == null || tasks.length == 0) {
			return  0;
		}

		HashMap<Integer, Integer> map = new HashMap<>();
		int slots = 0;
		for (int task : tasks) {
			// if task is already used or need to wait
			if (map.containsKey(task) && map.get(task) > slots) {
				slots = map.get(task);
			}
			map.put(task, slots + cooldown + 1); // next available slot for task
			slots++; // used 1 slot for current task
		}

		return slots;
	}
}
```

