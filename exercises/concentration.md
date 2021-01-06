---
sort: 1 # Order in the sidebar
permalink: /exercises/concentration
---

# Exercise: Concentration in 10 Steps

For this exercise, you will be implementing [Concentration](http://www.solitairecentral.com/rules/Concentration.html). This is a card game that involves matching cards of the same value.

Your version of concentration will use 4 cards, arranged as a 2x2 board, with the cards *face up*. In addition, you don't need to worry about shuffling your cards, as we're not trying to hide anything.

Cards will have 2 possible number values, `1` or `2`.

The game should end when all cards have been matched.

## Steps

1. Write up an algorithm to express the rules of the game. How do we know when we win? How do we know what cards we can try and match?

2. Using your algorithm, identify the **types** in the game of Concentration. Everything that you would need to express concepts in your algorithm is used here.
  - Keep in mind how you represent the idea of a card that has been matched.
  - Also think about the type of the information you need the user to ask for (i.e. how do you identify which cards to pick).
  - How do you express the idea of a matched card?

3. On a piece of paper, or somewhere on your computer, sketch our your types. You can use the existing types of `Int`, `Bool`.
  - Why do you need each type?

4. Looking back at your algorithm, write in an initial version of a board in [BoGL](https://bogl.engr.oregonstate.edu). We've included a snippet for you to use below.

5. Add a function that describes whether two **Card** values match or not.
  - Using the existing type of `Bool` would be helpful here.
  - The first part of your function might start like this: `matches : (...,...) -> ...`, where you have 3 spots to add the types you want to use (if you're not sure about the parentheses, check out [tuples](/tutorials/types.html#tuples)).
  - The second part of your function will start like this: `matches(card1,card2) = ...`, this is a bit of a hint.

6. Write a function that asks the user for 1 card, and picks it from the board.
  - There are two things that will help you here, [let](/tutorials/lets.html) and [input](/tutorials/input.html).
  - To get a card from a board, you can use `myBoard!(x,y)`, where x and y are the column and row of the card you want.

7. Take your function from (6), and extend it just a bit so that it asks for 2 cards, and returns both of them.
  - The same concepts from (6) will help, in addition to [tuples](/tutorials/types.html#tuples) again.

8. Write a function that takes a board, and tells whether there are any unmatched cards on it.
  - the sections on [relational operators](/tutorials/expressions.html#relational-operators) and [logical operators](/tutorials/expressions.html#logical-operators) will be helpful

9. Write a function that marks a card as matched on the board. This may vary based on what you sketched up before.

10. Combine these pieces together with a [loop](/tutorials/loop.html) that ends when there are no-unmatched cards on the board. This should be your final function, and you can call it `play`.

## Snippet

{% highlight haskell %}
game Concentration

-- ... your types can go here ...

type Board = Array(2,2) of ... -- decide what type is used to fill the board

-- a board of 4 spaces
-- based on what goes on the board, what should you put at each space?
myBoard : Board
myBoard!(1,1) = ...
myBoard!(1,2) = ...
myBoard!(2,1) = ...
myBoard!(2,2) = ...

-- ... your functions can go here ...
{% endhighlight %}

## Reflection

- Compare what you've done so far with your original algorithm. Is it similar to what you were thinking of, or is it different?

- Why do you think either is the case?

- What were some ideas that you thought of initially, but didn't end up using? Why?

- On the other hand, what were some ideas that you didn't think of initially, but ended up needing?
