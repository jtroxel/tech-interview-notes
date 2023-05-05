Given an array of integers, both -ve and +ve, find a contiguous subarray that sums to 0 (or some target).

What is the Algorithm?

* * *

### Solution Idea / Intuition

- Keep a Hash of PrefixSums -> index
- Traverse, if current *compliment* to a\[i\] is in hash, return subarray between

![image.png](../../../../_resources/image-7.png)

https://github.com/jtroxel/interview_code/blob/afef9ed3ffcdab53bbda9e2cbb4e2cc16bcc7fb1/jvm/src/main/java/icamp/PrefixSum.java