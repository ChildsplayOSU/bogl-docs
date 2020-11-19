---
sort: 1 # Order in the sidebar
#permalink: /tutorials/basics
---

# BoGL Basics
Welcome to BoGL, the Board Game Language! These tutorials will teach you the tools you'll need in order to get started with creating your own programs using this game oriented language.

## Defining your Game
Since BoGL is a game themed language, every BoGL program must begin with a game name. You can choose anything for this as long as it is a valid string (no weird characters), starts with a capital letter, and is preceded by the keyword `game`. Below is an example of the simplest program you can make in BoGL.
{% highlight haskell %}
game SimplestProgram
{% endhighlight %}

## Running your Code
BoGL code can be created and executed using a BoGL interface. The main interface can be found by following the link listed below. 

[:link: Link to main interpreter ](https://bogl.engr.oregonstate.edu/)

There are also smaller BoGL interfaces that can be found in these tutorial pages, like the one shown below. 

{% include code_module_template.html
content = "game SimplestProgram
"
%}
BoGL interfaces are comprised of two main parts:
- The *editor* (multi-line textbox on the left)
- The *interpreter* (single-line input box on the bottom right)  

The *editor* is for writing BoGL program code.   
The *interpreter* is for running BoGL expressions.

The simplest explanation for what an *expression* is in BoGL, is code that will evaluate to some value. The interpreter will take expressions and return what they evaluate to.
When running expressions in the interpreter, BoGL will first process everything written in the editor. If there is an error with the code written in the editor, an error message will be returned by the interpreter instead of a value.

:dart: **Excercise:**
1. Type the simple expression `2 + 2` into the interpreter of the interface above and press the **Enter** key. What gets returned?
2. In the editor, change the lowercase letter 'g' in the word `game` to an uppercase letter 'G'. What happens now when you enter `2 + 2` into the interpreter?

## Comments
Sometimes it can be useful to include comments within your code. Anything written after a double dash `--` on a line will be interpreted as comment text, meaning that the interpreter will not interpret that text as BoGL code.
Text can also be marked as comments if it is enclosed by curly bracket-dashes `{- comment text -}`.

{% highlight haskell %}
-- Anything after double dashes is comment text
game SimplestProgram -- even if code is on the same line.
{-
Comments can be
on multiple lines
if they are enclosed inside
of curly bracket-dashes
-}
{% endhighlight %}
