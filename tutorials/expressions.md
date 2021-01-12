---
sort: 5 # Order in the sidebar
---

# Understanding Expressions

An *expression* is something that must be evaluated in order to determine its value. An expression in BoGL can consist of [values](values), [operators](expressions#arithmetic-operators), [functions](./functions), [if/else statements](./conditional_statements), [local value definitions](./lets), and [loops](./loops) that together evaluate to some value. Not knowing what all of those things are is okay, it is still a good idea to get an early start on understanding the concept of an expression before completely comprehending all that it can be. Let's look at an example to illustrate the idea of an expression.

{% highlight haskell %}
2 + 3 - 4
{% endhighlight %}

The expression above consists of values (`2`, `3`, `4`) and operators (`+`, `-`). The resulting value is **1** when this expression is evaluated.

Expressions in BoGL are usually found inside of [value](./values) and [function](./functions) definitions, however, you may still evaluate one by typing it directly into the interpreter. This is useful for experimentation and practice. Try typing the expression `2 + 3 - 4` into the interpreter. It should return 1.

{% include code_module_template.html
content = "game ExpressionsDemo
-- Do not put code here.
-- Type your expression in the interpreter to the right and press enter.
"%}

Lets look at some more examples!

{% highlight haskell %}
not(True)
{% endhighlight %}

The expression above consists of a built-in function `not` and a value `True`. We may not know what this function does yet, but we do know that it will evaluate to some value. Try entering this expression into the interpreter to see the resulting value.

{% include code_module_template.html
content = "game ExpressionsDemo
-- Do not put code here.
-- Type your expression in the interpreter to the right and press enter.
"%}

An expression can be passed as an argument to a function as long as it evaluates to the function's parameter type. We saw in the example above that the function `not` takes a **Bool** parameter and returns a **Bool**. Try and see what happens when you enter the expression `not(not(True))` into the interpreter.

The order in which parts of an expression evaluate first can be very consequential to the resulting value.
We can have some control over which parts of an expression are evaluated first by using parenthesis `()`.
{% highlight haskell %}
12 / 4 / 2
{% endhighlight %}
The expression above currently evaluates to **1**. It does this by evaluating operations in the following order:

First operation: `12 / 4`, resulting in **3**

Second operation: `3 / 2`, resulting in **1**

If we instead wanted the expression to evaluate `4 / 2` first, we can wrap it in parenthesis.

{% highlight haskell %}
12 / (4 / 2)
{% endhighlight %}


Something that we have been using in these expression examples are *operators*. The arithmetic operators (+, -, /, \*) are fairly intuitve if you know basic arithmetic. There also exist other operators in BoGL that are not necessarily intuitive. Learning these operators and practicing by writing expressions with them will make it easier to work with more complicated expressions, like [conditional expressions](conditional_statements) and [loops](loops), which we will cover in further tutorials.

<br/>
## Arithmetic Operators
Expressions will often contain arithmetic logic (addition, multiplication, etc...). The BoGL language provides basic operators that can be used with **Int** values. The arithmetic operators in BoGL are *binary operators* because they have two *operands*. *Operands* are the values/expressions on each side of the operator.

| Operator       | Symbol | Example Expression | Example's Evaluation |
|----------------|--------|--------------------|----------------------|
| Addition       | +      | 2 + 2              | 4                    |
| Subtraction    | -      | 10 - 3             | 7                    |
| Multiplication | *      | 2 * 5              | 10                   |
| Division       | /      | 12 / 4             | 3                    |

:warning: **Note about integer division**

Since integers cannot be fractional values, the result of a division in BoGL will always be rounded down.

<br/>
## Relational Operators
Relational operators always evaluate to a **Bool**. They are commonly used as conditions for [conditional expressions](conditional_statements) and [loops](loops). You can think of these operators as evaluating a *relationship* between two values. For example, the relational operator `==` will check to see whether the operands are equal to eachother. If the operands are equal, then the expression will evaluate to **True**, otherwise it will evaluate to **False**. This operator is evaluating whether a relationship of equivalence exists between the two operands.

| Integer Specific Relational Operator  | Symbol | Example Expression | Example's Evaluation |
|---------------------------------------|--------|--------------------|----------------------|
| Equal to                              | ==     | 5 == 5             | True                 |
| Not equal to                          | /=     | 5 != 5             | False                |

:warning: The relational operators in the table below can only be used with **Int** operands.

| Integer Specific Relational Operator  | Symbol | Example Expression | Example's Evaluation |
|---------------------------------------|--------|--------------------|----------------------|
| Greater than                          | >      | 10 > 1             | True                 |
| Less than                             | <      | 10 < 1             | False                |
| Greater than or equal to              | <=     | 5 <= 5             | True                 |
| Less than or equal to                 | >=     | 4 >= 5             | False                |

<br/>
## Logical Operators
Logical operators are similiar to relational operators in that they always evaluate to a **Bool**. Where logical operators differ is that they can *only* be used on operands that evaluate to **Bool**. These operators can be used to combine two expressions or invert one. There are three logical operators in BoGL, and they are technically implemented as built-in [functions](functions). The parameter and return types for these functions are type **Bool**.

:exclamation: The word *expr* in the table below is short for *expression*.

| Logical Operator | Function             | Evaluation                                                                                                |
|------------------|----------------------|-----------------------------------------------------------------------------------------------------------|
| and              | and(*expr*, *expr*)  | True when both of the *expr* evaluate to True.<br>False when one or both of the *expr* evaluate to False. |
| or               | or(*expr*, *expr*)   | True when one or both of the *expr* evaluate to True.<br>False when both of the *expr* evaluate to False. |
| not              | not(*expr*)          | Negates *expr*. True when *expr* evaluates to False.<br>False when *expr* evaluates to true.              |
