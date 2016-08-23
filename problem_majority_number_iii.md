# Problem: Majority Number III (LintCode)


> http://www.lintcode.com/en/problem/majority-number-iii/

------------
##思路
* 其实和前面几道题的思路是一模一样的。但是我们没法建 k 个 canditate 来维护这些值。我们可以建一个 HashMap 来把 k 个值存起来维护。
* 同样地，Map 里没有这个 key 就建一个，有的话就在之前的基础上加1
* 超过 k 个值的时候，我们就删元素 removeKey()

-----------
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: As described
     * @return: The majority number
     */
    public int majorityNumber(ArrayList<Integer> nums, int k) {
        HashMap<Integer, Integer> counters = new HashMap<Integer, Integer>();
        for (Integer i : nums) {
            if (!counters.containsKey(i)) {
                counters.put(i, 1);
            } else {
                counters.put(i, counters.get(i) + 1);
            }
            
            if (counters.size() >= k) {
                removeKey(counters);
            }
        }
        
        // corner cases
        if (counters.size() == 0) {
            return Integer.MIN_VALUE;
        }
        
        // recalculate counters
        for (Integer i : counters.keySet()) {
            counters.put(i, 0);
        }
        for (Integer i : nums) {
            if (counters.containsKey(i)) {
                counters.put(i, counters.get(i) + 1);
            }
        }
        
        // find the max key
        int maxCounter = 0, maxKey = 0;
        for (Integer i : counters.keySet()) {
            if (counters.get(i) > maxCounter) {
                maxCounter = counters.get(i);
                maxKey = i;
            }
        }
        
        return maxKey;
    }
    
    private void removeKey(HashMap<Integer, Integer> counters) {
        Set<Integer> keySet = counters.keySet();
        List<Integer> removeList = new ArrayList<Integer>();
        for (Integer key : keySet) {
            counters.put(key, counters.get(key) - 1);
            if (counters.get(key) == 0) {
                removeList.add(key);
            }
        }
        
        for (Integer key : removeList) {
            counters.remove(key);
        }
    }
}
```
-----------
##易错点

1. 把整个题目的思路理清楚
**遍元素，不存在键的就创造一个，存在就加1，超过k个元素就删**-> **corner cases** -> **counters归零，重新记数** -> **找最大元素**
2. for 循环 type 要对应
```java
for (Integer i : counters.keySet()) {
        counters.put(i, 0);
}
for (Integer i : nums) {
        if (counters.containsKey(i)) {
             counters.put(i, counters.get(i) + 1);
        }
}
```
这里for循环的条件都是对应着的，当时我错写成 
```for (Integer i : counters)```
counters对应的是一个键值对，根本就不是 Integer，所以是不对的
3. removeKey() 方法
```java
private void removeKey(HashMap<Integer, Integer> counters) {
        Set<Integer> keySet = counters.keySet();
        List<Integer> removeList = new ArrayList<Integer>();
        for (Integer key : keySet) {
            counters.put(key, counters.get(key) - 1);
            if (counters.get(key) == 0) {
                removeList.add(key);
            }
        }
        
        for (Integer key : removeList) {
            counters.remove(key);
        }
}
```
  每个keySet里的值都减去1,如果被减得就剩下 0 了，就把这个key删掉，换人！

































