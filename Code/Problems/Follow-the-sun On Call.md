Follow-the-sun On Call
#### Tricks
- Use mod with the number of engineers
- factored out formatting
- 
```python
"""


Secrets Management team uses a “follow the sun” on-call model where on-call work is divided between engineers in North America and India. Each region has a separate weekly round robin rotation for determining who is on-call each week (E.g. N1,N2,N3,N1,... and I1,I2,I3,I4,...). 

Write a function that takes the number of engineers in each region and a week number and outputs which two engineers are on-call that week

e.g. input
NA engineers: 3
India engineers: 4
Week number: 5

e.g. output
N2, I1


1  2  3  4  5
N1 N2 N3 N1

- assume 1 eng/region, week # >= 1
- week can keep going

Anlysis
- map from a week # to 
    - eng in NA
    - Eng in N
- map to weeks based on a rotation:  something % # eng/reg


"""

def engId(prefix: str, weekNum: int, engCount: int):
    format_str = prefix + "%s"
    print(weekNum, engCount, weekNum % engCount)
    mod = (weekNum % engCount)
    if (mod == 0): return str(prefix) + str(engCount)
    
    return format_str % (weekNum % engCount)


def oncallsForWeek(NEnCount: int, IEngCount: int, weekNum: int):
    n_eng = engId("N", weekNum, NEnCount)
    i_eng = engId("I", weekNum, IEngCount)
    return (n_eng, i_eng)


t0 = oncallsForWeek(3, 4, 5)
assert t0 == ('N2', 'I1'), str(t0)

t2 = oncallsForWeek(7, 4, 8)
assert t2 == ('N1', 'I4'), str(t2)
```