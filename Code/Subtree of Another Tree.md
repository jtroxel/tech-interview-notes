#code-interview #dfs #tree-compare #recursive
```python
from binary_tree_node import BinaryTreeNode
from binary_tree import BinaryTree


def subtree(root, sub_root):
    '''
    EX (trivial): [100], [100] -> True
    EX: [1,2,3,4,5,6,7], [3,6,7] -> True

    - Empty/null Tree (either)? -> False
    - Time/space complexity? O(N) time

    Analysis
    - BST.  Heve to get to leaves, sounds like DFS
    - DFS for sub-root in tree-root
        - OR find during build
    - Traverse subtree, preorder:
        - Compare node-val
        - Compare left and compare right
    '''

    tree_find = BinaryTree()
    sub_root_root = tree_find.find_in_bst_rec(root, sub_root.data)
    if not sub_root_root:
        return False

    return compare_trees(sub_root, sub_root_root)

def compare_trees(sub_root, root):
    print("compare", sub_root, root)
    # base cases
    if not sub_root or not root or sub_root.data != root.data:
        return False
    print("compare subs", vars(sub_root), vars(root))
 
    return sub_root.left == root.left and sub_root.left == None \
        or compare_trees(sub_root.left, root.left) \
        and sub_root.right == root.right and sub_root.right == None \
        or compare_trees(sub_root.right, root.right)

```