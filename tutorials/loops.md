---
sort: 8 # Order in the sidebar
#permalink: /tutorials/expressions
---

# Loops

## Introduction

Now that we have an idea of what `Input` is and how to use it, we're ready to start getting into the idea of *loops*. First, we'll start off with a breakdown of what a loop is, and then we'll explain how to implement it in BoGL.

For starters, let's think of a situation we can use. There are many cases where a loop can be used. In ours we're going to think of summing up a bunch of numbers. Let's say our example is a board of 5 spaces, or a 1x5 board; so it's just 5 spaces all in a row. If each space can have a number, it might look something like `[4,1,9,5,10]`. If we wanted to calculate the sum, we would get 29. Now, the question is how do we calculate the sum?

If we wanted to do this in BoGL, we could write something like this:

{% highlight haskell %}
game Loops

type Board = Array(1,5) of Int

numbers : Board
numbers!(1,1) = 4
numbers!(1,2) = 1
numbers!(1,3) = 9
numbers!(1,4) = 5
numbers!(1,5) = 10

sum : Int
sum = numbers!(1,1) + numbers!(1,2) + numbers!(1,3) + numbers!(1,4) + numbers!(1,5)
{% endhighlight %}

This would work for our board of numbers, but what if it's 10 or 20 numbers? As you may be thinking, wow, that's going to be a lot of additions! It would be nice if there was a way to clean this up a bit, and to describe the process of *iterating* through all these numbers to sum them up. It turns out there is a way to do it, with loops!

## How to write Loops

So, first, how do we write loops? In BoGL, we do this with a **while** expression. After the `while`, we tell how long to loop for, something called the **condition**. This can be any expression, so long as it produces a `Bool`. As long as the value of the condition is True, the loop will keep running the **body**. The body indicates what we're doing every time we loop. Altogether, a `while` expression looks a bit like this:

![while loop, showing the condition and then the body](../imgs/while-loop.jpg)

In this case, we want our **while** to express the idea of repeating until we have summed up all numbers. An initial approach can be written like so:

{% highlight haskell %}
-- tells us how far we can go
count : Int
count = 5

-- our board of numbers to sum
numbers : Board
numbers!(1,1) = 4
numbers!(1,2) = 1
numbers!(1,3) = 9
numbers!(1,4) = 5
numbers!(1,5) = 10

-- our sum function, as a loop
-- takes the index to start, and the starting amount
-- returns where it stopped, and the new total
sum : (Int,Int) -> (Int,Int)
sum(x,total) = while x <= count do (x+1, total + numbers!(1,x))
{% endhighlight %}

Our above sum function is a bit more complex than we were expecting perhaps, but we'll be able to simplify it to just `sum` when we get to the end. However, first there are some important parts we want to make sure you're familiar with, so let's break those down.

To begin, why is the signature `(Int,Int) -> (Int,Int)`? For this function, we're taking the starting index of where we want to sum from, and also the starting value of our sum. If we wanted to sum all the numbers starting at the first one, we would write in `sum(1,0)` for the first index and a starting sum of zero. The reason we must do this will become clear in a moment. Our **while** has a condition of `x <= count`. While `x` is less than or equal to `count`, we will 'do' what is in the body. In turn, our body is `(x+1, total + numbers!(1,x))`, or more simply `(index forward one, our sum plus the number at this index)`. If we were to step through each part of the loop, we would see something like:

```
while 1 <= 5 do (1+1, 0 + 4)
while 2 <= 5 do (2+1, 4 + 1)
while 3 <= 5 do (3+1, 5 + 9)
while 4 <= 5 do (4+1, 14 + 5)
while 5 <= 5 do (5+1, 19 + 10)
(6,29)
```

## Context for Loops

Notice that the value of the body matches the type of the function that it is a part of. The body of a while loop must match the type of the context before it. In some cases this is a function, but in other cases this may be a let expression. For example:
{% highlight haskell %}
toZero : Int
toZero = let x = 10 in while x > 0 do x-1
{% endhighlight %}

Here the context is a **let** expression, with a type of **Int**. When you have more than one context, i.e. a function and a let, or multiple lets, the *last one before the while takes precedence*. For example consider the following program where the context is for `let z = True`, z being a `Bool`:
{% highlight haskell %}
-- This will NOT work!
-- The context of our while is for a 'Bool'
-- Although we can use 'y', this while can only return True/False
another : Int -> Int
another(x) = let y = 20 in
             let z = True in
             while y > 0 do y-1
{% endhighlight %}
Even though our while loop seems to be fine, properly using **y** as an `Int`, it is contained within the context of `let z = True`. This means that our while loop should produce exactly a `Bool` every time it does something. By switching y and z, we can fix this problem.
{% highlight haskell %}
-- This will work!
-- The context of our while is for an 'Int'
-- We can use both z and y if we want,
-- but our context, and all that we can change across loops, is 'y'
another : Int -> Int
another(x) = let z = True in
             let y = 20 in
             while y > 0 do y-1
{% endhighlight %}

To make an important point of the comments above regarding while loops, the only thing you can change is the value of your context, that's it. If we rewrite the loop above to the following, we have a problem:
{% highlight haskell %}
-- this will loop forever until bogl stops you
infiniteLoop : Int
infiniteLoop = let a = 10 in
               let b = 20 in
               while a > 0 do a-1
{% endhighlight %}
Although it looks like we should be changing `a`, we can only change our immediate context, which is an `Int` named `b`. Every time we loop, the value of `a` will be 10, as it was before. Remember, when you're writing a loop *a while loop can only update the value of it's context, and nothing else*. If your loop is misbehaving, think carefully about whether you are updating the name associated with your context, or something else by accident.

## Final Example

Finally, let's improve our `sum` example from before to make it a bit easier to use. Instead of having to pass in the index, an initial total, and getting back a tuple of both of these at the end, we can add a couple functions to make it a simple `sum`.
{% highlight haskell %}
game Loops

type Board = Array(1,5) of Int

count : Int
count = 5

numbers : Board
numbers!(1,1) = 4
numbers!(1,2) = 1
numbers!(1,3) = 9
numbers!(1,4) = 5
numbers!(1,5) = 10

-- A handy function to get the 2nd element
-- of the tuple passed, which is the value we want.
-- Ignores the 1st element, and gives back the 2nd
snd : (Int,Int) -> Int
snd(first,second) = second

-- the complex sum from before
-- which we can use in another function,
-- along with our 'snd' function above
complexsum : (Int,Int) -> (Int,Int)
complexsum(x,total) = while x <= count do (x+1, total + numbers!(1,x))

-- a handy sum that calls our
-- complexsum with the appropriate parameters,
-- and returns the 2nd value in the tuple we get from it
sum : Int
sum = snd(complexsum(1,0))
{% endhighlight %}

Now typing in `sum` will sum all the values on our board, immediately giving us the 29 we were looking for with no fuss. As you may be thinking, you can use this style of carrying something called *state* in your loops to allow them to work while updating a value over each iteration. When the loop is done, you can use handy functions like the `snd` I wrote above to extract the part you care about. If you wrote it the other way around, so the value you wanted was the first element in the tuple, you could write an `fst` function that returns the first element instead.
