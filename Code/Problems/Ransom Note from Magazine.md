Ransom Note from Magazine
### Tricks
- Map magazine chars to counts
- Consume note chars, decrementing from mag, until done
- 
```
class Solution:
  '''
  EG:   ransomNote = "a", magazine = "b" -> false
        "ab", "aab" --> true
        
  - Each char used individually
  
  Analysis
  - Sort mazagine first?  addl O(n log(n))
  - 2 passes:  build map of letters, counts, then match & decrement until 0
  
  
  '''
  def canConstruct(self, ransomNote: str, magazine: str) -> bool:
    magazine_letters = {}
    for i, ch in enumerate(magazine):
      if not ch in magazine_letters:
        magazine_letters[ch] = 0
      magazine_letters[ch] += 1
    print(magazine_letters)
    
    for i, ch in enumerate(ransomNote):
      print(ch, ransomNote)
      if ch not in magazine_letters or magazine_letters[ch] == 0:
        return False
      magazine_letters[ch] -= 1
      ransomNote = ransomNote[:-1]
      
    return True
```