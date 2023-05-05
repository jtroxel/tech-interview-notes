Python - Merging 2 Sorted Lists

```python
def merge_lists(lst1, lst2):
    result = []
    print(lst1,lst2,result)
    # Zip up while both lists non-empty
    while lst1 and lst2:
        next_e = lst1.pop(0) if lst1[0] < lst2[0] else lst2.pop(0)
        result.append(next_e)
        print(lst1,lst2,result)
    # Add on any remaining (at least 1 should be empty)
    result = result + lst1 + lst2
    print(lst1,lst2,result)
    return result
```