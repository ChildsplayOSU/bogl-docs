---
sort: 5 # Order in the sidebar
#permalink: /tutorials/expressions
---
 
# Understanding Expressions

:construction: Under construction :construction:

An *expression* is something that must be evaluated in order to determine its value. An expression can consist of values, operators, [functions](./functions), [if/else statements](./conditional_logic), [loops](./loops), and other bits of logic that ultimately evaluate to some ultimate value. To illustrate this, lets look at some examples.

**2 + 3 - 4**

The expression above consists of values (2, 3, 4) and operators (+, -). The resulting value is **1** when this expression is evaluated.

Expressions in BoGL are usually found inside of [value](./values) and [function](./functions) definitions, however, you may still evaluate one by typing it directly into the interpreter. Try typing the expression `2 + 3 - 4` into the interpreter. It should return 1.

{% include code_module_template.html 
content = "game ExpressionsDemo
-- Do not put code here.
-- Type your expression in the interpreter to the right and press enter.
"%}
