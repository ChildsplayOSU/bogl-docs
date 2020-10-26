---
sort: 3 # Order in the sidebar
#permalink: /tutorials/functions
---
 
# Functions

:warning: Make sure that you have a solid understanding of [types](./types) before jumping into this tutorial.:warning:

Jack and Rosa want to play a board game. They decide that who gets to go first should be determined by the result of a coin toss.

```
game WhoGoesFirst

type TossResult = {Heads, Tails}
type FirstPlayer = {Jack, Rosa}
```

So far we have the name of our game `WhoGoesFirst`, a type for capturing a coin toss result `TossResult`, and a type that can describe who the first player is `FirstPlayer`. Now we need a way to get an actual TossResult value. Since BoGL is largely a [functional language](https://en.wikipedia.org/wiki/Functional_programming) we will do this by creating a _function_ that returns such a value. 

Functions inside of BoGL are used to output, or return, some sort of value. The value that is returned from a function is often determined by the inputs provided to the function. 
If the inputs do not have an effect on the output of a function, then that function will always return the same result. To illustrate this idea, observe the math function below.

**_f(x)_ = 2**

In this function, no matter the value of the parameter **x**, the output (return) of **_f(x)_** will always be 2. Below is what this function looks like in BoGL.
```
fOfx : Int
fOfx = 2
```

To create a function we need to write two things: A declaration and a definition.

The first part of a function is it's declaration. The declaration is where the types of the function's parameters (if there are any) and return value are declared. You can write a function declaration by first writing out the function's name. Opposite of type names, function names must start with a lowercase letter. In the above example our type is named _fOfx_. After the name we write a colon `:`, which is followed by the parameter types (none in the above example), which are then followed by the output type. The above example takes no parameters, so it only needs its return type of `Int` declared.

The second part of a function is its definition. The definition is where all the logic goes that is used to determine the output value. The definition starts with the same function name that was written in the declaration, and then followed by an equals sign `=`. After the equals sign is where the logic that determines the output value goes. The code written in the function definition can often span multiple lines.

Now that we know how to create a basic function that returns a value, lets go over how to make a function that takes parameters. We will start with another math function as an example.

**_f(x)_ = 2x**

If we were to assign our parameter, **x**, the value of 3, then the value of **_f(x)_** would be 6. This function takes in a value for **x** and uses that to compute a value for **_f(x)_**, which in this case is **x** multiplied by two. We can also write this function in BoGL.
```
f : Int -> Int
f(x) = 2 * x
```



