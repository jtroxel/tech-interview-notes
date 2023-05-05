K Projects with Max Profits (IPO)
#### Tricks:

**- Greedy, can always taks local_max**
**- Basically BFS, but only pursure next steps from the max.**
**- Return gets propogated back up.  Iterate might be better**

```python
class Solution:
  '''
  Maximize Capital for IPO
  
  Starting with w capital, pick the top k net_profit projects where
    - net_profit = (profite - capital)
    - project capital <= running_budget
      
  EG:   k = 2, w = 0, profits = [1,2,3], capital = [0,1,1] -> 4
  EG2:  k = 3, w = 0, profits = [1,2,3], capital = [0,1,2] -> 6
  
        k = 5, w = 4, profits = [5,7,9], capital = [3,4,6] -> 6
  
  Edge Cases?
   - Can't afford any?
   - Multiple projects with same net_profit?
   - Can k be > # valid projects?  I.e. can't get K
   
 Complexity?
    - Possibly 10**5 projects.  O(n) time
    

   
   
 Analysis
  - Order matters.  Hill-climbing?
  - Can we be greedy?  Yes, maximizing at each step maximizes amount left to spend
  - DFS - Try all affordable projects, then recurse
  - BF:  DFS
    dfs with running_budget, k
    dfs(running_budget, visited, k):
      - Base: k == 0
      - for all capitals <= running_budget and not visited
        - running_budget -= capital
        - net_profit = profit-capital + dfs(running_budget, visited, k-1)
    return max(net_profits)
  
  '''
  def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
    self.profits: List[int] = profits
    self.capitals: List[int] = capital

    visited: set[int] = set()
    print(w, k,)
    print("caps", self.capitals)
    print("profits", self.profits)
    return self.greedyMaxProfits(w, visited)
    
  
  def greedyMaxProfits(self, running_budget, visited):
    print("Search", visited, running_budget)
    # Base:  All selected
    if len(visited) >= len(self.capitals):
      print("done", visited)
      return running_budget
    
    # Greedy part:  get the local optimum across children like BFS
      # print("check", capital, i, max_i, net, local_max)
    local_max, max_i = self.getMaxNext(visited, running_budget)
    visited.add(max_i)
    print("Found", local_max, "at", max_i, visited, " = ", running_budget + local_max)
    return self.greedyMaxProfits(running_budget + local_max, visited)
  
  def getMaxNext(self, visited, running_budget):
    local_max = 0
    max_i = 0
    for i, capital in enumerate(self.capitals):
      if i in visited or capital > running_budget: continue
      net = self.profits[i] - capital
      if net > local_max:
        local_max = net
        max_i = i
        print("check", capital, self.profits[i] )
    return local_max, max_i
```