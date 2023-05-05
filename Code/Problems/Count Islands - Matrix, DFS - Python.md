Problem: Count Islands - Matrix, DFS - Python

**Trick: Treat islands as graphs and DFS n/s/e/w to add neighbors.**

- **Zero founds**
    

### **General Form for Recursive DFS**

```python
def recurse_dfs(self, row, col, grid):
    print("dfs:", row, col)
  # Base case (when found)
   if ():
     # Return something
    
    # Or recurse down Depth-First
  	for child in children:
         recurse_dfs(row, col, grid)
```

## My Answer

```
```python
class Solution:
  '''
  Number of Islands
  Count the number of islands defined by adjacent land cells (1)
  
  - Adjacency is only horiz and vert
  
  EG:
    [
      ["1","1","0","0","0"],
      ["1","1","0","0","0"],
      ["0","0","1","0","0"],
      ["0","0","0","1","1"]
    ]
    --> 3
    
  Analysis
  BF:  Iterate each cell:
    if 1, check all neighbors.  Keep map of cell indexes to islands
     - check if neighboring land is already allocated
     - when done with "cell-block," add all to new island or first allocated
     
  DIY:  I would trace out borders
    - iterate cells:
      - add to island if cell is 1
      - go east, south, west north
      
  Make graphs, DFS of neighbors
    Similar to DIY, graph = island
    Oh, can 0 matrix cell once added/counted
    - iterate cells:
      - add count cell is 1
      - DFS: go east, south, west north
        - return if cell is 0
        - dfs if cell is 1
        - 0 out cell
  
  
  '''

  def numIslands(self, grid: List[List[str]]) -> int:
    retCount: int = 0
    self.printMatrix(grid)
    for row, cells in enumerate(grid):
      for col, cell in enumerate(cells):
        print("check:", row, col, cell)
        if int(cell) == 1:
          retCount += 1
          print("add:", row, col, retCount)
          self.island_dfs(row, col, grid)
          self.printMatrix(grid)
          grid[row][col] = "0"
    return retCount
  
  def island_dfs(self, row, col, grid):
    print("dfs:", row, col)
    
    if (row < 0 or row > len(grid) - 1
      or col < 0 or col > len(grid[row]) - 1
      or grid[row][col] == "0"):
        return
    grid[row][col] = "0"
    self.island_dfs(row, col+1, grid) # East
    self.island_dfs(row+1, col, grid) # South
    self.island_dfs(row, col-1, grid) # West
    self.island_dfs(row-1, col, grid) # North

  def printMatrix(self, matrix: List[List]):
    return
    for row, cells in enumerate(matrix):
      rowStr = "|"
      for col, cell in enumerate(cells):
        rowStr += cell + "|"
      print(rowStr)
```