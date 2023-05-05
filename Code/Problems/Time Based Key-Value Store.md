Time Based Key-Value Store

```python
from collections import OrderedDict

class TimeMap:
  '''
  Implement a time-series key-value store.
  
  EG:  
    [["foo", "bar", 1]]:                            get("foo", 1) --> bar;  get("foo", 3) --> bar
    [["foo", "bar", 1], ["foo", "bar2", 4]]:        get("foo", 4) --> bar2
    
    Analysis:
    
    BF:  Keep a nested/2D structure.  Indexed by key, sorted by timestamp.  O(n), but Omega more like Om(t/k)
      - Space is O(k*t) (timestamps are duplicated)
    
    - Index the timestamps too?
    
    - timestamps hashed and ordered?  Removes redundancy of data.
      ts -> hash-map of keys
            metadata?  could keep min and max key hashes, bloom filter
      
      
    
  
  '''

  def __init__(self):
    self.timeseries = OrderedDict()


  def set(self, key: str, value: str, timestamp: int) -> None:
    if timestamp not in self.timeseries:
      self.timeseries[timestamp] = {}
    time_obs = self.timeseries[timestamp]
    if key not in time_obs:
        time_obs[key] = value
    # print("set", key, value, timestamp)
    # print(timestamp, time_obs)


  def get(self, key: str, timestamp: int) -> str:
    '''
    Get the most recent value for key, on or before the timestamp
    Returns a value such that set was called previously, with timestamp_prev <= timestamp. 
    If there are multiple such values, it returns the value associated with the largest timestamp_prev.
    '''
    # get timestamp-observations from time-series
    for ts in (filter(lambda t: t <= timestamp, reversed(self.timeseries))):
      time_obs = self.timeseries.get(ts)
      # print("get", key, timestamp)
      # print(timestamp, time_obs)
      if key in time_obs:
        return time_obs[key]

    return ""

    

# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```