April 14, 2022 - Got it mostly working, last thing I missed was returning null if there was NO successor, i.e. last element in tree.

https://www.educative.io/module/lesson/data-structures-in-java/gkWzZXlDvz9

![image.png](../../../../_resources/image-1.png)

In the table below, we can see the in-order successor for some of the nodes in this tree:

| **Node** | **In-order Successor** |
| --- | --- |
| 25  | 50  |
| 100 | 125 |
| 350 | NULL |

**Note:** The in-order successor of 350 is NULL since that’s the last node.

### Sample input[#](https://www.educative.io/module/lesson/data-structures-in-java/gkWzZXlDvz9#Sample-input)

The input list below represents the level-order traversal of the binary search tree, while the value that follows represents the node whose in-order successor we need to find:

`[100, 50, 200, 25, 75, 125, 350], 50    `

### Expected output[#](https://www.educative.io/module/lesson/data-structures-in-java/gkWzZXlDvz9#Expected-output)

`75`

## Try it yourself[#](https://www.educative.io/module/lesson/data-structures-in-java/gkWzZXlDvz9#Try-it-yourself)

```
// Importing required functions
import java.util.*;

class InorderSuccessor {
    private static BinaryTreeNode suc = null;
    private static BinaryTreeNode notFound = new BinaryTreeNode(-1);

    static BinaryTreeNode findInorderSuccessor(BinaryTreeNode root, int findVal) {

        if (root == null) {
            return suc;
        }
        System.out.println("Find " + findVal + " suc, check " + root.data);

        // If the current < the findVal, keep moving right
        if (findVal > root.data) {
            if (root.right == null) return notFound;
            return findInorderSucRight(root.right, findVal);
        // if current > the find value, it's a potential successor
        // ... and we search left
        } else if (findVal < root.data) {
            System.out.println("Set suc " + root.data);
            suc = root;
            if (root.left == null) return notFound;
            return findInorderSucLeft(root.left, findVal);
        // If equal, then find the lowest val off of right child
        } else {
            if (root.right != null) {
                root = root.right;
                while (root.left != null) {
                    root = root.left;
                }
                return root;
            } else {
                System.out.println("Return suc " + root.data);
                return suc;
            }
        }
    }

    static BinaryTreeNode findInorderSucLeft(BinaryTreeNode root, int findVal) {

        return findInorderSuccessor(root, findVal);
    }

    static BinaryTreeNode findInorderSucRight(BinaryTreeNode root, int findVal) {

        return findInorderSuccessor(root, findVal);
    }
}
```

![Snapshot.jpg](../../../../_resources/Snapshot.jpg)