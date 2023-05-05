Next Higher Value with Stack - Python
**Trick: Iterate backward, keep a Stack of candidate "higher right values". As we progress back, pop all that are NOT greater. Stack means that the first found will be closest**

```python
from Stack import MyStack

def next_greater_element(lst):
    stack = MyStack()
    res = [-1] * len(lst)
    # Reverse iterate list
    for i in range(len(lst) - 1, -1, -1):
        print(lst, "@", i, "->", lst[i])
        print(stack.data(), res)
        ''' While stack has elements and current element is greater 
        than top element, pop all elements '''
        while not stack.is_empty() and stack.peek() <= lst[i]:
            print("popping all -", stack.peek(), "<=", lst[i])
            stack.pop()
        ''' If stack has an element, top element will be 
        greater than ith element '''
        if not stack.is_empty():
            print("copying", stack.peek())
            res[i] = stack.peek()
        # push in the current element in stack
        print("pushing", lst[i], "setting", res[i])
        stack.push(lst[i])
    for i in range(len(lst)):
        print(str(lst[i]) + " -- " + str(res[i]))
    return res

if __name__ == "__main__" :
    nge = next_greater_element([4, 6, 3, 2, 8, 1, 9, 9, 9])
```

\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 8 -> 9
\[\] \[-1, -1, -1, -1, -1, -1, -1, -1, -1\]
pushing 9 setting -1 --> Empty stack means nothing to right > lst-tail
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 7 -> 9
\[9\] \[-1, -1, -1, -1, -1, -1, -1, -1, -1\]
popping all - 9 &lt;= 9 --&gt; Pop off all lower items, 9==9 so pull it off (lst-tail is NOT greater)
pushing 9 setting -1 --> Now empty, push the lst-head. Nothing on the right >
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 6 -> 9
\[9\] \[-1, -1, -1, -1, -1, -1, -1, -1, -1\]
popping all - 9 <= 9
pushing 9 setting -1
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 5 -> 1
\[9\] \[-1, -1, -1, -1, -1, -1, -1, -1, -1\]
copying 9
pushing 1 setting 9
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 4 -> 8
\[9, 1\] \[-1, -1, -1, -1, -1, 9, -1, -1, -1\]
popping all - 1 <= 8
copying 9
pushing 8 setting 9
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 3 -> 2
\[9, 8\] \[-1, -1, -1, -1, 9, 9, -1, -1, -1\]
copying 8
pushing 2 setting 8
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 2 -> 3
\[9, 8, 2\] \[-1, -1, -1, 8, 9, 9, -1, -1, -1\]
popping all - 2 <= 3
copying 8
pushing 3 setting 8
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 1 -> 6
\[9, 8, 3\] \[-1, -1, 8, 8, 9, 9, -1, -1, -1\]
popping all - 3 <= 6
copying 8
pushing 6 setting 8
\[4, 6, 3, 2, 8, 1, 9, 9, 9\] @ 0 -> 4
\[9, 8, 6\] \[-1, 8, 8, 8, 9, 9, -1, -1, -1\]