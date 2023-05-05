[[Binary Search Template Python]]

1. Start with binary search
2. Tweak base case, when we are done
3. Tweak left, right evals and searches

#### Ex: Search folded array
	https://www.educative.io/courses/grokking-coding-interview-patterns-python/g7nR0Jo8gRr

### Ex: First Bad Version #
```python
from api import *

version_api = api(0)

def is_bad_version(v):
    return version_api.is_bad(v)

def first_bad_version(n):
    '''
    Find the first bad version in an array

    E.g.:
    | g | g | g | g | b | b | b|
      '           *           '    -> mid + 1 .. last
                 '    *   '        <- first .. mid
                 '*   '            -> mid + 1 .. last
                     '*'           mid == last

    - n versions with the IDs [1, 2, ..., n], n if first high
    - How do we know when we are done?
      - Finding a Bad num just means that first bad is <= num
      - Have to search left including mid until mid == last (left searches exhausted)
    - How do we set up next search?
      - n not bad, search mid+1 .. last
    '''
# -- DO NOT CHANGE THIS SECTION
    version_api.n = n
# -- 
    versions = range(1, n+1)
    return binary_search_low(versions, 0, len(versions)-1, 0, comp)

def comp(num):
    return is_bad_version(num)
 
def binary_search_low(nums, last_good, high, count, compare):

    if last_good > high:
        return 0, 0

     # Finding the mid using floor division
    mid = last_good + (high - last_good) // 2 # Rounded down

    is_bad = compare(nums[mid])
    print("search: %s \t| %s \t| %s \t (%s)" % (last_good, mid, high, count+1))
    print("Version @ %s == %s is Bad %s" % (mid, nums[mid], is_bad))
    # Bad @ mid, mid is a candidate if nothing to left
    if is_bad:
        if mid == high: # this is what happens when searching right ends
            return nums[mid], count
        else:
            print("\t<---")
            return binary_search_low(nums, last_good, mid, count+1, compare)

    # Target is good, search mid+1 to high
    else:
        print("\t--->")
        return binary_search_low(nums, mid+1, high, count+1, compare)

```

