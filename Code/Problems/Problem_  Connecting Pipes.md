An example of a "Greedy Algorithm."  The set of locally optimal connections gives the optimal solution.

```
/*
  Problem: Connect pipes

     Given n pipes of different lengths, implement a function that connects these pipes into one pipe. The cost to connect two pipes is equal to the sum of their lengths. We need to connect the pipes with minimum cost.

    - Each connection adds the cost of the connection, previous length + pipe

    The input is an int array where its length is equal to the number of pipes available and its indices are the specific lengths of the pipes.

  Analysis

  - Each combo of pipes is a potential connection.  n**2 combos
  - Nested loops is O(n**2)
  - Sort first, binary, O(n*log(n)), plus...
  - Then, connect from shortest to longest?

  E.g.: {4, 2, 3, 7} -> 30 // Length of each pipe, 4 pipes
        {2, 3, 4, 7}    Sum
         2+3 = 5       5
         5+4 = 9        14
         7+9 = 16       30
  E.p.:

 */

import static org.junit.Assert.assertEquals;

import java.io.*;
import java.util.*;

class Solution {

  public static void sort(int[] arr) {
    Arrays.sort(arr);
  }
  public static int connectionCost(int pipe1, int pipe2) {
    return pipe1 + pipe2;
  }
  public static int minCost(int[] pipes) {
    int cost = 0;

    // Using sorted pipes, add connections from shortest to longest
    for (int i = 1; i < pipes.length; i++) {
      sort(pipes);
      int lastJoint = pipes[i-1];
      int newJoint = connectionCost(lastJoint, pipes[i]);

      System.out.println("Connecting " + lastJoint + " to " + pipes[i] + " for "

          + (cost + newJoint));
      pipes[i-1] = newJoint;
      cost += newJoint;
    }
    System.out.println("Total cost for connecting pipes is " + cost);
    return cost;
}

  public static void main(String[] args) {
  int[] pipes = {4, 3, 2, 7 };
  assertEquals(30, minCost(pipes));
  int[] pipes1 = {1, 1, 2, 6};
  assertEquals(36, minCost(pipes1));
  int[] pipes3 = {1, 1, 2, 2, 4, 5}; // = 2
              //     2: 2, 2, 4, 5. = 6
              //        4: 2, 4, 5. = 12. or 2, 3, 4, 5 = 9
              //           6: 4, 5. = 22. or    4, 5, 5 = 18
              //              10, 5  = 37 or       5, 9 = 36

  assertEquals(12, minCost(pipes3));
  }
}
```