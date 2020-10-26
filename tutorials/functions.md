---
sort: 3 # Order in the sidebar
#permalink: /tutorials/functions
---
 
# Functions

:warning: Make sure that you have a solid understanding of [types](./types) before jumping into this tutorial.

Jack and Rosa want to play a board game. They decide that who gets to go first should be determined by the result of a coin toss.

```
game WhoGoesFirst

type TossResult = {Heads, Tails}
```

So far we have the name of our game `WhoGoesFirst` and a type for capturing a coin toss result `TossResult`. Now we need a way to get an actual value. We will do this by creating a _function_. A function consists of two parts: A 

```
result : TossResult
result = Heads
```
