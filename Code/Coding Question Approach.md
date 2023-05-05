### Challenges, Problems, Interview

## Code Template

```
/*
PROBLEM: /name

EG:
Ep (Prime): (Expand given if nec?)
Et (Trivial):
Base: // when you are done, return
Edge:
Other:

Clarifications:
Q.

Solution Discussion:

 - BF:

 -
 */
```

## Approach Notes

|  |  |  |
| --- | --- | --- |
| **Listen, notice, restate** | Don't write | **1-2 m** |
| **Example, Questions & Assumptions** | **EG,** edge cases, size/scope, complexity priority<br>Tests (write some up front if possible) | **\-\- 7m** |
| **Analysis & Design** | 1.  Look for **[[Coding Interview Patterns Index]]**<br>2. **BF**<br>2.  **Consider Map Tracking, Divide and Conquer**, prefix sum<br>3.  **DIY - IF Stuck**<br>4.  **Simplify, start base & build, trivial tests** | **--12-15m** |
| **Optimize: Review, Improve** | 1.  **Talk through EG**<br>2.  **Bottlenecks, Unnecessary code**<br>3.  **Hash? Subproblems?** |  |
| **Start Coding** | **Should be coding by 20m or w/ 25m remaining?** | **20m** |

1.  Listen, notice, restate - 1-2m
2.  Example, Questions & Assumptions - -7
    edge cases, size/scope, complexity priority
    Tests (write up front if possible)
3.  BF... - -12-15m
    - DIY *if stuck*
    - Simplify, start base & build, trivial tests
    - Look at BigO, think about "Best Conceivable," probably O(n) or O(n log(n))
4.  Optimize I: Review, Improve
    - Bottlenecks, Unnecessary code
    - Hash? Subproblems?
5.  Walk through with example (if time) - !! **-20m** !!

* * *

1.  Code. R/G/R
2.  Optimize II, add tests. Ask for additions

### TIPS

- **I am great to work with: friendly, positive, humble, and sharp**. Pretend that I am showing my process to a friend, and someone else is evaluating for comm. and teamwork.  Act like a leader
- Head up high, chin down.  Smile a little, not a lot.  Close your mouth.
- Demonstrate thoroughness, anticipation
- Demonstrate teamwork: ask questions, ask for help, surface issues that you missed
- Keep stateful junk in top layers, esp for recursive stuff
- Top level always calls an internal with initial conditions

### CtCI:

1.  *Listen*: Carefully.  You need all the info, think about what is unique.  What do they give away?
    Questions: edge cases, size/scope, tests, complexity priority. Tests (up front)?
    
2.  *Example*:  Capture or define the given or "primary" Example.  Make sure it isn't just a special case, and is large enough, expand on the given if nec.
    
3.  *Draw* the Example. In comments
    
4.  *State* / *draw* the Brute Force approach.
    
    1.  Naive solution, If stuck think DIY, base and build
5.  Improve on the base.
    
    1.  Unused info
    2.  Different example
    3.  Try an incorrect approach.  Simulate steps, flip assumptions.  Why would it be wrong?
    4.  Look for Unnecessary/ Duplicate work, Bottlenecks. Hash or Memoize results?
6.  Walk through the Solution
    
7.  Code
    
8.  Test
    
9.  Re-Optimize:  Bottlenecks, Unnecessary bits, Duplicated work.
    

### ESTCV:

1.  **Write *E*xamples and Clarify the Question**: You need to write examples, and in the process, ask questions that unearth the actual problem the interviewer wants you to solve.
    
2.  **Come up with *S*olutions** Come up with solutions and explain them to the interviewer, and once the interviewer seems to settle on one, write down simple steps, not more than a few lines. Doing this makes it clear (to both of you) what you will code for the rest of the interview.
    
3.  **Write down *T*est cases** When an interviewer sees you do this, they know you are legit. Quickly jot down key test cases.
    
4.  **Write *C*ode** Write the actual code. Make liberal use of helper functions.
    
    1.  Me:  Code with stubs & comments first
5.  ***V*erify code and test cases** Once you are done, make sure you step through the code and make sure it works.
    

### Behavior Tips

1.  **Talk while coding** \- Long gaps are bad, especially in phone interviews. Rule of thumb: don't have silences longer than 1 minute.
    
2.  **Ask lots of questions** \- The interviewer expects you to ask questions that clarify requirements. That is a basic skill they are trying to assess.
    
3.  **Be very humble** \- If the interviewer suggests something, show that you are open to suggestions and improvement. If you don’t know stuff, say it. That’s ok.
    
4.  **Your tone should be polite and slow** \- The interviewer should want to work with you, and should be able to clearly understand you.
    
5.  **Do not over advocate your solution** \- A lot of times interviewers have a particular solution in mind and are not able to grasp other solutions. Thats their fault, we know. However, if you argue too much, it is usually a red flag. They are in a position of power after all. Instead, be open to other solutions, and suggest that yours could work too with concrete examples
    
6.  **Slow down** \- you don’t need to hurry into the solution, no one is timing you. Yes, you want to finish coding in good time, but if you don't plan out your solution first, you will end up implementing the wrong solution - and that's worse.
    
7.  **Ask questions about the job** \- Ask about the work culture, team structure, technologies used, hierarchy, etc. You can also ask personal questions to the interviewer like - how long have you been here, what do you like about the company, etc. The interviewer should know that you are genuinely interested in working with them and the company.
    

* * *

### 09/09/2022 interviewing.com - Jovan

https://start.interviewing.io/feedback/06HXHXBKvnmt?id=63175c1ad0f7790046b67cc4 \- His feedback, notes

- [ ] Nix writing down a restatement, just say it
- [ ] Keep a timer