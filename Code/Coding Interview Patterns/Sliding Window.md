[Educative](https://www.educative.io/courses/grokking-the-coding-interview/7D5NNZWQ8Wr)**<br>**[LC Problems](https://leetcode.com/problems/maximum-subarray/solutions/1126554/maximum-subarray/)

#### Code - Max Subarray (Kadanes)
```python
def max_sub_array(nums):
  
    current_sub = nums[0]
    max_sub = current_sub

    for i, num in enumerate(nums[1:]):
        candidate = current_sub + num
        current_sub = max(candidate, num) # start current over if less than the current num
        max_sub = max(max_sub, current_sub) # capture new global max
    return max_sub

```
![[Pasted image 20221211144003.png]]

#### Problems
#two-sum (sorted)

