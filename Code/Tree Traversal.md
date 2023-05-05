### General Tree Traversal Problems

#### Binary Search Tree (BST) Traversal
"Next" node = 
	`if right child:`
		`get left-most child from right`
	`else:`
		`get first ancestor just > current`
		
##### Get Node Successor - Java
(https://leetcode.com/problems/inorder-successor-in-bst-ii/description/)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
};

BST - Next Node
-   if node.right: get rightmost child, 
    else:
        get parent while parent.val < node.val
- Edge: At end?  rightmost edge of root.  How do we know?
    - parent.val < node.val and no parent.parent.val
*/
import java.util.ArrayList;
import java.util.List;

class Solution {
    public Node inorderSuccessor(Node node) {
        // If there is a right node, get left-most from right sub
        if(node.right != null) return getLeftMost(node.right);
        // Otherwise, get the first ancestor just > node
        else return getParentJustGT(node);
    }
    
    public Node getLeftMost(Node node){
        return node.left!=null? getLeftMost(node.left):node;
    }
    
    //Get Parent node just greater than the given node.
    public Node getParentJustGT(Node node){
        Node par = node.parent;
        while(par!=null && par.val<node.val) par = par.parent;
        return par;
    }
}
```