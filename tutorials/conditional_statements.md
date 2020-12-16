---
sort: 7 # Order in the sidebar
#permalink: /tutorials/expressions
---
 
# If/Else Statements 


:construction: Under construction :construction:

Sometimes you may want the resulting value of an expression to be dependent on a *condition*.
In BoGL you can write a *conditional expression*, also known as an *if/else statement* or *conditional statement*.
A conditional expression is composed of three sub-expressions.

![conditional expression anatomy](../imgs/conditional_logic-conditional-expression-anatomy.jpg)

To write a conditional expression, you must first write the keyword `if`, followed by an expression that evaluates to a Bool.
After writing this first expression, you write the keyword `then`, followed by a second expression (which does not have to evaluate to a Bool).
After writing this second expression, you then write the keyword `else`, followed by a third expression (which also does not have to evaluate to a Bool). The line below shows that this will look like written out, with the word *expression* being a placeholder for where an actual BoGL expression would be.

**if *<span style="color:#D3A500">expression</span>* then *<span style="color:#00A600">expression</span>* else *<span style="color:#A60000">expression</span>***

The <span style="color:#D3A500">first</span> expression (located after the keyword `if`) in a conditional expression is the condition. This expression will determine which of the next two expressions to evaluate.
The condition must evaluate to be a Bool(True or False) value.

The <span style="color:#00A600">second</span> expression (located after the keyword `then`) is what is evaluated when the condition is **True**.

The <span style="color:#A60000">third</span> expression (located after the keyword `else`) is what is evaluated when the condition is **False**.


<br/>
:hammer_and_wrench: **Example: Coin Toss**

Lets return to our example with Jack and Rosa, which we last visited in the [functions tutorial](./functions).  

{% include code_module_template.html 
content = "game WhoGoesFirst

type TossResult = {Heads, Tails}
type Player = {Jack, Rosa}

coin : TossResult
coin = Heads

determineFirstPlayer : TossResult -> Player
determineFirstPlayer(coinSide) = Rosa
"
%}

The goal of our program is to determine a first player for a game using a coin toss result.

The function *determineFirstPlayer* will return a *Player* value, and takes a *TossResult* value as an argument. Right now, no matter if the TossResult value is Heads or Tails, Rosa will always be returned by the determineFirstPlayer function. To change this function so that Jack or Rosa can be returned depending on the TossResult argument, we can use a conditional experssion.

The modified function below will return Rosa or Jack depending on whether the value provided to it's TossResult parameter is Heads or Tails.
{% highlight haskell %}
determineFirstPlayer : TossResult -> Player
determineFirstPlayer(coinSide) = if coinSide == Heads then Rosa else Jack
{% endhighlight %}

Try this out in the interpreter!

:dart: **Excercise:**  

What happens when you type `determineFirstPlayer(Heads)` into the interpreter below?  
What happens when you type `determineFirstPlayer(Tails)` into the interpreter below?

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
