---
sort: 6 # Order in the sidebar
#permalink: /tutorials/expressions
---
 
# If/Else Statements 

:construction: Under construction :construction:

Sometimes you may want the resulting value of an expression to be dependent on a *condition*.
In BoGL you can write a *conditional expression*, which can also be refered to as an if/else statement.
A conditional expression is composed of three sub-expressions.

![conditional expression anatomy](../imgs/conditional_logic-conditional-expression-anatomy.jpg)


The first expression (located after the keyword `if`) in a conditional expression is the condition. This expression will determine which of the next two expressions to evaluate.
The condition must evaluate to be a Bool(True or False) value.

The second expression (located after the keyword `then`) is what is evaluated when the condition is True.

The third expression (located after the keyword `else`) is what is evaluated when the condition is False.

<br/>
#### Example: Coin Toss
The function below will return Rosa or Jack depending on whether the value provided to it's TossResult parameter is Heads or Tails.
{% highlight haskell %}
determineFirstPlayer : TossResult -> Player
determineFirstPlayer(coinSide) = if coinSide == Heads then Rosa else Jack
{% endhighlight %}

Try this out in the interpreter!

{% include code_module_template.html 
content = "game WhoGoesFirst

type TossResult = {Heads, Tails}
type Player = {Jack, Rosa}

coin : TossResult
coin = Heads

determineFirstPlayer : TossResult -> Player
determineFirstPlayer(coinSide) = if coinSide == Heads then Rosa else Jack
"
%}

What happens when you type `determineFirstPlayer(Heads)`?

What happens when you type `determineFirstPlayer(Tails)`?
