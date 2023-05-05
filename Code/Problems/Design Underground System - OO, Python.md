### Trick

**Keep 2 Maps:**

- **checkins = user_id -> (station, time)**
- **segments = startStation -> (endStation, time)**

**note: could have made class for segments**

```python
class UndergroundSystem:
  '''
  Track check In/Out times, by customer, between stations.  Calculate the average times for all customers, between 2 stations.
  
  EX:
  "checkIn":         [10,"Leyton",3]
  "checkOut"         [10,"Paradise",8]
  "getAverageTime"   ["Leyton","Paradise"] --> 5.0
  "checkIn"          [5,"Leyton",10]
  "checkOut"          [5,"Paradise",16]
  "getAverageTime"    ["Leyton","Paradise"] --> 5.0
  "checkIn"           [2,"Leyton",21]
  "checkOut"          [2,"Paradise",30]
  "getAverageTime"    ["Leyton","Paradise"] --> 6.66
  
  Analysis
  
  - Create a new station -> station -> time record (Segment)
  - First, need to track checkins by customer -> (station, time)
  - On checkOut, settle Segment by finding (most recent) checking for same customer
  - Add Segment to startStation -> endStation, time
  
  
  '''

  def __init__(self):
    self.checkins: dict[str, (str, float)] = {}
    self.segments: dict[str, list[(str, float)]] = {}


  def checkIn(self, id: int, stationName: str, t: int) -> None:
    self.checkins[id] = (stationName, t)


  def checkOut(self, id: int, stationName: str, t: int) -> None:
    ci_station, ci_time = self.checkins[id]
    if ci_station not in self.segments:
      self.segments[ci_station] = []
    self.segments[ci_station].append((stationName, (t - ci_time)))


  def getAverageTime(self, startStation: str, endStation: str) -> float:
    times = [t[1] for t in self.segments[startStation] if (t[0] == endStation)]
    print(times)
    
    return sum(times)/len(times)
        


# Your UndergroundSystem object will be instantiated and called as such:
# obj = UndergroundSystem()
# obj.checkIn(id,stationName,t)
# obj.checkOut(id,stationName,t)
# param_3 = obj.getAverageTime(startStation,endStation)
```