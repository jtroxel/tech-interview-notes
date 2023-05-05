from Exponent

[Jacob SimonSoftware Engineer, Co-founder at Exponent](https://www.tryexponent.com/coaching?role=swe)

Was this helpful?

👍👎[Send feedback](mailto:support@tryexponent.com?subject=Lesson%20Feedback%20on%20%22Practice%3A%20Maximum%20Profit%22)

You and your friend have decided to start an international trading business. You want to earn a profit through some ol' fashioned arbitrage: You'll buy widgets in one country and sell them in another at a higher price. Your friend has already found the current market prices for widgets in cities around the world, and you'd like to use this data to pick which cities to buy and sell widgets in.

Write a function max_profit(prices)that efficiently finds the two cities that maximize your profit (i.e. largest difference in prices).

Input: A dictionary with cities as keys and prices as values Output: An array (or tuple) containing the *names*of the cities (min, max)

```
def max_profit(prices):
  # Your Code Here...
```

### Example

```
prices = {'London': 72, 'New York': 70, 'Tokyo': 67, 'Miami': 62}

max_profit(prices) # => ('Miami', 'London')
```