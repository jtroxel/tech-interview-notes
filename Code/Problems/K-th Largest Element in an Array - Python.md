K-th Largest Element in an Array

```python
class Solution:
  '''
  Kth Largest Element in an Array
  
  - Not distinct
  
  EG: [3,2,3,1,2,4,5,5,6], k = 4 -->
      [1, 2, 2, 3, 3, 4, 5, 5, 6]
                      ^*  
  '''
  def findKthLargest(self, nums: List[int], k: int) -> int:
    sorted_list = sorted(nums)
    return sorted_list[-1 * k]
```