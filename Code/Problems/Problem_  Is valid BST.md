Initial (naive):  in-order traversal, check that current node is less between left and right children

      - does NOT detect if subtree is valid compared to parents

```
/**
 * Definition for a binary tree node.
  * Solution notes:

  - Initial (naive):  in-order traversal, check that current node is less between left and right children
      - does NOT detect if subtree is valid compared to parents

 */
class Solution {
  public boolean isValidBST(TreeNode root) {

    // In-order traversal starting with root
    return ioTraverse(root);

    }

  public boolean ioTraverse(TreeNode root) {
    if (root == null) return true;
    if (!ioTraverse(root.left)) return false;
    System.out.print(root.val + "... ");
    if (root.left != null && root.left.val >= root.val
       || root.right != null && root.right.val <= root.val) {
      return false;
    }
    if (!ioTraverse(root.right)) return false;

    return true;
  }

}
```

2nd try:  left subtrees must be < root, right must be > root
accepted solution

```
class Solution {
  public boolean isValidBST(TreeNode root) {

    // In-order traversal starting with root
    return ioTraverse(root, Integer.MIN_VALUE, Integer.MAX_VALUE);

    }

  public boolean ioTraverse(TreeNode root, int minVal, int maxVal) {
    // Done with this subtree
    if (root == null) return true;
    System.out.print(root.val + " [" + minVal + "," + maxVal + "]... ");
    // Check that the subtree is in the range defined by ancestors
    if (root.val > maxVal || root.val < minVal) return false;
    if (root.left == null && root.right == null) return true;

    // Check left, max is root
    if (!ioTraverse(root.left, minVal, root.val-1)) return false;
    if (root.left != null && root.left.val >= root.val
       || root.right != null && root.right.val <= root.val) {
      return false;
    }
    // Check right, min is root val
    if (!ioTraverse(root.right, root.val+1, maxVal)) return false;

    return true;
  }

}
```