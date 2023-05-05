DFS & BFS - Python
[**ACIQP BFS**](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#7tree-bfs)

[[Tree DS Notes]]

### General Form for Recursive DFS (Python)

```python
def recurse_dfs(node, data, visited):
 
	# Base case (when FOUND), pop result up
	#			equivalent to empty stack?
	if found(node):
		return True# return value or add to data
	# Backtracking (?): Check if continuing down is still valid (Optional)
	if not canContinue(node):
		return False
    # Or recurse down Depth-First
  	for child in getChildren(node):
	  	# For graphs, diff paths
	  	if child in visited:
		  	continue
		visited.append(children)
		if recurse_dfs(row, col, grid):
			return True
			# Or continue if multiple results are valid
```

#### Problems
[[Subtree of Another Tree]]


### General Form for BFS (Breadth-First)

BFS means check all children before recursing into each child.

#### BFS using QUEUE (Don't recurse) (Python)

```python

def found(node):
	return True # Conditional logic for "found"
def getChildren(node) -> List:
	return [] # Get left, right; or N/S/E/W, etc
	
queue.append(root)
while not queue.is_empty():
	# Dequeue a vertex/node from queue and add it to result
	current_node = queue.pop(0) # ordequeue()
	# Visit current node
	if found(current_node):
	   return True;
	# Get adjacent vertices/children to the current_node from the list,
	# and if they are not already visited then enqueue them in the Queue
	
	for child in getChildren(node):
		if not visited[child.data]: #visited only necessary if cycle is possible
			queue.enqueue(child.data) # or append(...)
			visited[child.data] = True  # Visit the current Node
			result += visit(child)
    return result

```


[**(Tree) Depth-first Search**](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#8tree-dfs)
BFS tips
```python
append(n)
popleft()
```
while note done, pop from queue:<br>\- for all children (use `range in len()`)
- append to current level, add children to queue
- append current level to results

### Jump Game II, Array BFS (Java)
```java
class Solution {
    /**
     EX1: [3,2,0,1,1,4] -> true
 
    Analysis
    - Forwards search:  DFS?  Try each combo of jump-counts, recursively
    - Backwards (BFS): Search remaining to left for any spot that gets you to the current one.
	    cur = n-1. from cur..0
        while val < pos-diff:
            if i <= 0:
                false
            update cur
     */
    public boolean canJump(int[] nums) {
        if (nums.length == 1) return true;
        int last = nums.length-1;
        int curi = last-1;
        do {
            int diffi = last - curi;
            int cur = nums[curi];
            if (cur >= diffi) {
                if (curi == 0) {
                    return true;
                }
                last = curi;
            }
            curi -= 1;
        }  while (curi >= 0);
        return false;
    }
}

```