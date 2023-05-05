List of Products of Other Elements - Python
```python
'''
- What if overflow integer, long?  Python2 handles, otherwise check product
    against sys.maxsize * 2 + 1, throw error
EG:  [1,2,3,4] -> [24,12,8,6]
      1,2,6,24
      24,12,
Analysis

BF: Do every combo, write to another list O(N**2) time, 2N space
- Rolling Product in new list
  - We know that each prod position is the prod of all left vals
  - We know that the last el is prod of all
  - All right vals are last-prod / cur-prod
  - So each pos is prod-left / cur-num * prod-all / prod-cur
  new val[i] = list end / val[i] * val[i-1]
  O(N)


'''
import sys
def find_product(lst):
    #print(sys.maxsize * 2 + 1) # if this is p2, we could throw error on this
    left_prods = []
    l_prod = 1 # prod of everything to left, shift 1
    for check in lst:
        # Add last left prod into prods
        left_prods.append(l_prod)
        # calc next-prod as current * last left prod
        l_prod = check * l_prod
    print(lst)
    print(left_prods)
    r_prod = 1 # prod of eveything to the right
    for r_pos in range(len(lst)-1, -1, -1):
        r_val = lst[r_pos]
        print(r_pos, r_prod, r_val, left_prods[r_pos])
        # Calculate prod of current r_val * l_prod, stuff in left_pods cuz done with it
        left_prods[r_pos] = r_prod * left_prods[r_pos]
        # multiply next right-prod with current lst
        r_prod *= r_val
        print(left_prods)
        print("[24, 12, 8, 6]")
    return left_prods
