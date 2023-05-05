Binary Tree Iterator
\*\*TRICK: \*\*

- Use Stack for parents
- Keep current pointer in instance
- next/hasNext recognize first call
- don't mutate cur or parents to check hasNext
    **Algo**
- hasNext: if cur not set OR cur.right OR no parents
- next: if right, tree_first cur.right. elif parents pop

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

'''
Binary Search Tree Iterator - In Order Successor
  - Keep pointer to current node
  - No parent in TreeNode

EG: 
  [[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []] -> [null, 3, 7, true, 9, true, 15, true, 20, false]
  BF, pre-order tree def            iterations of next()                   values returned from visit
  
Analysis
  - Need stack for parents (use call stack?)
  - On instantiation go to first (leftmost)
    - subtree_first
  
  - Traversal, at each node:
    - if node.right: subtree_first
    - else: walk up until child is left (parent.left = child(ret value?))
    - traverse right
  
'''
class BSTIterator:

    def __init__(self, root: Optional[TreeNode]):
      #print(root)
      self.root = root
      self.parents = []
      self.width = 0
      
      self.cur: Optional[TreeNode] = None
      self.printTree(self.root)

    def next(self) -> int:
      # print("next...")
			# First call, get leftmost child
      if not self.cur:
        self.cur = self.tree_first(self.root)
			 # Or find next 
      else:
        self.cur = self.tree_next(self.cur)
      
      self.print_cur()
      return self.cur.val if self.cur else -1
      
        
    def hasNext(self) -> bool:
      '''
      - if no cur (first time)
      - OR possible next:
        - node right
        - OR parents
      '''
      # print("hasNext...")
      self.print_cur()
      return (not self.cur
              or self.cur.right
              or self.parents)
    
    def tree_next(self, node: Optional[TreeNode]):
      '''
      go to:
      - tree_first left if cur not set
      - tree_first right if exists
      - else tree_parent if exist
      '''
      # print("tree_next...")
			# If we have a right, get leftmost of right
      if (node and node.right):
        # print("\\ to ", node.right.val)
        return self.tree_first(node.right)
			# No right, pop off of parents
      else:
        return self.tree_parent(node)
      return None
    
    def tree_first(self, start: Optional[TreeNode]) -> TreeNode:
      '''
      Go to left-most child
      '''
      node = start
      while (node.left):
        self.parents.append(node)
        node = node.left
      # print("/ to ", node.val)
      self.printParents()
      return node
    
    def tree_parent(self, node: Optional[TreeNode]) -> TreeNode:
      # while (node and self.parents):
      #   parent = self.parents.pop()
      #   print("^ to ", parent.val)
      #   if (parent.left == node):
      #     return parent
      #   else:
      #     node = parent
      # #     print("   ...", node)
      # # print("    ^ [", ' > '.join(str(p.val) for p in self.parents), "]")
      # return node
      if (not self.parents):
        return None
      ret = self.parents.pop() 
      # print("^ to ", ret.val if ret else ret)
      return ret
             
    def printParents(self):
      return
      print("    ^^[", ' > '.join(str(p.val) for p in self.parents), "]")
      
    def print_cur(self):
      return
      curVal = self.cur.val if self.cur else None
      print("--->", curVal)
      
    def printTree(self, root):
      return
      matrix = self.treeAsMatrix(root)
      print("---- TREE:")
      for row in matrix:
        for cell in row:
          print("%2s" % cell if cell else " ", end =" ")
        print("")
      print("-------------- ->", self.cur.val if self.cur else "None")
      
      
    def treeAsMatrix(self, root):
      """
      :type root: TreeNode
      :rtype: List[List[str]]
      """
      def get_height(node):
          return 0 if not node else 1 + max(get_height(node.left), get_height(node.right))

      def update_output(node, row, left, right):
          if not node:
              return
          mid = int((left + right) / 2)
          self.output[row][mid] = str(node.val)
          if self.cur and self.output[row][mid] == self.cur:
            self.output[row][mid] += "*" 
          update_output(node.left, row + 1 , left, mid - 1)
          update_output(node.right, row + 1 , mid + 1, right)

      height = get_height(root)
      width = 2 ** height - 1
      self.output = [[''] * width for i in range(height)]
      update_output(node=root, row=0, left=0, right=width - 1)
      return self.output

# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()
```