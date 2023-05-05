https://www.educative.io/module/lesson/dynamic-programming-patterns/3YyyqMYM59r
Recursive, top-down DP (save combos)

Remember:  Trick is *only track counts* along a tree of paths.  Memoization can be done by keeping a matrix of min costs for that combo, out to the leaf.  Again we don't have to know which choice, only how to increment.

micCost(s,t) =

- 0 if cells ==
- min of 1 +
    - minCost(each possibility for next letter)

Solution doesn't do DP:

```
/*
  Find the path with the lowest # changes...

  - for each combination of source-char and target char, a grid, calculate the min cost of swapping
  - the minimum path is

  - if source-char == target-char, calculate 0 + minPath of remaining chars of both

  - else, find the minimun of the paths with
  - removing source-char (source-char++)
  - swapping source-char and target-char (?)
  - inserting char before source-char
  f(b a t, b u t)
  b == b: f(a t -> u t)
  // f (a t, u t)
  a != u:
   Min of:
    f(t -> u t) // delete -
      t != u
        ...
    f(ut -> ut) // replace
    f(uat -> ut)  // insert
*/
class EditDistance {
  public int findMinOperations(String source, String target) {
    int[][] minDiff = new int[source.length()][target.length()];
    return findMinPath(source, 0, target, 0);
  }

  public int findMinPath(String source, int sourceI, String target, int targetI) {

    // End of target?
    if (targetI == target.length()) {
      return source.length() - sourceI; // distance is rest of source (delete)
    }
    // End of source?
    if (sourceI == source.length()) {
      return target.length() - targetI; // distance is rest of target (delete)
    }
    // chars are equal, calculate paths from next chars
    if (source.charAt(sourceI) == target.charAt(targetI))
      return findMinPath(source, sourceI + 1, target, targetI + 1);
    // Otherwise, try all 3
    return Math.min(
      1+ findMinPath(source, sourceI + 1, target, targetI + 1), // change == +1
      Math.min(

        1 + findMinPath(source, sourceI + 1, target, targetI), // skip one source ~like delete

        1 + findMinPath(source, sourceI, target, targetI + 1)) // skip next target, like insert

    );
  }
  public static void main(String[] args) {
    EditDistance editDisatnce = new EditDistance();
    System.out.println(editDisatnce.findMinOperations("bat", "but"));
    System.out.println(editDisatnce.findMinOperations("abdca", "cbda"));
    System.out.println(editDisatnce.findMinOperations("passpot", "ppsspqrt"));
  }
}
```

With DP

```
class EditDistance {
  public int findMinOperations(String s1, String s2) {
    Integer[][] dp = new Integer[s1.length()+1][s2.length()+1];
    return findMinOperationsRecursive(dp, s1, s2, 0, 0);
  }

  private int findMinOperationsRecursive(Integer[][] dp, String s1, String s2, int i1, int i2) {

    if(dp[i1][i2] == null) {

      // if we have reached the end of s1, then we have to insert all the remaining characters of s2

      if(i1 == s1.length())
        dp[i1][i2] = s2.length() - i2;

      // if we have reached the end of s2, then we have to delete all the remaining characters of s1

      else if(i2 == s2.length())
        dp[i1][i2] = s1.length() - i1;

      // If the strings have a matching character, we can recursively match for the remaining lengths

      else if(s1.charAt(i1) == s2.charAt(i2))
        dp[i1][i2] = findMinOperationsRecursive(dp, s1, s2, i1+1, i2+1);
      else {
        int c1 = findMinOperationsRecursive(dp, s1, s2, i1+1, i2); //delete
        int c2 = findMinOperationsRecursive(dp, s1, s2, i1, i2+1); //insert
        int c3 = findMinOperationsRecursive(dp, s1, s2, i1+1, i2+1); //replace
        dp[i1][i2] = 1 + Math.min(c1, Math.min(c2, c3));
      }
    }

    return dp[i1][i2];
  }
  public static void main(String[] args) {
    EditDistance editDisatnce = new EditDistance();
    System.out.println(editDisatnce.findMinOperations("bat", "but"));
    System.out.println(editDisatnce.findMinOperations("abdca", "cbda"));
    System.out.println(editDisatnce.findMinOperations("passport", "ppsspqrt"));
  }
}
```