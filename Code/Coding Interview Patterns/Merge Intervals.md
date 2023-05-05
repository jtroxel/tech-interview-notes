**Trick:** 
- Sort on start
- then iterate and merge when `b.start <= a.end`

**Code**
```python
def merge(intervals: list[list]):

def merge(self, intervals: List[List[int]]) -> List[List[int]]:
	if len(intervals) <= 1: # Nothing left to merge
		return intervals

	intervals = sorted(intervals) # Sort O(n log n), then just 1 pass
	# print(intervals)
	last = None
	for i, nxt_iv in enumerate(intervals):
		print(i, last, nxt_iv)
		# If overlap, merge nxt with last and pop it out
		if last and last[1] >= nxt_iv[0]:
			last[1] = nxt_iv[1]
			intervals.pop(i)
		print(last, nxt_iv, intervals)
		last = nxt_iv

```