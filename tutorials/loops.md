---
sort: 7 # Order in the sidebar
#permalink: /tutorials/loops
---

# Loops

## Introduction

There are many tasks that require some form of repeated action, such as counting up to 10, calculating the factorial of a number, or slowly adding ingredients until the flavor is where you want it to be. These all let us perform an action for as long as a condition is satisfied. We could also perform each of these without loops, but only for a constant number of times. For example you may be counting to 10 from 3, 9 or -1000, and writing a function for each would be tedious. Similarly, if we want to calculate the factorial of any number, we're going to want a way to do this for any `x`, rather than writing all possible factorials out. For each of these, a `while` loop would help to solve our problem.

## What are While Loops?

A while loop is an expression in BoGL that takes two other expressions, a condition and a body. The condition is an expression that evaluates to a result of `Bool`. The body is an expression that is evaluated every time the condition evaluates to `True`. A while loop repeatedly evaluates the condition, and for each time that it is `True` it evaluates the body again. Once the condition evaluates to `False`, the while loop returns the last value produced by the body. If the condition evaluates to `False` on the first check, the body is never evaluated, and the value that was passed into the while loop is returned unchanged.

## How to write Loops

So, first, how do we write loops? In BoGL, we begin with a `while`. Following the `while` keyword, we give our **condition** expression. This can be any expression, so long as it produces a `Bool`, as mentioned before. After the condition you write in `do`, which indicates that the **body** expression will follow. The **body** expression is evaluated as long as the condition evaluates to `True`.

In the case of counting up to 10, our condition would `x < 10` and our body would be `x + 1`. This means that so long as `x` is less than 10, our body will be evaluated, producing a new `x` with the value of `x+1` until our condition returns `False`. This looks like the following in BoGL.

![while loop, showing the condition and then the body](../imgs/while-loop.jpg)

If we give a value of `x=7` to this while loop, we would get the following execution:

```
while 7 < 10 do 7 + 1
while 8 < 10 do 8 + 1
while 9 < 10 do 9 + 1
10
```

If we were to write this into a BoGL program, using functions, we could express this as the following. To try it out, you can run `count(0)` in the example below.

{% include code_module_template.html
content = "
game Count<br/>
<br/>
count : Int -> Int<br/>
count(x) = while x < 10 do x + 1
"
%}

In the case where we call our function with a value greater than 10, like `count(15)`. We would get the same number back. Our condition `15 < 10` evaluates to `False`, and so the body is not evaluated. In this case, the while loop evaluates to the value of `x`.

## Context for Loops

Another example could be calculating the factorial of a number. Similar to our example above, we can produce this by counting, but in the other direction. However, there is an added problem of **context**. This is the immediate value that the while loop can change. There are two things that can set the context.

The first, **functions** (like our example above), set the context to the parameter passed. If a function takes an `(Int,Bool)` pair, then the context of the following while is for that same `(Int,Bool)`.

{% highlight haskell %}
-- counts to zero, and returns (0,b)
-- Context is for an (Int,Bool) tuple named (i,b)
f : (Int,Bool) -> (Int,Bool)
f(i,b) = while i > 0 do (i-1,b)
{% endhighlight %}

The second, **let expressions**, set the context to the named value that precedes the while expression.

{% highlight haskell %}
-- Context is for an Int named 'x'
a : Int
a = let x = 5 in while x < 20 do x * 2
{% endhighlight %}

If you mix these, the rule is that the last one takes effect. Although the names from other contexts can be used, the type that the while produces must match that of the last context. Consider the following example:

{% highlight haskell %}
game Ex

f : (Int,Bool) -> Bool         -- 1st context, (Int,Bool) named (i,b)
f(i,b) = let x = True in       -- 2nd context, Bool named x
         let z = 5 in          -- final context, Int named z
         while z > 0 do z - 1  -- and so our while produces an Int, only changing 'z'
{% endhighlight %}

Keep in mind that if you have multiple contexts of the same type, you may only change the value of the most recent context. If you are not careful about this you can introduce an infinite loop by using a name in the condition that never changes.

{% highlight haskell %}
game Ex

-- this will loop infinitely
-- as the condition is on a value that never changes.
-- x will always be 1.
infinite : Int
infinite = let x = 1 in -- 1st context is x of Int
           let y = 2 in -- 2nd context is y of Int
           while x > 0 do x - 1 -- the type is correct, but only y will update when we loop!
{% endhighlight %}

To remedy the situation above, we could change our while loop to update and check `y` instead. This is the only value we can change, as it is in the closest context to the while loop.

## Loops with Tuples

In some cases you may need to use a tuple to allow a loop to properly accumulate some value. Take for example `factorial`. If we want to take `x!`, we need to both count from `x` to 1 and store the product of all the numbers along the way. We can achieve this using a tuple of `(Int,Int)`. In our example the tuple will represent `(Number,Product)`, where `Number` is the number we are taking the factorial of, and `Product` is our current product. Our while loop should have a condition of `x > 1`. While this is true, we want to decrement our number by 1 and multiply our product by this number.

{% highlight haskell %}
game Factorial
-- factorial takes (Number,Product)
-- ex. (5,1)
-- Our product must always start at 1 to produce the correct result

factorial : (Int,Int) -> (Int,Int)
factorial(num,prod) = while num > 1 do (num - 1, prod * num)
{% endhighlight %}

Now this example is a bit cumbersome, as we have to type in `factorial(5,1)`, and we get back `(1,120)`. We probably want to run `factorial(5)` and just get `120` on by itself. To do this, we can write an additional function to return the second element of a tuple. This will allow us to get the final product out of the result. To simplify the input, we can use what we learned about context before to allow our function to take a single Int.

{% highlight haskell %}
game Factorial

-- get the 2nd element
snd : (Int,Int) -> Int
snd(a,b) = b

-- takes a num and 1, and returns the 2nd element of the while result
factComplex : (Int,Int) -> Int
factComplex(num,prod) = snd(while num > 1 do (num - 1, prod * num))

-- our new factorial function w/ a single parameter
factorial : Int -> Int
factorial(num) = factComplex(num,1)
{% endhighlight %}

By using a second function, we can use the context of another function to simplify what we need to pass to `factorial`.
