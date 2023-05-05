Hit Counter - Python

```python
class HitCounter:
    HIT_WINDOW = 300

    def __init__(self):
      self.hits = {}
        

    def hit(self, timestamp: int) -> None:
      if timestamp in self.hits:
        self.hits[timestamp] += 1;
        return
      self.hits[timestamp] = 1
      
        

    def getHits(self, timestamp: int) -> int:
      return sum(self.hits[t] for t in self.hits.keys() if timestamp-t < self.HIT_WINDOW)
```