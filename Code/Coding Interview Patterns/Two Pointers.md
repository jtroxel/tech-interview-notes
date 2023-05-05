[GitHub](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#22-pointers-or-iterators)
[**LC Problems**](https://gist.github.com/tykurtz/3548a31f673588c05c89f9ca42067bc4#pattern-two-pointers)<br>[pattern code](../../../../PROFESSIONAL%20DEV/Interview%20Prep/Code/Coding%20Interview%20Patterns/Two%20Pointers.md)

## Leader / trailer from start pattern - Code

```python
# From start
  nextElement = 0  # index of the next element which is not 'key'
  # i is leader, always advance
  for i in range(len(arr)):
    if conditionToAdvanceTrailer(arr, nextElement, i):
      arr[nextElement] = arr[i]
      nextElement += 1

  return nextElement
```

## Outside-in pattern - Code

```python
left, right = 0, len(arr) - 1
  while(left < right):
    current_sum = arr[left] + arr[right]
    
    if foundCondition(arr, left, right):
      return [left, right]

    # we need a larger left
    if increasingCondition(arr, left, right):
      left += 1  
    else: # need smaller right
      right -= 1  # we need a pair with a smaller sum
```


