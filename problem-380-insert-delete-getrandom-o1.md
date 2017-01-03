# Problem 380: Insert Delete GetRandom O(1)


> https://leetcode.com/problems/insert-delete-getrandom-o1/

--------
##思路
* insert() 和 remove() 要再 O(1) 的时间完成，我们很自然地想到用 ArrayList 来实现。那如何才能知道要添加和删除元素的 index 呢？配合一个 HashMap 来记录 (val, position)，这样就可以了。
* 添加还好办，每次在屁股后面加入新来的元素，index 也同时递增。但是删除呢？如果删除掉 list 内的某一个元素，那几乎所有的 index 都会发生改变。解决的办法就是：每次把要删除的元素和 list 里的最后一个元素交换位置，然后我们把最后一个元素删除掉就可以了。
* 随机产生数的话，自然是 Random.nextInt() 函数了。

-----------------


```java
public class RandomizedSet {
    ArrayList<Integer> list;
    HashMap<Integer, Integer> map;
    Random rand;
    
    /** Initialize your data structure here. */
    public RandomizedSet() {
        list = new ArrayList<Integer>();
        map = new HashMap<Integer, Integer>();
        rand = new Random();
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        boolean isContain = map.containsKey(val);
        if (isContain) return false;
        
        list.add(val);
        map.put(val, list.size() - 1);
        
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        boolean isContain = map.containsKey(val);
        if (!isContain) return false;
        
        int curPos = map.get(val);
        if (curPos < list.size() - 1) {
            int lastVal = list.get(list.size() - 1);
            list.set(curPos, lastVal);
            map.put(lastVal, curPos);
        }
        list.remove(list.size() - 1);
        map.remove(val);
        
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

