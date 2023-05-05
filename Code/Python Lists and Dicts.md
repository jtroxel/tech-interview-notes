Python Lists and Dicts

### Last element of a list

```python
my_list = [1, 2, 3, 4]
my_last = my_list[-1]
```

### Navigating OrderedDict
```python
# Get first key
next(iter(od))

# Get last key
next(reversed(od))

# Get first value
od[next(iter(od))]

# Get last value
p4intbrush


# Get first key-value tuple
next(iter(od.items()))

# Get last key-value tuple
next(reversed(od.items()))

# Get sorted dict on value
balances = OrderedDict(sorted(nets.items(), key=lambda kv: kv[1]))
```

### Comprehensions

```python
# List from range
my_list = [i for i in range(1, 100)]

# List comp to for odds
#      mapF FOR iter IN list IF condEx]
odds = [i for i in my_list if i % 2 != 0]
print(odds)

# "Dict comprehension" on list with map function
import datetime
from typing import OrderedDict
one_day = datetime.timedelta(days = 1)
#          MapF w/ name: val
my_dict = {i: str(datetime.date.today() + (i * one_day))
    for i in odds}
print(my_dict)
     
```

### Initialize 2-D Matrix (list(list()))
```python
	self.board = [list([0] * n) for r in range(0,n)]
```
### Matrix math trick, iterate on adjacent cells in a 2-d matrix

```python
x = 0 # cur x
y = 0 # cur y
y_range = self.getAdjacentList(y, len(board))

for y_check in y_range:
	print(y_check, x_check, board[y_check][x_check])
    
def getAdjacentList(self, val: int, size: int):
''' get a list object with the values of the axis points around the cell,
	  and also inside the bounds of the array
'''
	return [c for c in range(max(val-1, 0), min(val+1, size-1)+1) ]
```

#### Get Neighbors using Generator
#python/generator #python/yield #python/lists
```python
def getNeighbors(i, j, grid):
    for di, dj in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
      ni, nj = i + di, j + dj
      if 0 <= ni < len(grid) and 0 <= nj < len(grid[i]):
        yield ni, nj
            
for new_i, new_j in getNeighbors(i, j):
	print(new_i, new_j)
```