#### 2nd Try, Working, Dynamic #dynamic-programming #python #code-interview 
```python
TWEENS = ["ten",  # ???
          "eleven",
          "twelve",
          "thirteen",
          "fourteen",
          "fifteen"
          "sixteen",
          "seventeen",
          "eighteen",
          "nineteen"]

TENS = ["",
        "ten",
        "twenty",
        "thirty",
        "forty",
        "fifty",
        "sixty",
        "seventy",
        "eighty",
        "ninety"]

DIGITS = ["",
          "one",
          "two",
          "three",
          "four",
          "five",
          "six",
          "seven",
          "eight",
          "nine"]

THOUSANDS = ["",
             "thousand",
             "million",
             "billion"]


def textNumbers(num, thousands=0):
    '''
    EG-t: 1-digit, 0..9.  -> text for digit
    EG-w: 1000 -> "one thousand"
    EG-w: 1000000 -> "one thousand"

    Analysis
    - Pattern:  sets of 3, with modifier, left to right?
        - Modifier based off of remaining - or *level*
        <triplet-2> + " " + <thousands-2> + " " + <triplet-1> + " " + <thousands-1> + " " + <triplet-0>
    - Can pop off stacks, or unwind.  Latter should be easier - (Dynamic)
      - Local subproblem is creating triplet words from current remainder
    - Triplet pattern: DIGITS(triplet/100) + "hundred" + TENS(remainder/10) + DIGITS(remainder/10)
      - TWEENS is special case of TENS, < 20
     '''

    if num == 0:
        return ""
    # print("calc", num, thousands)

    remainder = num % 1000
    trip_words = tripWords(remainder, thousands)
    new_num = int(num / 1000)

    # print("...", new_num, remainder, trip_words, sep="|")

    # Combine local solution with (recursive) subproblem
    result = textNumbers(new_num, thousands + 1) + trip_words
    return result


def tripWords(triplet, thousands):
    trip_words = ""
    # Take off the hundreds
    if triplet > 99:
        trip_words += DIGITS[int(triplet / 100)] + " hundred "
        triplet = triplet % 100
    if triplet > 9 and triplet < 20:
        trip_words += TWEENS[triplet - 10]
    else:
        if triplet > 9:  # two digits still
            trip_words += TENS[int(triplet / 10)] + " "
            triplet = int(triplet % 10)
        trip_words += DIGITS[triplet] + " "
    if triplet > 0:
        trip_words += THOUSANDS[thousands] + " "

    return trip_words


# textNumbers(214)
print(textNumbers(100))  # one hundred
print(textNumbers(1000))  # one thousand
print(textNumbers(1001))  # one thousand one
print(textNumbers(97214))  # ninety seven thousand two hundred fourteen
print(textNumbers(123456789))  # one hundred twenty three million ...

```
#### First Try, Live Interview (Nuna)

```python
def textNumbers(num):
    '''
    EG-t: 1-digit, 0..9.  -> text for digit
    EG-w: 1000 -> "one thousand"
    EG-w: 1000000 -> "one thousand"

    Analysis
    - Pattern:  sets of 3, with modifier, left to right
        - Modifier based off of remaining
    '''

    results = []
    triplet_counter = 0
    digit_counter = 0
    while num > 0:
        if num >= 1000:
            triplet = num % 1000
        print(num, triplet)
        triplet_counter += 1
        modifier = MODIFIERS[triplet_counter]
        while triplet > 0:
            if triplet >= 10:
                triplet = triplet % 10
            results.push(DIGITS[triplet]).push(TRIP_MODS[digit_counter]).push(modifier)
            digit_counter += 1
            
        num = int(num / 1000)
    

# textNumbers(214)
textNumbers(1000)
textNumbers(97214)
textNumbers(123456789)
```
