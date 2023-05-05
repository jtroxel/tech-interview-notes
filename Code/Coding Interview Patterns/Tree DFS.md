**Tricks**
[[Coding Interview Patterns Index]]<ins>Recursive</ins> solution:  Use parent param as stack var, copy with `list()`

All logic at Node-level.  Check for <ins>None</ins>, then <ins>Base case</ins> (match logic)

Then recurse `left, right`.  Use <ins>results passed down</ins>, so no return vals.

```python
class TreeNode:
  def __init__(self, val, left=None, right=None):
    self.val = val
    self.left = left
    self.right = right

  def __str__(self):
    return "(%s: [%s, %s])" % (str(self.val),
      str(self.left.val) if self.left else "-",
      str(self.right.val) if self.right else "-")


def find_paths(root, required_sum):
  allPaths = []
  find_paths_recursive(root, required_sum, [], allPaths)
  return allPaths

def find_paths_recursive(currentNode, requiredSum, currentPath, allPaths):
  if currentNode is None:
    return None

  # add the current node to the path
  currentPath.append(currentNode.val)
  #Base: if all parents + node == sum, return if at leaf
  if sum(currentPath) == requiredSum and currentNode.left == None and currentNode.right == None:
    allPaths.append(list(currentPath))
    return

  # Continue left, right
  find_paths_recursive(currentNode.left, requiredSum, list(currentPath), allPaths)
  find_paths_recursive(currentNode.right, requiredSum, list(currentPath), allPaths)
```