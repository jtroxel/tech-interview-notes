Problem - Top K Frequent Elements (ints)

**Trick - Map to keep # to counts, Max Heap (priorityQueue) to order by count**

**![cdf08feb22862f480cbc93980ce23f2a.png](../../../../_resources/cdf08feb22862f480cbc93980ce23f2a.png)**

```java
/* Top K Frequent Elements

- No ties

EG:  [1,1,1,2,2,3], 2 --> [1,2]

*/

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if (k == nums.length) {
            return nums;
        }
        
        Map<Integer, Integer> counts = new HashMap();
      
      for (int num : nums) {
        if (!counts.containsKey(num)) {
          counts.put(num, 0);
        }
        counts.put(num, counts.get(num) + 1);
      }
      prettyPrintMap(counts, "counts", 0);
      
      PriorityQueue<Integer> maxHeap 
        = new PriorityQueue<>(counts.size(),
                              // order by counts, ascending
                             (n1, n2) -> counts.get(n1) - counts.get(n2));
      
        // 2. keep k top frequent elements in the heap
        // O(N log k) < O(N log N) time
        for (int n: counts.keySet()) {
          maxHeap.add(n);
         // maxHeap.forEach(i -> System.out.printf("%5d|", i));
          if (maxHeap.size() > k) {
            int popped = maxHeap.poll(); // pop off f
            //System.out.printf(" ... pop %d", popped);
          }
          //System.out.println();
        }
      
        return maxHeap.stream().mapToInt(myInt-> myInt).toArray();

        // 3. build an output array
        // O(k log k) time
        // int[] top = new int[k];
        // for(int i = k - 1; i >= 0; --i) {
        //     top[i] = maxHeap.poll();
        // }
        // return top;
      
        
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
```