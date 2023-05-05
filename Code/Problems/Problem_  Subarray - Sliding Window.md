![image.png](../../../../_resources/image-4.png)
Problem:

Given an array of positive integers, find a subarray that sums to a given number X.

Prime Ex:  For e.g, input = \[1,2,3,5,2\] and X=8, Result = \[3,5\] (indexes 2,3)

Questions to Clarify:

Q. How to return the result?A. Return the start and end indices of the subarray.

Q. What to return if the array is empty or null?A. Return null.
Q. What to return if no subarray is found?A. Return null.
Q. What to do if there are multiple subarrays?A. Return any one.

**Main Idea is to keep a rolling sum, adjusting the window to right if < and left if <.**