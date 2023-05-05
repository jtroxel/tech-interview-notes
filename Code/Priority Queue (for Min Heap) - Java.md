```java
Queue<Integer> ladderAllocations = new PriorityQueue<>((a, b) -> a - b);
```

The comparator compares a and b, returning -1/0/1 if  `first argument is less than, equal to, or greater than the second.`

Ex using Comparitor from outside DS:

```java
PriorityQueue<>(counts.size(),
                              // order by counts, ascending
                             (n1, n2) -> counts.get(n1) - counts.get(n2));
```