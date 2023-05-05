## Desc

You are given a 2D matrix with 0's and 1's. **1**represents Land. \*\*0 \*\*represents Water. Find the number of islands in the matrix.

*Note*: Connections need to be top-down or left-right. Diagonals 1's don't count as land connections.

![2JdRTVThTDqr9tEQEXcl](../../../../_resources/2JdRTVThTDqr9tEQEXcl)

**TRICK: DFS for contiguous neighbors, +1 per search. 0 out visited (or track otherwise)**

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
      - go east, south, west north, as far as possible
      
  Make graphs, DFS of neighbors
    Similar to DIY, graph = island
    Oh, can 0 matrix cell once added/counted (instead of keeping separate visited or allocated DS)
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

## Original Attempt

### ESTCV ([Coding Question Approach](Coding%20Question%20Approach.md))

Examples:
\[ 0 \] = 0
\[ 1 \] = 1
\[ 1 0
  0 1 \] = 0 (diagonals don't count)
0 1
0 1 = 1

- boundaries don't "roll over" ?
- are there NFRs?  time or space concerns?  let's say time complexity

Solutions:

- Brute force.  \[Nested?\] array traversal, visit NSEW, keep Map of coordinate -> islands.
    - O(n) compute, 2n space
    - Do we need to keep separate structure?
- Recursive:  visit = visit E,S
    - count = (par == false and this  == true) + children
    - O-n time, O-n space
    - Bad usability
- Reuse matrix
    - Mark with island #
- Brute force with Skip nexts
    - Can we use width \[and height\] to skip checks?
        
    - ~~Starting with pos = nw~~
        
    - ~~Check island (n=0, e=0, north-size = 0, island-count = 0)~~
        
        - ~~If island:~~
            - ~~Check east neighbors, checkIsland(n, e, north-size, island-count+1)~~
                - ~~count x-size~~
                - ~~mark with island #~~
                - ~~return x-size~~
            - ~~Check south neighbors, , checkIsland(nw-pos + 1, north-size, island-count+1)~~
                - ~~from nw to x-size~~
                    - ~~mark 1s with island #~~
    - ~~Go to pos = x-size + 1~~
        

Code:

(stubs & comments)

```
public countIslands(
ArrayList<ArrayList<Integer>> landMatrix) {
  # traverse cells
  for (Integer row : landMatrix) {
      for (Integer col : landMatrix.get(row) {
  # List neighbors
      }
  }

```