```Python
from typing import List
import unittest

NO_DUPE_RAINBOW = "red,orange,yellow,blue,green,purple"
LONG_RAINBOW = "red,orange,yellow,blue,green,indigo,violet"

def asserListsEqualUnordered(l1: List, l2: List):
    assert (all(elem in l1  for elem in l2)) and (all(elem in l2  for elem in l1))
    pass
    
def dedupe(dupList: List):
    return list(set(dupList))

def dedupeListComp(dupList: List):
    res = []
    [res.append(x) for x in dupList if x not in res]
    return res

test_list = list(NO_DUPE_RAINBOW.split(','))
result = dedupe(test_list)
print(*test_list)
print(*result)
asserListsEqualUnordered(result, test_list)
result = dedupeListComp(test_list)
assert (result == list(test_list))
```