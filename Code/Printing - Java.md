#### Expected vs Actual, and Logging

System.out.printf("\\nActual: 3, Expected: %s", 2);

System.out.printf("\\nActual: 3, Expected: %s", Arrays.toString(new int\[\]{1,2,3}));

#### Print primitive array

```java
String[] myArray = new String[]{"Java", "Node", "Python", "Ruby"};

System.out.printf("\nActual: 3, Expected: %s", Arrays.toString(new int[]{1,2,3}));

Arrays.stream(myArray).forEach(System.out::println);
```

Print 2D array

```java
String[][] deepArrayStr = new String[][]{{"mkyong1", "mkyong2"}, {"mkyong3", "mkyong4"}};

Arrays.stream(deepArrayStr).flatMap(x -> Arrays.stream(x)).forEach(System.out::println);

System.out.println(Arrays.deepToString(my2DArray));

// Output : [[mkyong1, mkyong2], [mkyong3, mkyong4]

int[][] deepArrayInt = new int[][]{{1, 3, 5, 7, 9}, {2, 4, 6, 8, 10}};

Arrays.stream(deepArrayInt).flatMapToInt(x -> Arrays.stream(x)).forEach(System.out::println);

System.out.println(Arrays.deepToString(deepArrayInt));

// Output : [[1, 3, 5, 7, 9], [2, 4, 6, 8, 10]]
```

Print List or Set

```java
System.out.println(myList);

maxHeap.forEach(i -> System.out.printf("%5d|", i));
```

Print Map

```java
Arrays.toString(map.entrySet().toArray());

myMap.forEach((k,v)->System.out.println("Key : " + k + " Value: " + v));
```

#### Print Tree
from https://stackoverflow.com/a/46279667
```java
   public void printTree(TreeNode node) {
        int depth = 0;
        TreeNode cursor = node;
        while (cursor.left != null)  {
            depth += 1;
            cursor = cursor.left;
        }

        List<TreeNode> to_print = new ArrayList<>();
        to_print.add(node);
        // TODO:  This could all be a loop
        visitLevelOrder(node, to_print, depth * 2);
    }

    public void visitLevelOrder(TreeNode root, List<TreeNode> parents, int depth) {
        TreeNode n;
        List<TreeNode> children = new ArrayList<>();
        while (parents.size() > 0) {
            n = parents.get(0);
            if (n == null) continue;
            children.add(n.left);
            children.add(n.right);
            if (depth > 0) {
                System.out.print("\t".repeat(depth));
            }
            System.out.print(n.val);
            parents.remove(0);
        }
        System.out.println("_");
        if (!children.isEmpty()) {
            visitLevelOrder(root, children, depth-1);
        }
        System.out.println("-----------------------");
    }
```
