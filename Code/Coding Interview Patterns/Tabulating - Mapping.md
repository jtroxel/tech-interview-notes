#### Problem Ex:
https://www.educative.io/courses/grokking-coding-interview-patterns-python/N0ZJEAjl2zK

### Ex Code, General form
#code-interview #tracking #contains-duplicate
```python
def contains_duplicate(nums):
    ''' Returns True if nums contains any duplicate
    '''
    # mapping num to count (or existence)
    nums_found = dict()
    for n in nums:
        # If dupe so far bail with True
        if isFound(n, nums_found):
            return True
        else:
            # else track it
            trackFound(n, nums_found)
    return False

```

#### EX: Two-Sum
Note: for unsorted.  If sorted use [[Sliding Window]] & Kadane's
#code-interview #two-sum 
```python
    '''
    Problem:  For the given array of integers arr and a target t, 
    you have to identify the two indices that add up to generate the target t.
    Moreover, you can’t use the same index twice, and there will be only one solution.

    EX: [-4,-8,0,-7,-3,-10], -15 -> -8, -7

    Analysis
    - Sounds like "tracking" ...  what have we seen before?
    - What to track:  Diff with target, so when we see that value we know the 
        metching index
    '''
    visited = {}

    for i, current in enumerate(arr):
        diff = t - current
        # print(i, current, diff, visited)
        if diff in visited.keys():
            # print("Found", diff)
            return [visited[diff], i]
        visited[current] = i
    return []
 
```