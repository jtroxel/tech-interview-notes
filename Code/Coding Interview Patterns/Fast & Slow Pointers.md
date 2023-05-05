 [Fast & Slow Pointers](https://github.com/MahdiMashrur/Awesome-Coding-Interview-Question-Patterns#3fast-and-slow-pointers-or-iterators)<br>[Pattern Code](../../../../PROFESSIONAL%20DEV/Interview%20Prep/Code/Coding%20Interview%20Patterns/Fast%20&%20Slow%20Pointers.md)
 
Find Cycle (linked-list)

```python
def find_cycle_length(head):
  slow, fast = head, head
  while fast is not None and fast.next is not None:
    fast = fast.next.next
    slow = slow.next
    if slow == fast:  # found the cycle
      return calculate_cycle_length(slow)

  return 0


def calculate_cycle_length(slow):
  current = slow
  cycle_length = 0
  while True:
    current = current.next
    cycle_length += 1
    if current == slow:
      break
  return cycle_length
```

Happy Numbers - Sum of Squares
```python
from sum_of_digits import sum_digits
def is_happy_number(n):
    slow = n
    fast = sum_digits(slow)
    while fast != 1 and fast != slow:
        slow = sum_digits(slow)
        fast = sum_digits(fast)
    return (fast == 1)

```

