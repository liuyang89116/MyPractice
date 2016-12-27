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

