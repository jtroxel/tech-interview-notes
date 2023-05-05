#### Binary Trees and Binary Search Trees
- https://www.geeksforgeeks.org/difference-between-binary-tree-and-binary-search-tree/
	- Binary just means 0..2 children.  Not sorted or balanced.
	- Binary Search Tree is sorted so wrt each nodes:
		- left subtree only contains nodes < node
		- right only > node
#### Tree Traversal Notes
	[[Tree Traversal]]

#### Serialize/Deserialize a Binary Tree from Array
#level-order-traverse #binary-tree 
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from collections import deque
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str

        - in-order traversal
        """

        # base case
        if not root:
            return "null"
        # self.printTree(root)

        retArr = []
        def visit(val):
            retArr.append(val)

        self.verticalTraverse(root, visit)
            
        return ",".join(retArr)

    def verticalTraverse(self, root, visitor):
        queue = list()
        queue.append(root)
        while queue:
            node = queue.pop(0)
            if node:
                visitor(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            else:
                visitor('null')

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        node_list = data.split(",")
        # print(data, node_list)

        def addNode():
            value = node_list.pop(0)
            if value != 'null':
                return TreeNode(int(value))
            else: 
                return None

        
        parents = list() # list of parents
        # queue.append(addNode)
        root = addNode()
        parents.append(root)
        kids = list()
        while len(node_list):
            while len(parents):
                parent = parents.pop(0)
                if parent:
                    parent.left = addNode()
                    kids.append(parent.left)
                    parent.right = addNode()
                    kids.append(parent.right)
            parents = kids
            # self.printTree(root)

        return root


    def showTree(self, root: TreeNode) -> List[List[str]]:
            def get_depth(node):
                if not node: return 0
                return max(get_depth(node.left), get_depth(node.right)) + 1
            
            def insert_value(node, lo, hi, depth=0):
                if not node: return
                mid = (lo + hi) // 2
                output[depth][mid] = str(node.val).center(3)
                insert_value(node.left, lo, mid, depth + 1)
                insert_value(node.right, mid, hi, depth + 1)

            depth = get_depth(root)
            output = [["."] * (2**depth - 1) for _ in range(depth)]
            
            insert_value(root, 0, 2**depth - 1)
            return output
            
    def printTree(self, root):
        for li, level in enumerate(self.showTree(root)):
            print(li, ":", end="")
            for i in level:
                print(i.center(5) if i else (" " * 5), end="")
            print()


# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```