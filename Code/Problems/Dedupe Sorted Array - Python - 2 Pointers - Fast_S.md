Dedupe Sorted Array - Python - 2 Pointers - Fast/Slow

```python
class Solution:
  '''
  EG:
    [0,0,1,1,1,2,2,3,3,4] -> 5
           |     |
    [0,1,2,3,4,...]
  '''
  def removeDuplicates(self, nums: List[int]) -> int:
    ins_idx= 1
    i = 1 # el 0 can't be dupe
    #last_highest = nums[ins_idx] # set last highest seen
    # Iterate on i, and ins_idx only when a dupe is found
    while (i <= len(nums)-1):
      # if vals are !=, new found 
      if nums[i] != nums[ins_idx-1]: # (idx - 1 is last max seen)
        nums[ins_idx] = nums[i] # copy new into insert idx, inc both
        ins_idx += 1
      i += 1       
    return ins_idx
```