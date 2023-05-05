#code-interview #temporal #matrix-traversal #dfs ?

```java
/*
 * Click `Run` to execute the snippet below!
 */

import java.io.*;
import java.util.*;

/*
 * Conway’s Game of Life

Imagine we have an n x n grid (n>=4) with each cell containing an organism. At any stage a cell can be alive or dead. The cell’s lifecycle is determined by its state (alive or dead) in the previous stage.

Example of a starting grid (T=0):

0 0 0 0
0 1 1 0
0 0 0 0
0 0 1 0

Where 0 and 1 represent dead and live organisms, respectively.

Rules for Subsequent stages:

* Any live cell with fewer than two live neighbours dies, as if caused by underpopulation.
* Any live cell with two or three live neighbours lives on to the next generation.
* Any live cell with more than three live neighbours dies, as if by overpopulation.
* Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

Every cell interacts with its eight neighbours, which are the cells that are horizontally, vertically, or diagonally adjacent.

Example of subsequent grid stages:

T=1

0 0 0 0
0 0 0 0
0 1 1 0
0 0 0 0
T=2

0 0 0 0
0 0 0 0
0 0 0 0
0 0 0 0

Problem statement
* Implement a simulation of the Conway's Game of Life, where the only inputs are the initial board, and a maximum number of stages.

* At each stage, print the current board.

* Stop the simulation as soon as the maximum number of stages is reached.

(T=0)
0 0 0 0
0 1 1 0
0 0 0 0
0 0 1 0

Analysis
  BF: iterate through all the cells, and run through the rules
*/

class Solution {
  public static void main(String[] args) {
    // Set up EX1:
    Board board1 = new Board().size(4)
      .with(
            0, 0, 0, 0,
            0, 1, 1, 0,
            0, 0, 0, 0,
            0, 0, 1, 0);

    board1.boardCells.forEach(v -> System.out.printf("%d | ", v));

    List<Integer> result1 = board1.play(2);
    System.out.println("Result: ");
    result1.forEach(v -> System.out.printf("%d | ", v));

    List<Integer> expected = new ArrayList<>();
    expected.addAll(Arrays.asList(
                    0, 0, 0, 0,
                    0, 0, 0, 0,
                    0, 0, 0, 0,
                    0, 0, 0, 0));

    System.out.println("");
    System.out.println("Expected: ");
    expected.forEach(v -> System.out.printf("%d | ", v));

    assert (result1.equals(expected));

  }
}
class Board {
  int size;
  //. Idx ->  Row, Idx -> Cell
  List<Integer> boardCells;

  public Board() {};

/**
  fluent size setter
 */
  public Board size(Integer boardSize) {
    this.size = boardSize;
    return this;
  }

  public Board with(Integer... cells) {
    this.boardCells = Arrays.asList(cells);
    return this;
  }

  public List<Integer> play(int maxCycles) {
    List<Integer> retCellList = null;
    int listSize = this.size*this.size;
    //iterate until maxCycles
    for (int c = 1; c <= maxCycles; c++) {
      retCellList = new ArrayList<>(listSize);
      // get. a new board
      for (int cIdx = 1; cIdx <= (listSize); cIdx++) {
        retCellList.add(cIdx-1, applyRules(cIdx));
      }
    //  System.out.println("");
    //   retCellList.forEach(v -> System.out.printf("%d | ", v));

    }
    this.boardCells = retCellList;
    return retCellList;
  }
  /* 
  * Any live cell with fewer than two live neighbours dies, as if caused by underpopulation.
* Any live cell with two or three live neighbours lives on to the next generation.
* Any live cell with more than three live neighbours dies, as if by overpopulation.
* Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.


  */
  public int applyRules(int cellIdx) {
     int count = countNeighbors(cellIdx);
     boolean liveCell = (this.boardCells.get(cellIdx-1) == 1);

     if (liveCell) {
      if (count > 2 && count < 3) {
        // flip live
        return 1;
      } 
     } else {
       if (count == 3) return 1;
     }
    return 0;
  }

  private int countNeighbors(int cellIdx) {
      int count = 0;
    int myRow = rowByIdx(cellIdx);
    int myCol = colByIdx(cellIdx);
    for (int cr = -1; cr <= 1; cr ++) {
      for (int cc = -1; cc <= 1; cc ++) {
        // TODO extract method to make readable
        if (cr == 0 && cc == 0) continue; // don't count ourselves
        int checkR = myRow + cr;
        int checkC = myCol + cc;
        if (checkR < 0 || checkR >= this.size) continue;  // don't check off edge
        if (checkC < 0 || checkC >= this.size) continue;  // don't check off edge
        count += this.boardCells.get(listIdxBy(checkR, checkC));
      }
    }
    return count;
  }

  int listIdxBy(int row, int col) {
    return row*col;
  }
  int rowByIdx(int cIdx) {
    return cIdx/this.size;
  }
  int colByIdx(int cIdx) {
    return cIdx % this.size;
  }


}
```

Problem - Impl Conway's Game of Life
``