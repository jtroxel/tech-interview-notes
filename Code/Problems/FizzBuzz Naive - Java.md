```Java
/* Problem: Fixx Buzz

From 1 to n:
answer[i] == "FizzBuzz" if i is divisible by 3 and 5. .. LCF = 15
answer[i] == "Fizz" if i is divisible by 3.
answer[i] == "Buzz" if i is divisible by 5.
answer[i] == i (as a string) if none of the above conditions are true.

Analysis
- Simple case statement or if/else...  3 comparisons and else
- Use LCF = 15...  up to 3
- Build return string

*/

class Solution {
    public List<String> fizzBuzz(int n) {
      List retList = new ArrayList();
      
      for (int i = 1; i <= n; i++) {
        if (i % 15 == 0) {
          retList.add("FizzBuzz");
        }
        if (i % 5 == 0) {
          retList.add("Buzz");
        } else if (i % 3 == 0) {
          retList.add("Fizz");
        } else {
          retList.add("" + i);
        }
      }
      
      return retList;
        
    }
}
```