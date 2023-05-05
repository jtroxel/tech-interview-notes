**Note:  this is a form of "Islands" question.**

```python
# Your previous Plain Text content is preserved below:

# We are given a two-dimensional board of size N x M (N rows and M columns).

# Each field can be one of the following:

# - empty: “.”
# - obstacle: “X”
# - player (only one): “A”
# - guard. There can be four types of guards:
#     - looking at the left: “<”
#     - looking at the right: “>”
#     - looking up: “^”
#     - looking down: “v”

# The guards can see everything in a straight line in the direction in which they are facing, as far as the first obstacle ('X' or any other guard) or the edge of the board

# Player can move from the current field to any other empty field with a shared edge but cannot move onto fields containing obstacles or guard.

# Write a function:

# `public isPassable(board: string[]): boolean;`

# that, given an array `board` consisting of N strings denoting rows of the array, returns `true` if is it possible for the player to sneak from their current location to the bottom-right cell of the board undetected, and `false` otherwise.
'''
Determine if the player can get from the starting  position to the lower right cell without contacting or being seen by a guard or obstacle
- N, M can fit into memory

EG:
    "A . . . ."
    ". . . X ."
    ". . . . <"
    ". . . . ." <--

    "A . . . ."
    ". . . . ."
    ". . X . <"
    ". . . . ." <--

Analysis
- BF - DFS
  - Iterate all cells.
    if guard, "draw line" until it hits something
  - Checking available neighbors
    Recursing down for valid ones
'''

def isPassable(board: list[str]) -> bool:
    # Preprocess
    player_square = None
    for row in board:
        for col in row:
            # If it's a guard, draw line
            if isGuard(row, col):
                drawLine(row, col):
                    pass
            if isPlayer(row, col):
                player_square = (row, col)
    # Start with players cell
    return checkAllNeighbors(player_square)
    # Visit all neighbors
        # Check if guard or line - Base case -> false
    
    def checkAllNeighbors(cell):
        for board[cell[0], cell[1]]:
            
        for dir in [N,S,E,W]:
        # check e
        if (
        # check s
        # check w
        # check n
```