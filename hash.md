# Hash
##Operation
* Insert: `O(1)`
* Delete: `O(1)`
* Find: `O(1)`
---------
## Hash Function
* Magic Number 33
```java
int hash(String key) {
    int sum = 0;
    for (int i = 0; i < key.length(); i++) {
        sum = sum * 33 + (int) (key.charAt(i));
        sum = sum % Hash_TableSize;
    }
    return sum;
}
```
-------
## Hash Collision

### 1. Open Hashing
Use **Linked List** to chain different elements on the same position.    
这个 Visualization 挺好的。    
> https://www.cs.usfca.edu/~galles/visualization/OpenHash.html

![](/assets/openHashing.png)

### 2. Closed Hashing
Use **Array** to allocate different elements. If the position is occupied, move to the next available position.  
这个 Visualization 挺好的。      
> https://www.cs.usfca.edu/~galles/visualization/ClosedHash.html

![](/assets/closedHashing.png)

### 3. Rehashing
![](/assets/reHashing.png)



























