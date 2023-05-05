**Trick: Using a Priority Queue as a \[Max\] Heap**

Basically we can iterate once

- Allocate a ladder if not all used
- Then take the ladder for the smallest climb and use bricks on it
- If bricks are all used up, return last pos

> We decided above that the strategy we'll use is to use a ladder if we have one available. If we're out of ladders, we'll replace the most wasteful ladder allocation with bricks. In code, this means we'll need a data structure that we can insert climbs into, and then when needed, retrieve the smallest climb. The data structure we use for this is a  **heap**, also known as a  **priority queue**.
> 
> > Recall that a  **heap**  is a data structure that allows us to efficiently perform two operations: inserting items with a priority and retrieving and/or removing the item with the highest priority. In some cases, such as this problem, the priority is calculated from the inserted item itself with a priority function, removing the need for an explicit priority to be inserted.

```Java
/*
Furthest Building You Can Reach - Bricks and Ladders
  Optimize the buildings you can reach with the provided bricks and ladders
  
- 0 possible? - yes

 
 EG:  heights = [4,2,7,6,9,14,12], bricks = 5, ladders = 1 --> 7 
 
 Analysis
 
 - Want to use ladders for longest, then bricks
 
 - BF:
    - outter:  
      - use all ladders, use all  -  (-) 2*N
        - inner: from i+1, use up ladders then bricks - N
      
    
  - DIY:  I would place bricks until I ran out.  Track biggest cost so far, sorted map to poc
    - then back up to biggest pos, place a ladder, then continue .. O(n * log(N)) ?
    
    - keep sorted map of climb to pos.  keep a counter for bricks used and ladders used
    - iterate through heights, while bricksUsed < bricks:
      - increment bricksUsed
      - add to map
      - once we've iterated through, we rejigger the counters
        - place ladders at the top heights (sutract those heights from bricks used)
      - once replacing the ladders doesn't add more bricks, we'll fall out
 
 
 */
class Solution {
    public int furthestBuilding(int[] heights, int bricks, int ladders) {
      
//       TreeMap<Integer, Integer> climbs = new TreeMap<>();
       Queue<Integer> ladderAllocations = new PriorityQueue<>((a, b) -> a - b);

      int bricksUsed = 0;
    
      // prettyPrintArray(heights, "Bldgs", heights.length, 0);
      for (int i = 0; i < heights.length -1; i++) {
        int climb = heights[i + 1] - heights[i];
        if (climb < 1) continue;
//        climbs.put(climb, i);
        
        System.out.println();
//        prettyPrintMap(climbs, "Climb", i);
        bricksUsed += climb;

        // Otherwise, allocate a ladder for this climb.
        ladderAllocations.add(climb);
        // If we haven't gone over the number of ladders, nothing else to do.
        if (ladderAllocations.size() <= ladders) {
            continue;
        }
        // Otherwise, we will need to take a climb out of ladder_allocations
        bricks -= ladderAllocations.remove();
        // If this caused bricks to go negative, we can't get to i + 1
        if (bricks < 0) {
            return i;
        }

        // prettyPrintArray(heights, "Bldgs", i, i);
        // System.out.printf("END\ti: %d; bldg: %d; climb: %d; bricksUsed: %d\n", i, heights[i], climb, bricksUsed);
        
      }
      System.out.println("-----");
        // If we got to here, this means we had enough materials to cover every climb.
        return heights.length - 1;
        
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
```