#code-interview #two-sum #sliding-window

Level: Easy

Given an array of integers, find a pair of integers that sums to a number Target.

**Trick:  Use A Map!  Map the diff to the current value as you go, while searching the map for current diff.**

> ***O(n)* as the whole array is iterated over once.  (Hash put/get both O(1))**

```Java
/*
 Problem Target Sum using Prefix Sums 

 EG: {1, 21, 3, 14, 5, 60, 7, 6}, 27 --> {21, 6} or {6, 21}

Analysis
 - We use a hash of diff vals to  

 */
class CheckSum
{   
  public static int[] findSum(int[] arr, int n) 
  {
    int[] result = new int[2];
    // write your code here
    Map<Integer, Integer> compliments = new HashMap<>();
    for (int cur : arr) {
      int diff = n - cur;
      if (compliments.containsKey(cur)) {
        result[0] = compliments.get(cur);
        result[1] = cur;
        return result;
      }
      compliments.put(diff, cur);

    }
    return result;   // return the elements in the array whose sum is equal to the value passed as parameter 
  }
}
```

```python
def find_sum(lst, k):
    diffs = {}
    for idx, cur in enumerate(lst):
        diff = k - cur
        print(cur, diff)
        if cur in diffs:
            return [diffs[cur], cur]
        diffs[diff] = cur
        print(diffs)
    return None
    pass
```

For e.g, if A = \[6,3,5,2,1,7\]. Target = 4, Result= \[3,1\]

Questions to Clarify:
Q. How do you want the output?
A. Return a pair of numbers.

Q. What if there are multiple pairs that sum to Target?
A. Return any pair.

Q. What to return if there are no pairs that sum to Target?
A. Return null.

* * *

January 12, 2022

- thought of new question, can items be summed to themselves.  let's say no

January 11, 2022
**Restate:**

Given an array of ints, and a Target sum, find any pair from the array that sum to the target, or null for no match

**Solution Notes--clues and concept(s):**

- Generally array traversal.  Ideally want to avoid n**2, nested loops.  Do we need to sort?
- Use a DS?  Hash values to ??
    - *Sparse hash of found numbers, compare  with T - array(idx)*
- ~~Matrix math?~~
- Brute force (n**2):  Traverse with 2 indexes
    - "outside" ix: skip numbers >= the target.
        - "inside" ix:  from ix , skip ix
            - test sum

\*\*Remember:  \*\*Verify if the array is sorted!  If so then we can use 2 pointers to adjust up and down against the target, moving toward the center.

![image.png](../../../../_resources/image-2.png)

```
    public static int[] targetSum(int[] inArray, int target) {
        if (inArray == null || inArray.length == 0) {
            return null;
        }
        return targetSumSection(inArray, target, 0, inArray.length - 1);
    }

    @Nullable

    private static int[] targetSumSection(int[] inArray, int target, int start, int end) {

        if (start == end) {
            return null;
        }
        int check = checkSum(inArray, start, end, target);
        if (check < 0) {
            return targetSumSection(inArray, target, start + 1, end);
        } else if (check > 0) {
            return targetSumSection(inArray, target, start, end - 1);
        }
        return new int[]{inArray[start], inArray[end]};
    }

    private static int checkSum(int[] inArray, int start, int end, int target) {

        return inArray[start] + inArray[end] - target;
    }
```

## Unsorted FindSum

Same situation, use quick or merge sort ant then binary search:

```Java
import java.util.Arrays;

import javax.xml.stream.events.EndDocument;

class Solution {

 public static int[] findSum(int[] arr, int n) //Returns 2 elements of arr that sum to the given value

 {
  Arrays.sort(arr); //Sort the array in Ascending Order (quick sort)

  System.out.print("Searching in: ");
  for (int i : arr) System.out.print(i + "|");

  int[] elements = new int[2];
  int foundIndex = 0, arrSize = arr.length;

  for (int i = 0; i < arrSize; i++) {
   //using binary search to find the index of the value that sums to n
   //after addition with the value at current index
   foundIndex = binarySearch(arr, arrSize, n - arr[i]);
   if (foundIndex != -1) {
    elements[0] = arr[i];
    elements[1] = arr[foundIndex];
   }
  }
  return elements;
 }

 static int binarySearch(int[] arr, int arrSize, int searchVal) {
    return binarySearchRecursive(arr, searchVal, 0, arrSize-1);
 }

 static int binarySearchRecursive(int[] arr, int searchVal, int start, int end) {

   int mid = start + ((end - start)/2);

  System.out.println("Searching |" + start + "|" + mid + "|" + end + "| mid val =  " + arr[mid]);

  if (mid == start || mid == end) return -1;
  if (arr[mid] == searchVal) return mid;
  if (searchVal < arr[mid]) {
      System.out.print("LEFT:");
    return binarySearchRecursive(arr, searchVal, start, mid-1);
  } else {
      System.out.print("RIGHT:");
    return binarySearchRecursive(arr, searchVal, mid+1, end);
  }
 }

 public static void main(String args[]) {
  int n = 9;
  int[] arr1 = {2, 4, 5, 7, 8};
   int[] arr2 = findSum(arr1, n);
  int num1 = arr2[0];
  int num2 = arr2[1];

  if ((num1 + num2) != n)
   System.out.println("Results not found!");
  else
   System.out.println("Sum of " + n + " found: " + num1 + " and " + num2);
 }
}
```