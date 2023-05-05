#code-interview #coding-interview #ci-patterns #greedy #dynamic-programming 

### From LC Discussion
https://leetcode.com/problems/optimal-account-balancing/
https://leetcode.com/problems/optimal-account-balancing/solutions/757795/easy-to-understand-greedy-size-combination-faster-than-100/?languageTags=python

#### My attempt 2023-01-17
#todo : orderedDict needs 2ndary sort

```python
from itertools import combinations
class Solution:
        def mostVisitedPattern(self, username: List[str], timestamp: List[int], website: List[str]) -> List[str]:
            '''
            EG-case1: -> ["home","about","career"] (score = 2)

            - In timestamp order? No

            Analysis
            - Tuples are arrays zipped, look like click-stream or behavioral data
            - Sites [a, b, c, d] in order, yields abc, abd, acd, bcd

            - build dict of users to activity stream
            - for each user:
                - gen combinations
                - for each:
                    add/increment count for map of combo-as-string -> count
            '''
            # print(list(combinations(["a", "b", "c", "d"], 3)))

            tuples = list(zip(timestamp, username, website))
            tuples.sort(key=lambda t: t[0])

            user_activity = {}
            for t, u, w in tuples:
                print(t, u, w)
                activity = user_activity.get(u, list())
                activity.append(w)
                user_activity[u] = activity
            print(user_activity)

            patterns = {}
            # Track pattern instances 
            for id, ua in user_activity.items():
                if len(ua) < 3:
                    continue
                print(id, ua)
                combos = list(combinations(ua, 3)) if len(ua) > 3 else [ua]
                print(combos)
                for combo in combos:
                    key = "+".join(combo)
                    patterns[key] = patterns.get(key, 0) + 1

            patterns = OrderedDict(sorted(patterns.items(), key=lambda kv: kv[1], reverse=True))
            print(patterns, next(iter(patterns.items())))
            return next(iter(patterns)).split("+")
```

### My try

```Java
/*

Optimal Account Balancing

- Least amount of transactions or least amount of money?

E.g: [[0,1,10],[2,0,5]] -> [1,0,5], [1,2,5]  (Input could be the answer too?)
E.g2: [[0,1,10],[1,0,1],[1,2,5],[2,0,5]] -> [1, 4, 0]

Analysis 
- Source of money doesn't matter, like a clearinghouse
- Simple ledger? (E.g2)
  0: -10
  1: +10
  1: -1 = 9
  0: +1 = -9
  1: -5 = 4
  2: +5
  2: -5  = 0
  0: +5 = -4
  
  0 = -4; 1 = 4; 2 = 0
  
  - Need 2 DS?  Ledger - Map person->sum, Sums - Map/Ordered list sum -> list people
- Calculating the min transactions
  Given a Sum map, we match by 
  - Finding a 2nd person with compliment sum, then done
  - Adding next lowest sum/person pairs until done or diff next sum > diff
  - Split sum, and modify the sums

*/

class Solution {
  private Map<Integer, Integer> netLedger;
  private Map<Integer, Set<Integer>> sums;
  public int minTransfers(int[][] transactions) {
    this.netLedger = new HashMap<>();
    // Build ledger
    for (int i = 0; i < transactions.length; i ++) {
      int[] tran = transactions[i];
      Integer outSum = netLedger.getOrDefault(tran[0], 0) - tran[2];
      netLedger.put(tran[0], outSum);
      Integer inSum = netLedger.getOrDefault(tran[1], 0) + tran[2];
      netLedger.put(tran[2], inSum);
    }
    
    // Calculate transactions
    this.sums = new HashMap<>();
    List<int[]> minTransList = new ArrayList<>();
    for (int key : netLedger.keySet()) {
      Integer sum = netLedger.get(key);
      if (sum == 0) continue;
      Set persons = sums.getOrDefault(sum, new LinkedHashSet());
      persons.add(key);
      sums.put(sum, persons);
    }
    
    int minTrans = this.sums.size();
    
    // First simplify by finding exact matches
    Set<Integer> keys = sums.keySet();
    for (int sum : keys) {
      if (sums.containsKey(sum * -1)) {
        Set<Integer> posPersons = sums.get(sum);
        int pos = posPersons.iterator().next();
        posPersons.remove(pos);
        if (posPersons.size() == 0) {
          sums.remove(sum);
        }
        Set<Integer> negPersons = sums.get(sum * -1);
        int neg = negPersons.iterator().next();
        negPersons.remove(neg);
        if (negPersons.size() == 0) {
          sums.remove(sum * -1);
        }
        minTransList.add(new int[] {pos, neg, sum});
      }
    }
    
    return 0;

  }
}
```