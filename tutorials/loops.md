---
sort: 7 # Order in the sidebar
#permalink: /tutorials/expressions
---

# Loops

Now that we have an idea of what `Input` is and how to use it, we're ready to start getting into the idea of *loops*. First, we'll start off with a breakdown of what a loop is, and then from there we'll step up into how to do something similar to that in BoGL.

For starters, let's think of a situation we can use. There are many cases that the idea of a loop can apply to, but in ours we're going to think of summing up a bunch of numbers. Let's say our example board game is a 1x5 board. So it's just 5 spaces all in a row. This would look something like [4,1,9,5,10]. If we wanted to calculate what all these numbers would be, we would get 29.

If we wanted to do this in BoGL, we could try and write something like so:

{% highlight haskell %}
game Loops

type Board = Array(1,5) of Int

numbers : Board
numbers!(1,1) = 4
numbers!(1,2) = 1
numbers!(1,3) = 9
numbers!(1,4) = 5
numbers!(1,5) = 10

sumAll : Int
sumAll = numbers!(1,1) + numbers!(1,2) + numbers!(1,3) + numbers!(1,4) + numbers!(1,5)
{% endhighlight %}

This would work for our board of numbers, but what if it's larger, what if it's 10 or 20 numbers? As you may be thinking now, wow, that's going to be a lot of additions! It would be nice if there was a way to clean this up a bit, and to describe the process of *iterating* through all these numbers until we're done. It turns out there is a way to do it, with loops!

So, first, how do we write loops? Loops are declared using a **while** expression. After the word `while`, we give it a way to tell how long to loop for, formally called the **condition**. This will be in the form of a `Bool`, and as long as it's true, it will keep running what's called the **body**. The body is the next bit of a while, and it indicates what we're doing every time we loop. Altogether, a while looks a bit like this:

```
while condition do body
```

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

Our above sum function is a bit more complex than we were expecting perhaps, but we'll be able to simplify it to just `sum` when we get to the end. But first, there are some important parts we want to make sure you're familiar with, so let's break those down.

First, why is the signature `(Int,Int) -> (Int,Int)`? For this version, we're taking the starting index of where we want to sum from, and also the starting value of our sum. The reason we must do this will become clear in a moment. Our **while** has a condition of `x <= count`, so while x is less than or equal to the count, we will 'do' what is in the body. In turn, our body is `(x+1, total + numbers!(1,x))`, or more simply `(index forward one, our sum plus the number at this index)`.

Notice that this matches the form of the function that while is a part of. The body of a while loop must match the type of the context before it. In some cases this is a function, but in other cases this may be a let expression, like:
{% highlight haskell %}
toZero : Int
toZero = let x = 10 in while x > 0 do x-1
{% endhighlight %}

Notice here, the context that precedes the while is a **let** expression, with a type of **Int**. When you have more than one context, i.e. a function and a let, or multiple lets, the *last one before the while takes precedence*. For example consider the following program where the context is for `let z = True`, z being a `Bool`:
{% highlight haskell %}
-- This will NOT work!
-- The context of our while is for a 'Bool'
-- Although we can use 'y', this while can only return True/False
another : Int -> Int
another(x) = let y = 20 in
             let z = True in
             while y > 0 do y-1
{% endhighlight %}
Even though our while loop seems to be fine, properly using **y** as an `Int`, it is contained within the context of `let z = True`. This means that our while loop should produce exactly a `Bool` every time it does something. A fixed up version of our program above could be made by switching y and z.
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

To make an important point of the comments above, the only thing you can change is the value of your context, that's it. If we rewrite the loop above to this, we have a problem:
{% highlight haskell %}
-- this will loop forever, but bogl will stop you after a few seconds
infiniteLoop : Int
infiniteLoop = let a = 10 in
               let b = 20 in
               while a > 0 do a-1
{% endhighlight %}
Although it looks like we should be changing `a`, we can only change our immediate context, which is an `Int` named `b`. Every time we loop, the value of `a` will be 10, as it was before. So remember when you're writing a loop, *a while can only update the value of it's context, and nothing else*. If your loop is misbehaving, think carefully about whether you are updating the name associated with your context, or something else by accident.


Finally, it is possible to take advantage of context to cleanup our example from before. Instead of having to pass in the index, and an initial result, and getting back a tuple of both of these at the end, we can add a couple functions to make it a simple `sum`.
{% highlight haskell %}
-- asuming count, numbers, and the board type are all the same from before...

-- A handy function to get the 2nd element
-- of the tuple passed, which is the value we want
-- ignores the 1st item, and gives back the 2nd
snd : (Int,Int) -> Int
snd(first,second) = second

-- the complex sum from before
-- which we can use in another function,
-- along with our 'snd' function above
complexsum : (Int,Int) -> (Int,Int)
complexsum(x,total) = while x <= count do (x+1, total + numbers!(1,x))

-- our end result, a handy sum that calls our
-- complexsum with the appropriate parameters,
-- and returns the 2nd value in the tuple we get from it
sum : Int
sum = snd(complexsum(1,0))
{% endhighlight %}

Now typing in `sum` will sum all the values on our board, immediately giving us the 29 we were looking for with no fuss. As you may be thinking, you can use this style of carrying *state* in your loops to allow them to work, but using handy functions like the `snd` I wrote above to extract the part you care about.
