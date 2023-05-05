\[Group Anagram\]
(leetcode https://leetcode.com/problems/group-anagrams )

**TRICK**: Sort word as key to dict of Lists of words. Alternative to sort would be some sort of bitmask

... like roll a 1 into an int by ord(letter) - ord('a')

```python
class Solution:
  '''
  TRICK:  Sort word as key to dict of Lists of words.  Alternative to sort would be some sort of bitmask
            ...  like roll a 1 into an int by ord(letter) - ord('a')
          
  Analysis:
  - Sort key, map words
  '''
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        ret_dict: dict[str, List] = {}
        for word in strs:
          # print(word, ret_dict)
          s_word = ''.join(sorted(word)) if len(word) else ''
          if s_word not in ret_dict.keys():
            ret_dict[s_word] = []
          ret_dict[s_word].append(word)
          
              
        ret_dict[s_word].sort()
        # print(ret_dict)
        return ret_dict.values()
```

```java
/*

E.g.: ["eat","tea","tan","ate","nat","bat"] => [["bat"],["nat","tan"],["ate","eat","tea"]]

E.t.: ["a"] => [["a"]]

Clarification:

- dupe strings?  no

Analysis:

- Sorted strings can used to match
- Sorted strings can be used to hash, map to original strings

- #1: For each string:

        sort, add to map
      For each map key, add values to return list

 */

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
      Map<String, List> anagrams = new HashMap<>();
      List<List<String>> retLists = new ArrayList<>();
      for (String str : strs) {
        char[] tmp = str.toCharArray();
        Arrays.sort(tmp);
        String hash = new String(tmp);
        if (!anagrams.containsKey(hash)) {
          anagrams.put(hash, new ArrayList());
        }
        anagrams.get(hash).add(str);
      }
      //System.out.println("Ret: " + anagrams);

      for (String key : anagrams.keySet()) {
        retLists.add(anagrams.get(key));
      }

      return retLists;
    }
}
```