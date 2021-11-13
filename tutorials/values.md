---
sort: 4 # Order in the sidebar
---

# Values

:leaves: **This tutorial covers:**
- Defining values
- Calling values

:seedling: **Before starting, you should be familiar with:**
- [The BoGL basics](./GettingStarted.md)
- [Types](./types)
- [Understanding Expressions](./expressions)

:deciduous_tree: **At the end, you should be able to:**
- Write a value definition
- Call a value from the interpreter


## Creating Values

Jack and Rosa want to play a board game. They decide that who gets to go first should be determined by the result of a coin toss.

In these first few tutorials, we will create a program using the BoGL language that will take the result of a coin toss and choose who gets to go first based on that result.

In order to do this, our program must be able to...

1. Capture the inputted value of the coin toss result.
2. Output whether Jack or Rosa gets to go first based off of the result value.


Jack and Rosa want to play a board game. They decide that who gets to go first should be determined by the result of a coin toss.

{% highlight haskell %}
game WhoGoesFirst

type TossResult = {Heads, Tails}
type Player = {Jack, Rosa}
{% endhighlight %}

So far we have the name of our game `WhoGoesFirst`, a type for capturing a coin toss result `TossResult`, and a type that can describe who the first player is `Player`. Now we need a way to get an actual TossResult value. In order to do this we will need to know how values work in BoGL.

To define a value in BoGL we must create a *value definition*. We can define the value of **x** to be **4** in mathematics by writing **x = 4**. Shown below is how we can define **x** as **4** in BoGL.

{% highlight haskell %}
x : Int
x = 4
{% endhighlight %}

The code above is a *value definition* for the value **x**, which we define as **4**.

The first line of a value definition is where the value's type is declared. You can write this by first writing out the name of the value. Opposite of type names, value names must start with a lowercase letter. In the above example our value is named _x_. After the name we write a colon `:`, which is followed by the value's type.

The second line of a value definition is where the value itself is defined. This line starts with the same value name that was written in the first line followed by an equals sign `=`. After the equals sign is where the logic that determines the value goes. Oftentimes this is simply a value, but can also be an [expression](./expressions) which we will cover in another tutorial.

![Anatomy of a value definition](../imgs/values-value-definition-anatomy.jpg)

Once a value definition is created, the name of the value that was defined will evaluate to it's defined value. Try typing `x` into the interpreter (right side text box) below and press the `enter` key. It will return the value defined for **x**.

{% include code_module_template.html
content = "game ValueDemo

x : Int
x = 4
"
%}

Now lets utilize what we have learned about values and [types](./types) to define a value for a coin toss result.
We will call this value _coin_. We will define it's type as `TossResult` and define it's value to be `Heads`. Here is it's definition:
{% highlight haskell %}
coin : TossResult
coin = Heads
{% endhighlight %}

Try typing `coin` into the interpreter below. It should return the value `Heads`.

{% include code_module_template.html
content = "game ValueDemo

type TossResult = {Heads, Tails}

coin : TossResult
coin = Heads
"
%}

In the next tutorial we will look at [functions](./functions), which can return different values based on inputs that are provided to them.
