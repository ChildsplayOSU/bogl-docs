---
sort: 8 # Order in the sidebar
#permalink: /tutorials/loops
---

# Locally Defined Values

:construction: Under construction :construction:

In the [values](values) tutorial we learned how to create values for use in BoGL programs.

For a quick recap, say I wanted to create a value that represented the length of a game board (in squares).
I may want a value that holds the length so that I can use it in multiple parts of my program without needing to remember the represented value every time I need to use it. 

We could use [Chess](https://en.wikipedia.org/wiki/Chess) as an example. The board in Chess has a length of 8 squares.
I could define a value in BoGL to represent the length of a Chess board like so:

{% highlight haskell %}
boardLength : Int
boardLength = 8
{% endhighlight %}

I could then use this value in other parts of my program. 

{% highlight haskell %}
totalSquares : Int
totalSquares = boardLength * boardLength
{% endhighlight %}

Thats fine and all, but what if I just need a value to use in just a single expression rather than in an entire program?
This is where *locally defined values* can come in handy.
A locally defined value is a value that is only to be used in a single specified expression. Lets look at an example of this idea.

Say we wanted to decrease the amount of letters we had to write out in this nonsensical sentence: 

*The incomprehensibilities of the situation are getting out of hand, and it is to the point where these incomprehensibilities are adding more incomprehensibilities to the incomprehensibilities that I perceive as incomprehensibilities.*

We could define a symbol to represent the word with the most characters:

**Let the symbol :information_source: be the word "incomprehensibilities" in the sentence**  
*"The :information_source: of the situation are getting out of hand, and it is to the point where these :information_source: are adding more :information_source: to the :information_source: that I perceive as :information_source:."*

Since I am specifying the representation of :information_source: for just a single sentence, I could potentially reuse it as a representation for a different word in a different sentence later on.

**Let the symbol :information_source: be the word "carnivore" in the sentence**  
*"The :information_source: of a :information_source: will eat a :information_source: when it is hungry because it is a :information_source:."*


*Let expressions* are useful in BoGL when we need to refer to a specific expression/value multiple times within another specific expression.

![let statement anatomy](/imgs/lets-let-statement-anatomy.jpg)

You can write a let expression by first writing the key word `let` followed by the desired name of the value (must start with a lowercase letter), followed by an equals sign `=`. After the equals sign is where the expression of the locally defined value is defined. After this expression goes the keyword `in`, following this keyword is the expression that the locally defined value will be used in.

**Example:**

{% highlight haskell %}
game LetEx

y : Int
y = let x = 10 in
    x / 5
{% endhighlight %}

**Example:**

{% highlight haskell %}
game LetEx

x : Int
x = let a = 1 in
    let b = 2 in
    let c = 3 in
    a + b + c
{% endhighlight %}
