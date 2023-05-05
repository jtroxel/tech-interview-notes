Example "take-home" from coderpad.  I think this mostly runs except extra spaces on the end.

```
import java.io.*;
import java.util.*;

/*

Examples
“pig” => “ig-pay”
“pig latin” => “ig-pay atin-lay”
“Pig Latin” => “ig-Pay atin-Lay”

"thor" -> or-thay // cluster of consonants
apple -> apple-way
Out house -> out-way ouse-hay

Solution Discussion:

 - BF:

   // Seperate works - for each-way
   //   if first letter is vowel, don't seperate
   //   else find first vowel index
   //   separate string from 0..vowelIdx
   //   print prefix, suffix

 - Refine

*/
class Solution {
  public static int TOP_CAP_ASCII = 90;
  public static String ALL_VOWELS = "aeiouAEIOU";
  public static String solution(String phrase) {

    StringBuilder bld = new StringBuilder();

   // Seperate works - for each-way
   for (String word : phrase.split(" ")) {
     String prefix = word, suffix = "";
     String firstLetter = word.substring(0, 1);
      //   if first letter is vowel, don't seperate
     if (ALL_VOWELS.contains(firstLetter)) {
       if (firstLetter.getBytes()[0] < TOP_CAP_ASCII) {
          suffix = "Way";
       } else {
         suffix = "way";
       }
    //   else find first vowel index
     } else if (isLetters(firstLetter)){
    //   separate string from 0..vowelIdx

       int startVowels = 0;

       while (startVowels < word.length()-1 && !ALL_VOWELS.contains("" + word.charAt(startVowels))) {

         //System.out.println("'" + word + "': v at " + startVowels);
         startVowels++;
       }
       //System.out.println("'" + word + "': v at " + startVowels);
       suffix = word.substring(0, startVowels) + "ay";
       prefix = word.substring(startVowels);

     }
      System.out.println("'" + prefix);

      //   build prefix, suffix
      bld.append(prefix);
      if (suffix.length() > 0) {
        bld.append("-").append(suffix);
      }
      bld.append(" ");
    }
    return bld.toString();
  }
  static boolean isLetters(String letters) {
    for (Character c : letters.toCharArray()) {
      if (c < 65 || c > 122 || (c > 90 && c < 97)) return false;
    }
    return true;
  }
}
```