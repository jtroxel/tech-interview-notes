#back-tracking

[Popular LC Post - Various DFS/Backtracking](https://leetcode.com/problems/combination-sum-ii/solutions/750378/python3-dfs-solutions-templates-to-6-different-classic-backtracking-problems-more/?orderBy=most_votes&languageTags=python3)

#### Combo Sum (Reuse Elements)
```python
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:

        def dfs(idx, path, cur, level=0):
            print(level * '\t', cur, target, res)
            if cur > target: return # Bail
            if cur == target: # Done
                res.append(path)
                return
            # Continue: try cur (sum from up-stack), + each candidate 
            for i in range(idx, len(candidates)):
                dfs(i, path+[candidates[i]], cur+candidates[i], level+1)

        if not candidates: return []
        res = []
        candidates.sort()
        dfs(0, [], 0)
        return res

```

#### Combo Sum II (Can't reuse elements)
[40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/discuss/?currentPage=1&orderBy=recent_activity&query=)

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        candidates.sort() # sorting makes it like 2-pointers
        print(candidates, target)
        def dfs(idx, path, cur, level=0):
            print(level*'\t', "dfs at", idx, "cur total =", cur, path, res)
            if cur > target: return # skip
            if cur == target: # Found
                res.append(path)
                return
            for i in range(idx, len(candidates)):
                print(level*'\t', "combo at %s -> %s" % (i, candidates[i]))
                # Check prev. Sorted, can't reuse same number so cont
                if i > idx and candidates[i] == candidates[i-1]:
                    continue
                # Continue search
                dfs(i+1, path+[candidates[i]], cur+candidates[i], level+1)
            print()
        dfs(0, [], 0)
        return res
```

### Path through Matrix - Python Incomplete
```python
class Solution:
    def hasPath(self, maze: List[List[int]], start: List[int], destination: List[int]) -> bool:
        '''
        Ex1: [[0,0,1,0,0],[0,0,0,0,0],[0,0,0,1,0],[1,1,0,1,1],[0,0,0,0,0]], start = [0,4], destination = [4,4]
             --> True
        Ex2: [[0,1][0,0]], start = [0,1], dest = [1,0] -> True
            | __ | S  |
            | G  | __ |
        Ex3: [[0,0,1][0,0,0]][0,0,0], start = [0,2], dest = [1,0] -> False

        Analysis:
        - Start with goal. Only valid tries are opposite walls or previous direction
        - DFS from goal, backtracking?


        '''

        def printMaze(matrix: List[List[int]], markers: dict, trueMark = 'X'):
            
            print("   ", end="")
            for j, v in enumerate(matrix[0]):
                print("|" + str(j).center(5, '_'), end="")
            print()
            for i, row in enumerate(matrix):
                print(str(i).center(3), end="")
                for j, col in enumerate(matrix[i]):
                    found = None
                    for marker, point in markers.items():
                        if point[0] == i and point[1] == j:
                            found = marker
                            break
                    if found:
                        print("|" + str(found).center(5), end="")
                    elif matrix[i][j]:
                        print("|" + str(trueMark).center(5), end="")
                    else:
                        print("| ___ ", end="")
                print("|")
            print()

        # def getBoundaries(cells):
        #     def getBoundary(ball, cell):
        #         if  cell == 0:
        #             return -1
        #     retList = []
        #     for cell in cells:
        #         if maze[cell[0]][cell[1]] == 1:
        #             retList.append()

 
        def getAdjacentCells(ball, dir) -> List:
            row = ball[0]
            col = ball[1]
            retAds = [(max(row-1, 0), col),
                        (min(row+1, len(maze)-1), col),
                        (row, max(col-1, 0)),
                        (row, min(col+1, len(maze[0])-1))]
            # print(ball, [cell for cell in retAds if not (cell[0] == ball[0] and cell[1] == ball[1]) ])
            return [cell for cell in retAds if cell != ball ]

        def getValidMoves(ball, dir):
            '''
            We can only move in the previous direction, or opposite a wall?
            '''
            adjacents = getAdjacentCells(ball, dir)
            return adjacents

        def tryPath(ball, target, dir, visited=[], level=0):
            print(level, ":", level * '\t', "try", ball, target, "d:", dir)
            # base - found
            if ball[0] == target[0] and ball[1] == target[1]:
                return True

            # hit wall
            if maze[ball[0]][ball[1]] == 1:
                # print(".  ", level * '\t', "wall - unwind", ball)
                return False

            visited.append(ball)

            moves = getValidMoves(ball, dir)
            if not moves or not len(moves):
                return False

            dir_cell = None
            if dir != None:
                dir_cell = tuple(map(operator.add, ball, dir))
                print(".  ", level * '\t', "continue?", dir_cell, moves, "d:", dir)
                printMaze(maze, {'<B>': ball, 'e': destination})
                # can continue in dir
                if dir_cell in moves:
                    if tryPath(target, dir_cell, dir, visited, level+1):
                        # print(".  ", level * '\t', "unwind", ball)
                        return True

            # print("Change", level * '\t', ball, "from", moves)
            for try_cell in [c for c in moves if c != dir_cell and c not in visited]:

                new_dir = tuple(map(operator.sub, try_cell, ball))

                if tryPath(target, try_cell, new_dir, visited, level+1):
                    # print(".  ", level * '\t', "unwind", ball)
                    return True
            # print(level * '\t', "Dead end")
            return False

        printMaze(maze, {'s': destination, 'e': start})

        return tryPath(destination, start, None)
        


        
        


        

```