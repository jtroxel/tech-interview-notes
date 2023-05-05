## Print Array, Map Horizontal with pointer

```java
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
```

## Print Linked-list

```Java
for (ListNode i = newHead; i != null; i = i.next) System.out.print(i.val + ", ");
```