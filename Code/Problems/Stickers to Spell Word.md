Stickers to Spell Word
[LC](https://leetcode.com/problems/stickers-to-spell-word/)

### Tricks

- Use array of ints for counts of chars by ord
- Nested compare of sticker chars with word
    - Subtract and increment count
- Count use bitmaps to quickly get matching chars out of a sticker, decrement those

```python
class Solution:
  
  stickers = []
  '''
  Stickers to Spell Word
  
  Use letters from any number of the stickers provided to spell a target word...  what is the minimum # of stickers target?
  
  - Edges:
    - Impossible --> -1
    - empty --> -1
    - Sticker-type for every character -> max result len(target)
  - Max 10 stickers
  - target = 15
  - Infinite if each
    
  EG:  ["with","example","science"], target = "thehat" --> 3
  
  Analysis
  - Need to know characters in each word, counts per word
  - characters in target, with counts
  
  - Trick is how to evaluate options, effeciently compare fit...
  - What about sorting...  
  - sparse array with index = ch -'a', values counts of words?  Or roll left...  OR bitmask
    - with bitmasks, can do substraction to find the closest word, then iterate?
    
  BF:  Iterate through the target, look for and subtract charaters from list of stickers
       start by mapping the matching characters and counts to the words in the list
       - Take all the chars from each sticker
       - DFS
      For each sticker, add all the characters, then recurse down
        For each other sticker, recurse down
        subtrac the found characters as we go
        
        Base case: whenn no more chars from sticker are in the remaining target

  
  Find the closest word, min (bitmask subtract)
       - take that word (res++)
       - iterate on the diff
  
  '''
  def minStickers(self, stickers: List[str], target: str) -> int:
      max_ans = len(target) + 1
      m = len(stickers)
      mp = [[0]*26 for y in range(m)] 
      for i in range(m):
          for c in stickers[i]:
              mp[i][ord(c)-ord('a')] += 1    
      dp = {}
      dp[""] = 0
      
      print(mp)

      def helper(dp, mp, target):
          if target in dp:
              return dp[target]
          n = len(mp)
          tar = [0]*26
          for c in target:
              tar[ord(c)-ord('a')] += 1   
          ans = max_ans
          for i in range(n):
              if mp[i][ord(target[0])-ord('a')] == 0:
                  continue
              s = ''
              for j in range(26):
                  if tar[j] > mp[i][j]:
                      s += chr(ord('a')+j)*(tar[j] - mp[i][j]) 
              tmp = helper(dp, mp, s)
              if (tmp != -1): 
                  ans = min(ans, 1+tmp)    
          dp[target] = -1 if ans == max_ans else ans
          return dp[target]

      return helper(dp, mp, target)
```