Top K Elements - Python
![91a14025e8e60c58504ddbf8201d6b1e.png](../../../../_resources/91a14025e8e60c58504ddbf8201d6b1e.png)

```python
from heapq import *


def find_k_largest_numbers(nums, k):
  minHeap = []
  # put first 'K' numbers in the min heap
  for i in range(k):
    heappush(minHeap, nums[i])

  # go through the remaining numbers of the array, if the number from the array is bigger than the
  # top(smallest) number of the min-heap, remove the top number from heap and add the number from array
  for i in range(k, len(nums)):
    if nums[i] > minHeap[0]: # "top" of heap
      heappop(minHeap)
      heappush(minHeap, nums[i])

  # the heap has the top 'K' numbers
  return minHeap


def main():

  print("Here are the top K numbers: " +
        str(find_k_largest_numbers([3, 1, 5, 12, 2, 11], 3)))

  print("Here are the top K numbers: " +
        str(find_k_largest_numbers([5, 12, 11, -1, 12], 3)))


main()

```

### Top Frequencies
```python
from heapq import *
def find_k_frequent_numbers(nums, k):
  topNumbers = []
  frequencies = {}
  for i, num in enumerate(nums):
    if num not in frequencies:
      frequencies[num] = 1
    else:
      frequencies[num] += 1
  for num, freq in frequencies.items():
    heappush(topNumbers, (freq, num))
    if len(topNumbers) > k:
      heappop(topNumbers)
  return [num[1] for num in reversed(topNumbers)]

def main():

  print("Here are the K frequent numbers: " +
        str(find_k_frequent_numbers([1, 3, 5, 12, 11, 12, 11], 2)))

  print("Here are the K frequent numbers: " +
        str(find_k_frequent_numbers([5, 12, 11, 3, 11], 2)))


main()


```