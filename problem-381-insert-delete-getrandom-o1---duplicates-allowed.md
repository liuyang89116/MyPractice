# Problem 381: Insert Delete GetRandom O(1) - Duplicates allowed

> https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/

---------
##思路
* 允许重复元素，这么一个变化，难度增加了不少。很容易在小地方犯错。
* 用 `HashMap<Integer, LinkedHashSet<Integer>>` 来实现 map，这样相同的元素的位置可以不断地挂在后面

--------------


```java
public class RandomizedCollection {
    ArrayList<Integer> list;
    HashMap<Integer, LinkedHashSet<Integer>> map;
    Random rand;

    /** Initialize your data structure here. */
    public RandomizedCollection() {
        list = new ArrayList<Integer>();
        map = new HashMap<Integer, LinkedHashSet<Integer>>();
        rand = new Random();
    }
    
    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    public boolean insert(int val) {
        boolean isContain = map.containsKey(val);
        if (isContain) {
            list.add(val);
            map.get(val).add(list.size() - 1);
            return false;
        } else {
            list.add(val);
            map.put(val, new LinkedHashSet<Integer>());
            map.get(val).add(list.size() - 1);
            return true;
        }
    }
    
    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        boolean isContain = map.containsKey(val);
        if (!isContain) return false;
        
        int curPos = map.get(val).iterator().next();
        map.get(val).remove(curPos);
        if (curPos < list.size() - 1) {
            int lastVal = list.get(list.size() - 1);
            list.set(curPos, lastVal);
            map.get(lastVal).remove(list.size() - 1);
            map.get(lastVal).add(curPos);
        }
        list.remove(list.size() - 1);
        
        if (map.get(val).isEmpty()) {
            map.remove(val);
        }
        
        return true;
    }
    
    /** Get a random element from the collection. */
    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

