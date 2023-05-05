## Problem LRU Cache

**get, put over a FIFO queue with capacity**

### Python

**Trick:**

- Combination of direct access and a FIFO queue
- Coordination of queue updates, evictions and cache put

```python
'''
Analysis:
  - Need a queue to evict oldest items
  - And need a dict to index by key
  - OR Ordered map / dictionary
'''
  

class LRUCache:
  
    size = 0
    cache: OrderedDict = None
    keys_by_age = None

    def __init__(self, capacity: int):
      self.size = capacity
      self.cache = OrderedDict()
      print(self.__dict__)
    

    def get(self, key: int) -> int:
      # print("get", key)
      if key not in self.cache:
        return -1
      # For gets: must *move* key back to end (most recent).
      #   Note *can't* just add new and pop, will be out of synch with dict
      self.cache.move_to_end(key)
      # print(self.cache)
      return self.cache[key]
        

    def put(self, key: int, value: int) -> None:
      # print("put", key, value)
      
      # For puts, need to update queue and dict, and check for evictions
      # Key in list, move to end (most recent)
      if key in self.cache:
        self.cache.move_to_end(key)
      # Set new value
      self.cache[key] = value # If key is new, will also update list end
      # print(self.cache)
      
      # If exceeded capacity, pop off the oldest from list and same from queue
      if len(self.cache) > self.size:
        # print("pop")
        self.cache.popitem(last=False)
        # print(self.cache)
        


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

### Java - Incomplete

```java
/*
LRU Cache
 - Direct access get (Cahce)
 - LRU eviction (Queue, or fist pointer)
 
 - get not found?  -1


EG: 
  [[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
  ... { 1 => 1; 2 => 2}... + 3 { 2 => 2; 3 => 3}...
  --> [null, null, null, 1, null, -1, null, -1, 3, 4]
  
Analysis
  - Map w/ pointer, simplest?  No still need queue of keys to track LRU
*/

class LRUCache {
  
    private Map<Integer, Integer> cache;
    private int queueSize;
    private PriorityQueue<Integer> lru;

    public LRUCache(int capacity) {
      this.cache = new HashMap<>(capacity);
      this.lru  = new PriorityQueue<Integer>(capacity); // Setting the capacity should cause eviction
      this.queueSize = capacity;
    }
    
    public int get(int key) {
      if (this.cache.containsKey(key)) {
        this.lru.add(key);
        return this.cache.get(key);
      }
      return -1;
    }
    
    public void put(int key, int value) {
      System.out.print("put " + key + ": ");
      if (cache.size() == queueSize) {
        int toDelete = this.lru.iterator().next();
        System.out.println("evicting " + toDelete);
        this.lru.remove(toDelete);
        this.cache.remove(toDelete);
        System.out.println("LRU: " + Arrays.asList(this.lru).toString());
      }
      this.lru.add(key);
      System.out.println("LRU: " + Arrays.asList(this.lru).toString());
      this.cache.put(key, value);
      prettyPrintMap(this.cache, "", 0);
      return;
    }
  
  public void prettyPrintArray(int[] arr, String label, int limit, int idx) {
        StringBuilder ln1 = new StringBuilder();
        StringBuilder ln2 = new StringBuilder();
        ln1.append(String.format("%5s:\t", label));
        ln2.append(String.format("%5s\t", " --> :"));
        for (int i = 0; i < arr.length && i <= limit; i++) {
          ln1.append(String.format("|%5d", i));
          ln2.append(String.format("|%5d", arr[i]));
        }
        ln1.append("|\n");
        ln2.append(String.format("|\n%5s:\t", " "));
        for (int i = 0; i < idx; i++) ln2.append(String.format("|%5s", " "));
        System.out.println(ln1.append(ln2) + "|___/\\| = " + idx);
    
  }
  public void prettyPrintMap(Map<Integer, Integer> map, String label, int limit) {
        StringBuilder ln1 = new StringBuilder();
        StringBuilder ln2 = new StringBuilder();
        ln1.append(String.format("%5s:\t", label));
        ln2.append(String.format("%5s:\t", " --> :"));
        map.forEach((k,v)->{
            ln1.append(String.format("|%5d", k));
            ln2.append(String.format("|%5d", v));
          });
        ln1.append("|\n");
        ln2.append("|\n");
        System.out.println(ln1.append(ln2));
    
  }
  
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```