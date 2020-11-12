---
sort: 10 # Order in the sidebar
# permalink: /tutorials/boards
---

# Boards

:construction: Under construction :construction:

## Background: What is a BoGL Board?
BoGL wouldn't be a board game language if there weren't a way to create a board!
*Board* is the name that *arrays* are given in BoGL.
An [*array*](https://en.wikipedia.org/wiki/Array_data_structure) in computer science is a [*data structure*](https://en.wikipedia.org/wiki/Data_structure), which is a term used to describe an organization of stored data.
Arrays are one of the simpler data structures to understand because they are often used to describe organizations that resemble lists (one-dimensional arrays) or grids (two-dimensional arrays).
For example, in the game of [Chess](https://en.wikipedia.org/wiki/Chess) the pieces are organized on a grid of squares (the board), and in the game of [Candy Land](https://en.wikipedia.org/wiki/Candy_Land) the path that the players move upon can be described as a list of squares.

It is important to note that the *board* term is specific to BoGL. If you were to directly translate a program that uses a board in BoGL to a different language, you would likely implement the board as a two-dimensional array.

## Defining a Board

To define our board, we must first write the keyword `type` followed by `Board` followed by an `=`.
After the `=` we write the keyword `Array` followed by parenthesis `()`.
Within the parenthesis are where the board dimensions are specified with two integer values seperated by a comma.
These integer values correspond to the width and length of our board respectively.
Following the parenthesis containing the board dimensions we write the keyword `of` followed by the desired
type for each square on our board. Below are a few examples of defining a board.


Shown below is how we might define a 3 by 3 [Tic-tac-toe](https://en.wikipedia.org/wiki/Tic-tac-toe) board.
{% highlight haskell %}
type TicTacToeSquare = {O, X, Unmarked} -- Board square type

type Board = Array(3, 3) of TicTacToeSquare -- Board definition
{% endhighlight %}

Shown below is how we might define a 7 by 6 [Connect Four](https://en.wikipedia.org/wiki/Connect_Four) board.
{% highlight haskell %}
type ConnectFourSquare = {Red, Yellow, Empty} -- Board square type

type Board = Array(7, 6) of ConnectFourSquare -- Board definition
{% endhighlight %}

Note that the board definition is a *type* definition. We will be using it to create board values (or *states*). 

## Creating a Board State

Using our defined board, we can create a board state (or value representing the board).
Doing this is similiar to how we would create a value normally.
We start by creating a name for our board state (must be lowercase) followed by a `:`, followed by the word `Board`.
After this we may then define *board equations*, which are the expressions that specify which parts of the board should be defined as which values.

To create a board equation we must first write the name we chose for the board state, immediately followed by an `!` followed by parenthesis that contain the position values for which part of the board is being defined.
Following the parenthesis is an expression that should evaluate to the same type that the board is made up of.
The board equation(s) must define a value for each part of the board.
If you leave a part of the board undefined, you will get an error.

Below is the code for one of the simplest boards we can make, which is a 1 by 1 board that holds a Bool. 
{% highlight haskell %}
type Board = Array(1, 1) of Bool -- Board definition

-- Board state
boardState : Board
boardState!(1,1) = True -- Board equation defining the value for position (1, 1)
{% endhighlight %}

Below is the code for a 1 by 2 board that holds Bool values. 
{% highlight haskell %}
type Board = Array(1, 1) of Bool -- Board definition

-- Board state
boardState : Board
boardState!(1,1) = True  -- Board equation defining the value for position (1, 1)
boardState!(1,2) = False -- Board equation defining the value for position (1, 2)
{% endhighlight %}

### Generalizing a Board Equation

If we wanted to initialize a Tic-tac-toe board with `Unmarked` values, we could do something like this:
{% highlight haskell %}
-- Initial board state
initialTTTBoard : Board
initialTTTBoard!(1,1) = Unmarked
initialTTTBoard!(1,2) = Unmarked
initialTTTBoard!(1,3) = Unmarked
initialTTTBoard!(2,1) = Unmarked
initialTTTBoard!(2,2) = Unmarked
initialTTTBoard!(2,3) = Unmarked
initialTTTBoard!(3,1) = Unmarked
initialTTTBoard!(3,2) = Unmarked
initialTTTBoard!(3,3) = Unmarked
{% endhighlight %}

In the above value definition we specify the initial value (Unmarked) for each part of our board. Since a Tic-tac-toe board is 3 by 3, there are 9 total board positions we need to define values for (hence the 9 board equations).
This is many lines of code.
In this instance, since we are making each position on the board the same initial value, there is no real reason we should have to write 9 equations.

We can write this same initialization by generalizing a board equation to refer to all position values rather than to a specific one.
To create a board equation that refers to all board positions, we will write a board equation that has non-integer (lowercase) names instead of integers for the position values. This will tell the equation to refer to all board positions rather than just one. The example code shown below does the same thing as the code shown above (but in less lines)!

{% highlight haskell %}
-- Initial board state
initialTTTBoard : Board
initialTTTBoard!(x,y) = Unmarked -- Board equation defining the values for all positions on the board 
{% endhighlight %}



## Built-in Board Functions

### Place

### InARow

### CountBoard

