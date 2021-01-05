---
sort: 11 # Order in the sidebar
# permalink: /tutorials/recursion
---

# Recursion

## What is Recursion?
Recursion is the act of a function making a call to itself. This technique is used to repeat computations, and can be used as an alternative to the [*while loop*](./loops).

Below is an example of what we would call a *recursive function*.

{% highlight haskell %}
recursiveFunction : Int -> Int
recursiveFunction(x) = recursiveFunction(x + 1) 
{% endhighlight %}

The function `recursiveFunction` shown above is recursive because it has a call to itself within its defining expression `recursiveFunciton(x + 1)`.
This means that if it is called initially with an argument of `1`, `recursiveFunction` will make a call to `recursiveFunction` with an argument of `2`, which will then make a call to `recursiveFunction` with an argument of `3`, which will then make a call to `recursiveFunction` with an argument of `4`, etc...

![recursiveFunction](../imgs/recursion-recursiveFunction.jpg)

The function will repeatedy call itself like this and will not stop.

<br/>
:dart: **Excercise:** 
- Try writing your own recursive function in the editor below.  
- What happens when you call the function in the interpreter?

{% include code_module_template.html 
content = "game RecursionExcercise

-- Recursive function goes here!
"
%}


## The Base Case
To prevent a recursive function from recurring forever, you must add a *base case*. The base case is described as when the argument provided to the function **will not** trigger another recurrence, and the function will instead return without calling itself again.

Reaching the base case in a recursive function often means an end to the repetition.
In this way, the base case acts similiarly to a while loop's condition.
