---
sort: 9 # Order in the sidebar
---

# User Input

You can make a program interactive by using the *input* statement.
The keyword `input` acts as a placeholder that will be replaced with a value provided by the user during runtime.
Using this can allow users to make decisions while the program is running (like what move they would like to make during a turn).

When the `input` keyword is evaluated, the interpreter will prompt the user to provide input to the program (giving the message seen below).  
```
🤖 BoGL Says: Enter input, or "clear" to stop.
```
The program will not proceed until the user has typed something into the interpreter.
The prompt expects you to type in a value that matches the `Input` type, which you should define if you are using the input statement in your program.
An input that does not match the `Input` type will be rejected by the interpreter (see message below).
```
Got type Bool, but expected type Int from input.
Your last input was discarded. Please enter a new one.
```

To define the input type, you can create a type definition as you normally would, but name the type `Input`.
{% highlight haskell %}
type Input = Bool -- This tells BoGL that any user input is expected to be of type Bool
{% endhighlight %}

If the word `clear` is given as input, the program will abort.

<br/>
:hammer_and_wrench: **Example: Add Two Numbers**  
The program below will prompt the user for input twice.
The resulting value will be the sum of those two inputs.

{% highlight haskell %}
game AddTwoInputs

type Input = Int

addTwoNums : Int
addTwoNums = input + input
{% endhighlight %}

<br/>
:dart: **Excercise: Second Power**   
Write the definition for a value that takes a single integer input from the user during runtime, and then returns the integer that was input multiplied by itself.

{% include code_module_template.html
content = "game InputToSecondPower

type Input = Int

secondPower : Int
secondPower = WRITE DEFINING EXPRESSION HERE
"
%}
<details><summary>:eyes: Click to see a hint</summary>
<p>
You will have to use a local value in your defining expression.
</p>
</details>

<details><summary>:eyes: Click to see a solution (but try yourself first!)</summary>
<p>
{% highlight haskell %}
game InputToSecondPower

type Input = Int

secondPower : Int
secondPower = let x = input in x * x  
{% endhighlight %}
</p>
</details>

<br/>
:hammer_and_wrench: **Example: Rock Paper Scissors**  
Below is an implementation of the game [*Rock Paper Scissors*](https://en.wikipedia.org/wiki/Rock_paper_scissors) in BoGL.
Calling the value `playGame` will cause the interpreter to ask for user input twice, each input representing a player move.
These input player moves are stored as local values (`p1move` and `p2move`) which are then compared to see which player won the game.

{% highlight haskell %}
game LetExample

type GameOutcome = {Player1Wins, Player2Wins, Tie}
type PlayerMove = {Rock, Paper, Scissors}

type Input = PlayerMove

playGame : GameOutcome
playGame =
	let p1move = input in
	let p2move = input in
	if and(p1move == Rock, p2move == Scissors) then Player1Wins
	else if and(p1move == Paper, p2move == Rock) then Player1Wins
	else if and(p1move == Scissors, p2move == Paper) then Player1Wins
	else if and(p2move == Rock, p1move == Scissors) then Player2Wins
	else if and(p2move == Paper, p1move == Rock) then Player2Wins
	else if and(p2move == Scissors, p1move == Paper) then Player2Wins
	else Tie
{% endhighlight %}
