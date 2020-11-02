---
sort: 7 # Order in the sidebar
---
 
# User Input

:construction: Under construction :construction:

To recieve input from the user of a program you may use the `input` statement.

Before using `input`, you must always define a type that the user's input values are expected to be. This is done by using the keyword `Input` in a type definition. See example below.

{% highlight haskell %}
type Input = Int -- User input is expected to be of type Int
{% endhighlight %}

Try typing `input` into the interpreter and running it.

{% include code_module_template.html 
content = "game InputDemo

type Input = Int
"
%}
