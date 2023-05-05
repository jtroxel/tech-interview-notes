## Matrix - List\[List\]

```python
def printMatrix(matrix):
    print("----- " + ".".join(("%3s" % c) for c in range(len(matrix[0]))))
    for row, cells in enumerate(matrix):
        rowStr = "%3s: |" % row
        for cell in cells:
            rowStr += "%3s|" % cell
        print(rowStr)
```

## Dict
```python
  public void prettyPrintMap(Map<Integer, Integer> map, String label, int limit) {
        StringBuilder ln1 = new StringBuilder();
        StringBuilder ln2 = new StringBuilder();
        ln1.append(String.format("%5s:\t", label));
        ln2.append(String.format("%5s:\t", " --> :"));
        map.forEach((k,v)->{
            ln1.append(String.format("|%5d", k));
            ln2.append(String.format("|%5d", v));
          });
        ln1.append("|\n");
        ln2.append("|\n");
        System.out.println(ln1.append(ln2));

```
## Binary Tree

```python
class Solution:
    def printTree(self, root: Optional[TreeNode]) -> List[List[str]]:
        tree = BinarySearchTree(root, None)
        lst = tree.printList()
        tree.print()
        return lst

class BinarySearchTree:

    def __init__(self, root: TreeNode, cur = None):
        self.root = root
        self.current = cur

    def depth(self, root, h = 0):
        if not root: return h
        return max(self.depth(root.left, h+1), self.depth(root.right, h+1))

    def printList(self, cur: Optional[TreeNode] = None):
        if not self.root: return [""]
        if cur: self.current = cur

        d = self.depth(self.root)
        self.res = [[""] * (2**d - 1) for _ in range(d)]

        def helper(node, d, pos):
            self.res[-d - 1][pos] = str(node.val)
            if node.left: helper(node.left, d - 1, pos - 2**(d - 1))
            if node.right: helper(node.right, d - 1, pos + 2**(d - 1))

        helper(self.root, d - 1, 2**(d - 1) - 1)
        return self.res

    def print(self, padding = 3):
        matrix = self.printList()
        for row in matrix:
            nodes = []
            for j, col in enumerate(row):
                if len(col):
                    nodes.append(j)
                    print(str(col).center(padding), end="")
                else:
                    print(" " * padding, end="")
            print()

            for j, col in enumerate(row):
                if j in nodes:
                    print("/".ljust(padding-1) + "\\".rjust(padding-2), end="")
                else:
                    print(" " * padding, end="")
            print()
```

