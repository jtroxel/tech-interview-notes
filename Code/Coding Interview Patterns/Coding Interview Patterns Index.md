#### Sources
- https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#awesome-coding-interview-question-patterns
[[Firestone]]
#### Table

| **Pattern** | **Usage** | **Tricks** |
|:--------------- |:--- |:--- |
| [[Tabulating - Mapping]]<br>["What to Track"](https://www.educative.io/courses/grokking-coding-interview-patterns-python/RMmYnp1WW6O) | *Looks* like `O(n2)`<br> calc, agg., boolean by obsv.<br>2-sum, frequencies | Pivot, array -> map,<br>OrderedDict for 2nd idx |
| **[[Sliding Window]]**<br> ![[Pasted image 20221229091430.png\|150]]<br>**List, Array** | Calc from <ins>All Subarrays</ins> of a <ins>given size (K)</ins>.  Looks like nested, `O(n^2)`<br>BF is `O(K * N)` | Slide the window when `w_end >= K-1`, adjusting the result from both ends |
| **[[Two Pointers]]**<br>![[Pasted image 20221229092902.png\|150]]<br>**<ins>Sorted</ins> List, Array, organized | Deduce about vals either side of pointers<br>Find a pair or subarray. Figure something in a range, between ends (max/min), **in-place**<br>`O(N)` | F/Start: Find & track end & start of range, or last match.<br>Out-in:  Sorted, can move from ends based on criteria<br><ins>Change array in-place (ends visited)</ins>, subset summing to K,<br>*palindrome* |
| (Tree) [[DFS & BFS#**General Form for Recursive DFS** \|DFS]] | Asked <ins>DFS</ins>:  in-order, pre, post<br>Searching for something where the result node is closer to **leaf nodes** | <ins>Recursive</ins> solution:  Use parent param as stack var, copy with `list()`<br>All logic at Node-level.  Check for <ins>None</ins>, then <ins>Base case</ins> (match logic)<br>Then recurse `left, right`.  Use <ins>results passed down</ins>, so no return vals. |
| (Tree) [[DFS & BFS#BFS w/ QUEUE \|BFS]] | Traverse a tree/graph in *level-by-level* order<br>check near root | Use a queue, not recursion.  [[DFS & BFS#BFS w/ QUEUE]] |
| **[Islands (Matrix Traversal)](https://gist.github.com/tykurtz/3548a31f673588c05c89f9ca42067bc4?permalink_comment_id=4294856#gistcomment-4294856)** | Often with DFS or BFS<br>[[Python Lists and Dicts#Matrix math trick, iterate on adjacent cells in a 2-d matrix\|Trick]] |
| [[Top K Elements - Python]]<br>[**Top 'K' Elements**](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#13k-way-merge) | The <ins>top/smallest/frequent ‘K’ elements</ins> among a given set.<br>Best DS for <ins>‘K’ elements is Heap</ins><br>Sort an array to find an exact element | \- Insert ‘K’ elements into the min/max -heap.<br>\- Iterate through the remaining numbers:<br>   \- if you find one that is larger than what you have in the heap, then remove that number and insert the larger one.<br>For "Top Observations":  Keep map with counts, then do Top K on the values/count tuples<br>`from heapq import *` |
| [[Fast & Slow Pointers]] | Finding loops<br>Finding el/position meeting criteria | Fast Ptr moves multiple<br>Fast catch slow == loop |
| [[Dynamic Programming]]<br> ![[Pasted image 20230110114507.png\|100]] | <ins>Overlapping Subproblems</ins>(nested)<br> | `f(n) = f(n-1) + local` |
| [[Back-Tracking]]<br>Tree, Graph, List<br> | <ins>All</ins> **Paths** or **Permutations**<br>Paths can be eliminated part way<br>Combo-sum, Subsets | BFS/DFS + found/cont/bail<br>`start-combo:`<br> - `decide: done/next/backtrack (previous)`. |
| [[Modified Binary Search]] | Find a value in a *sorted* list (or portions of)<br>X Position of<br>Dictionary, folded array, first bad version | [Modified Binary Search](https://www.educative.io/courses/grokking-coding-interview-patterns-python/xo7NXlymxMP) |
| [Merge Intervals](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#4merge-intervals)<br>[Code](../../../../PROFESSIONAL%20DEV/Interview%20Prep/Code/Coding%20Interview%20Patterns/Merge%20Intervals.md) | \- Produce a list with only mutually <ins>exclusive</ins> / <ins>overlapping</ins> intervals.<br>\- <ins>Intersecting</ins>, counting <ins>simultaneous</ins> | Sort intervals on start:  `a.start <= b.start`<br>...OR map ivs like `map[start] = end`<br>If `b.start <= a.end` then there is <ins>Overlap</ins> |
| [[Greedy Algos]]/ Local Optimum<br>Graph, List | **Local Optima** series -> **Global Optima**<br>Filling a container, balancing payments |  |
| **[Subsets](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#10subsets)** | <ins>Combinations</ins>, <ins>Permutations</ins> of a given Set.<br><ins>Subsets</ins> with XXX, <ins>Permutations</ins> of a String | Each iteration adds a num to a copy of all the previous subsets, then appends<br>Start with 1 empty set, add first elem<br>Iterate on orig, then Iterate on subsets:<br>   create a copy of the subset, add orig.elem, and append subset to sets |
| Topological Sort | Partial ordering, dependencies, prereqs |  |
| [**Cyclic Sort**](/Applications/Joplin.app/Contents/Resources/app.asar/They%20will%20be%20problems%20involving%20a%20sorted%20array%20with%20numbers%20in%20a%20given%20range%20If%20the%20problem%20asks%20you%20to%20find%20the%20missing/duplicate/smallest%20number%20in%20an%20sorted/rotated%20array) | They will be problems involving a <ins>sorted array</ins> with numbers in a <ins>given range</ins><br>If the problem asks you to find the <ins>missing/duplicate/smallest</ins> number in an <ins>sorted</ins>/rotated array | Iterate, swap `el[i]` w/ el @ `el[val]` if not =<br> https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#5cyclic-sort |

#### Python Recipes & Idioms

[Helpful Patterns](https://towardsdatascience.com/19-helpful-python-syntax-patterns-for-coding-interviews-3704c15b758f)
 
[**Python Cheat Sheet for Leetcode**](https://leetcode.com/discuss/study-guide/2122306/python-cheat-sheet-for-leetcode)

https://betterprogramming.pub/10-tiny-python-idioms-for-collections-and-data-structures-2f0d2923832

[Binary Search Template](https://leetcode.com/discuss/general-discussion/786126/python-powerful-ultimate-binary-search-template-solved-many-problems)
