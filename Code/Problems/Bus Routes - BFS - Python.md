Bus Routes - BFS - Python
**TRICK:  BFS, Searching busses at stops.  Search bus_shchedule for each stop_busses[cur] for the target, then recurse down **
```python
NOT_FOUND = -1

class Solution:
  '''
  Bus Routes
    Minimum buses to connect source and target
  
  - seq is cylical (loop)
  - 
  
  
  
  EG:
    routes = [[1,2,7],[3,6,7]], source = 1, target = 6
    --> 2 (1->7->6)
    
    1->2-\
    |<----7
    3->6-/
    
  Analysis
    BF:  Nested loops, compare each stop in each list with other lists?  Still have to build a graph or something to 
          track the links between buses
    DIY:  Looked for common element
      - Treat the *busses* as nodes, with a set of stops.  Then common stops create an edge
      - BFS for shortest path?
      - starting with source, check all the busses
                    
      
      stopsBFS(stop):
        for busses in stop_busses
          checkBus:
            - if bus has target, then done
          for stops in stop
            - stopsBFS()
  '''
  
  def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
    '''
      bus_schedules {0: {1, 2, 7}, 1: {3, 6, 7}}
      stop_busses {1: {0}, 2: {0}, 7: {0, 1}, 3: {1}, 6: {1}}
                       ^                          get busses at stop (source)
      bus_schedules {0: {1, 2, 7}, 1: {3, 6, 7}}
                    ^                             check stops for bus
                        X, X, X
                                now call bfs for each stop for the bus
                          ...   for each
    
    '''
    if source == target: return 0
    self.bus_schedules: dict[set] = {} # busses mapping to the stops they make
    self.stop_busses = {} # bus stops mapped to the list of busses that stop
    visited: set = set()
    for bus, stops in enumerate(routes):
      self.bus_schedules[bus] = stops
      for stop in stops:
        if not stop in self.stop_busses:
          self.stop_busses[stop] = set()
        self.stop_busses[stop].add(bus)

    print("bus_schedules", self.bus_schedules)
    print("stops Busses", self.stop_busses)
    
    count = self.stopsBFS(source, target, visited)
    
    return count
    
  def stopsBFS(self, stop, target, visited: set):
    # print("stopBFS", stop, "->", target, ":", visited)
    # 1 check all stops for busses servicing stop (BF)    
    # for busses at stop     
    for bus in self.stop_busses[stop]:
      # check bus's schedule for target
      if bus in visited: continue
      if target in self.bus_schedules[bus]:
        # print("-->found connection", stop, target, bus, self.bus_schedules[bus])
        return 1
    # 2 Now check next level
    min_next = NOT_FOUND
    # next_
    for bus in self.stop_busses[stop]:
      # try connecting from the bus's stops to target
      if bus in visited: continue
      # print("checking Bus", bus, self.bus_schedules[bus], visited)
      visited.add(bus)
      for next_stop in self.bus_schedules[bus]:
        # print("next_stop", next_stop)
        if next_stop == stop: continue
        next_leg = self.stopsBFS(next_stop, target, visited)
        if (next_leg != NOT_FOUND):
          if (min_next != NOT_FOUND):
            min_next = min(min_next, 1  + next_leg)
          else:
            min_next = 1  + next_leg

          # print("Next Count", next_leg, "min_next", min_next)
      
    return min_next
```