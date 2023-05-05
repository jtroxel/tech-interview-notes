Subsets (copy and append)

```python
def find_subsets(nums):
  subsets = []
  # start by adding the empty subset
  subsets.append([])
  # Iterate on input
  for currentNumber in nums:
    # take all current subsets and insert the current number in them to create new subsets
    # 3 ->  [[], [1]] # second step for [1, 3]
    print("%d -> " % currentNumber, subsets)
    n = len(subsets) # Need *current* len because list will change
    # Iterate on current subsets
    for i in range(n):
      # create a new subset from the existing subset and insert the current element to it
      # [], [1]
      set1 = list(subsets[i]) # Pull out subset, list() makes copy
      # [3], [1] # Add 3 to empty (next iter would add 3 to [1])
      set1.append(currentNumber) # add cur to subset
      subsets.append(set1) # append the subset with this currentNum to subsets from start of loop
      # [[], [1], <-- [3], [1]]
  # --> [[], [1], [3], [1, 3]]
  print(" --> ", subsets)
```