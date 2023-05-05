#matrix-traversal #dfs #code-challenge #dfs #union-find
https://www.educative.io/courses/grokking-coding-interview-patterns-python/gxEWvAZA1xZ


```python


def estimate_water_flow(heights):

    both_heights = []
    y_size = len(heights)
    x_size = len(heights[0])

    for row in heights:
        print(row)

    def dfs_downhill(x, y, par_x, par_y, matrix):
        return (matrix[y][x] <= matrix[par_y][par_x])
 
    def flows_pacific(x, y, par_x, par_y, matrix):
        if x == 0 or y == 0:
            print("Pacific")
            return True
        else:
            return dfs_downhill(x, y, par_x, par_y, matrix)

    def flows_atlantic(x, y, par_x, par_y, matrix):
        if x == x_size-1 or y == y_size-1:
            print("Atlantic")
            return True
        else:
            return dfs_downhill(x, y, par_x, par_y, matrix)

    def flows_to_both(x, y, par_x, par_y, matrix):
        return flows_pacific(x, y, par_x, par_y, matrix) and flows_atlantic(x, y, par_x, par_y, matrix)

    def add_to_found(x, y, matrix):
        both_heights.append((x, y))
        return True

    visited = []

    
    # Outer loop:  iterate through y, x positions until all visited
    # for y in range(0, y_size-1):
    #     for x in range(0, x_size-1):
    #         print(x, y, visited)
    #         
    #             dfs_cell(x, y, heights, visited, flows_to_both, add_to_found)
    dfs_cell(2, 2, heights, visited, flows_to_both, add_to_found)
    return both_heights


def dfs_cell(x, y, matrix, visited, dfs_found, dfs_action):
    ''' Matrix DFS search

    '''
    print([y, y], visited, [x,y] in visited)
    ret_val = [y,y]
    if [x,y] in visited:
        return True
    # Get lists to represent all the valid neighbors
    y_range = getAdjacentList(y, len(matrix))
    x_range = getAdjacentList(x, len(matrix[0]))
    #print(y_range, x_range)
    # Check through each 
    for y_check in y_range:
        for x_check in x_range:
            print("Checking", y_check, x_check, "=", matrix[y_check][x_check])
            visited.append([x,y])
            print("Add to visited", visited)
            if dfs_found(x_check, y_check, x, y, matrix):
                ret_val = dfs_action(x_check, y_check, matrix)
            else:
                return dfs_cell(x, y, heights, visited, flows_to_both, add_to_found)

    return False
# ...  
def getAdjacentList(val: int, size: int):
    return [c for c in range(max(val-1, 0), min(val+1, size-1)+1) if c != val ]


```

#### DFSCustom class
```python
class DfsNode:
    def getChildren(): list

class DfsCustom:
    visited = list()

    def __init__(self, funComplete, funContinue, funVisit, nodesData):
        self.isFound = funComplete
        self.continueSearch = funContinue
        self.doVisit = funVisit
        self.nodesData = nodesData

    def isFound(node, nodesData):
        return self.isFound(node, nodesData)

    def continueSearch(node, parent, nodesData):
        return self.continueSearch(node, parent, nodesData)

    def doVisit(node: DfsNode):
        self.doVisit(node, nodesData)

class MatrixNode(DfsNode):
 
    def __init__(self, x, y, data):
        self.x = x
        self.y = y
        self.data = data

    def getChildren(self, nodesData):
        ret_children = []
        y_range = getAdjacentList(self.y, len(nodesData))
        x_range = getAdjacentList(self.x, len(nodesData[0]))
        for y_check in y_range:
            for x_check in x_range:
                ret_children.append(MatrixNode(x, y, nodesData))

```