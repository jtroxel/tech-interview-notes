## My First Try, BF

```Java
/*
Count Smaller To Right

counts[i] = count of smaller nums to right in array
return the sum of counts


E.g: nums =     [3, 8, 4, 1] --> 4
     counts =   [1, 2, 1, 0]
     
Analysis
- Have to see all, we have to know 
- BF:  O(n**2). Nested loop, compare each with each to right. O(N * log(N))?

- Use a Sorted List
    - Sort is O(N log N)
    - Then we can access by num and get count of remaining
    
- Can we use two pointers?  Keep some sort of min/max
    

*/

long solution(int[] nums) {
    
    int arrLen = nums.length;
    int[] counts = new int[arrLen];
    
    for (int i = 0; i < arrLen; i++) {
        int iCount = 0;
        for (int j = i+1; j < arrLen; j ++) {
            if (nums[j] < nums[i]) {
                iCount++;
            }
            //System.out.printf("%d v %d - %d ...", nums[i], nums[j], iCount);
            //System.out.printf("\ni: %d, j: %d, count right = %d\n", i, j, iCount);
        }
        counts[i] = iCount;
    }
    //System.out.println(Arrays.toString(counts));
    int retSum = 0;
    for (int count : counts) {
        retSum += count;
    }
    
    return retSum;

}
```