https://leetcode.com/problems/insert-delete-getrandom-o1/solution/

...popular statistical algorithms like [Markov chain Monte Carlo](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo) and [Metropolis–Hastings algorithm](https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm). These algorithms are for sampling from a probability distribution when it's difficult to compute the distribution itself.

O(1)
[average insert time](https://wiki.python.org/moin/TimeComplexity):

- Hashmap (or Hashset, the implementation is very similar): [Java HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)/ [Python dictionary](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)
- Array List: [Java ArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)/ [Python list](https://docs.python.org/3/tutorial/datastructures.html)

Problem is a hash function is not truly random, need to spread observations over the space by index.  So delete is the trick:

![image.png](../../../../_resources/image-4.png)

```
/*

- E.g.:

    ["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]

    [[], [1], [2], [2], [], [1], [2], []]
    =>
    [null, true, false, true, 2, true, false, 2]
 */
class RandomizedSet {

    private ArrayList<Integer> dist;
    private Map<Integer, Integer> sampleIndex;

    public RandomizedSet() {
        this.dist = new ArrayList<>();
         this.sampleIndex = new HashMap<>();
    }

    public boolean insert(int val) {
      //System.out.println("Add: " + val + " to " + this.dist);
      //System.out.println("\t   " + this.sampleIndex);
        if (this.sampleIndex.containsKey(val)) return false;
        this.sampleIndex.put(val, this.sampleIndex.size());
        this.dist.add(val);
      //System.out.println("\t=> " + this.dist);
      //System.out.println("\t   " + this.sampleIndex);
      return true;
    }

    public boolean remove(int val) {
      //System.out.println("Rem: " + val + " from " + this.dist);
      //System.out.println("\t   " + this.sampleIndex);
        if (!this.sampleIndex.containsKey(val)) return false;
        int idx = this.sampleIndex.get(val); // idx of val
        int lastVal = this.dist.get(this.dist.size()-1);
        // Pull last dist to idx
        this.dist.set(idx, lastVal);
        // [re]set sampleIndex for lastVal to idx
        this.sampleIndex.put(lastVal, idx);
        this.dist.remove(this.dist.size()-1);
        this.sampleIndex.remove(val);
      //System.out.println("\t=> " + this.dist);
      //System.out.println("\t   " + this.sampleIndex);
      return true;
    }

    public int getRandom() {
      //if (this.dist.size() == 1) return this.dist.get(0);
      int rando = (int) Math.round(Math.random() * (this.dist.size()-1));
      //System.out.println("getRand: " + rando + "\t=> " + this.dist);
      return this.dist.get(rando);
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