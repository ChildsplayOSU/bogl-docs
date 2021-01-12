---
sort: 12 # Order in the sidebar
---

# Testing and Debugging

This guide is here to give advice on strategies one might use to prevent and resolve issues with their programs.
BoGL programs and bugs are used as examples in this guide, but the techniques and strategies discussed can be used in other contexts as well.

## Background: What is a Software Bug?
The term *bug*, in the fields of software developement and computer science, is a term that is commonly used to describe an issue or problem with a program. An example of this could be the program not working the way you expected (i.e. a function returning x when it should return y). It could also be that the code just doesn't work at all due to something being undefined or an instruction being written incorrectly. There are several ways to classify bugs. In this tutorial we will separate bugs into two categories: *Language errors* and *runtime errors*.

### Language Errors
Before you code is allowed to run, the interpreter will examine it. During this examination the interpreter will try to detect any *syntax* errors and even some *semantic* errors. We will refer to these errors, that were caught by the interpreter, as *language errors*.

The BoGL language has many rules that determine what is and isn't BoGL code. These rules, as a whole, are refered to as BoGL's *syntax*. *Syntax* can be thought of as the rules that determine how a language is structured.

**Examples of BoGL syntax rules:**
- Programs must start with a `game` definition.
- Function and value name definitions must start with a lowercase letter.
- Type name definitions must start with an uppercase letter.
- Text that is commented will not be treated as code.
- The defining expression of a function must evaluate to the function's defined return value.
- A function cannot have an undefined type in it's definition.

**Examples of English syntax rules:**
- The first letter of a sentence must start with a capital letter.
- A proper noun must start with a capital letter.
- A sentence must end with a question mark, exclamation mark, or period.

If your code breaks a BoGL syntax rule, the interpreter will prevent your code from runnning and return an error.

The interpreter can also detect some semantic (meaning) errors.
These are not syntax errors, but would cause problems if they were allowed to occur.
An example of this is the expression `False + False`. There is nothing in the BoGL syntax that prevents you from writing this, but in practice this expression does not make any sense (It is unclear what this expression would evaluate to; There is no defined meaning) so the interpreter will detect and prevent it.

It is important to note that not all semantic errors are detected by the interpreter before you run your code. An example of this is the expression `1 / 0`. This is also a valid expression according to the BoGL syntax, but there is no defined meaning for it (the result of dividing by zero is undefined in mathematics). The BoGL interpreter does not detect this error before running the code, so it will break a program at the time it gets evaluated during *runtime*.

### Runtime Errors
Runtime errors are errors that occur in the program while it is running, or in other words, errors that were not detected by the interpreter before program runtime.
These could be pieces of logic within your program that don't make sense or cause desired behavior. A common term used for these kinds of issues are *logic errors*.
These kind of issues are usually much harder to detect because there is oftentimes no error message.

<br/>
## Preventing Bugs
With good programming practices, the amount of bugs you produce can be decreased.
Planning ahead and testing as you code are good practices that will help reduce the amount of time you spend trying to find and resolve bugs.

### :telescope: Planning Ahead

> "Weeks of coding can save hours of planning." - Unknown

It is generally a good idea to plan out your program before trying to implement it in code.
Even just a little planning can drastically reduce the amount of time you spend on fixing bugs.
This section goes over some planning steps that you can take before you start coding.

*These steps are adapted from George Pólya's [problem solving principles](https://en.wikipedia.org/wiki/How_to_Solve_It).*

**Understand the problem.**  
It is important to make sure that you understand the problem best you can before attempting to solve it. One method you can use to think more deeply about a problem is to ask yourself questions about it. These might include:
- What are the ways in which I can restate the problem?
- What knowledge do I already have that may help me solve this?
- What knowledge don't I have which might help me solve this?
- What is gained by solving this problem?

**Devise a plan.**  
Once you understand the problem, you can then try to solve it.
It need not be with code though, at least not to begin with.
While coding you can often introduce many errors if you do not have a clear idea of what you are attempting to do.
Creating a solution in the form of pseudocode or a flowchart can help you find issues before you get to the coding step.

**Design tests or evaluation criteria.**  
It is a good idea to create tests or some other evaluation criteria that you can use to assess your solution.
This could be in the form of a *testing table* (see failsafe division example below) or list of testable behaviors that the program will be expected to follow.

### :alembic: Testing as you Code

**Frequently test your code.**  
Whenever you write a *unit* of code that can be tested, test it! All functions in BoGL are testable, meaning that after you define it in the editor you can call it in the interpreter. After you write a function, try calling it. Does it run? Does it return the value you expected? Try giving it different arguments. It is incredibly useful to find these bugs sooner than later.

More complicated functions may call upon other functions, meaning that a function could potentially break due to a bug that is located in a different function.
This can be difficult to debug, but it is easy to prevent by testing your functions before encorporating them.

If you find that the first functions you define are ones that call upon other functions, it may be best to leave placeholder code and a comment that references the functions that this one will be calling.
You can come back to these functions after you have defined and tested the other functions that it is composed of.
In BoGL it is best to first define and test functions that are independent of other functions.

**Example: Testing a Failsafe Division Function**  
If I were to create a calculator in BoGL, I might want to make a division function that would avoid runtime errors.
Here are some behaviors I would expect from such a function:
- If the user attempts to divide the numerator by zero, then the function will return the value "RestrictedCalculation".
- If the user attempts to give arguments that may be too big for BoGL to compute properly (we'll say over a quadrillion), the value returned will be "RestrictedCalculation".
- If the arguments are not greater than a quadrillion and the denominator is not 0, then the function will return the integer quotient of the arguments.

Here is what the testing table might look like for this function:

| Argument 1 (numerator) | Argument 2 (denominator) | Expected return value | Reasoning                                         |
|------------------------|--------------------------|-----------------------|---------------------------------------------------|
| 10                     | 2                        | 5                     | Valid integer division                            |
| 8                      | 4                        | 2                     | Valid integer division                            |
| 50                     | 30                       | 1                     | Valid integer division (quotient is rounded down) |
| 60                     | 0                        | RestrictedCalculation | Cannot divide by zero                             |
| 1000000000000001       | 1                        | RestrictedCalculation | Numerator argument is above the allowed threshold |
| 1  					 | 1000000000000001         | RestrictedCalculation | Denominator argument is above the allowed threshold |

:dart: **Excercise:**  
With the above information kept in mind, try writing a failsafe division function called "failsafeDivide" in the editor below.
If you click the **Check** button, the tests shown in the testing table will be run.

{% include exercise_module_template.html
content = "game FailsafeDivision

type MaybeInt = Int & {RestrictedCalculation}

failsafeDivide : (Int, Int) -> MaybeInt
failsafeDivide(n, d) = -- WRITE DEFINING EXPRESSION HERE
"

checks="failsafeDivide(10, 2)
failsafeDivide(8, 4)
failsafeDivide(50, 30)
failsafeDivide(60, 0)
failsafeDivide(1000000000000001, 1)
failsafeDivide(1, 1000000000000001)"

expects="5
2
1
RestrictedCalculation
RestrictedCalculation
RestrictedCalculation"
%}

<details><summary>:eyes: Click to see a solution (but try yourself first!)</summary>
<p>

{% highlight haskell %}
game FailsafeDivision

type MaybeInt = Int & {RestrictedCalculation}

failsafeDivide : (Int, Int) -> MaybeInt
failsafeDivide(n, d) = if d == 0 then RestrictedCalculation
                       else if n > 1000000000000000 then RestrictedCalculation
                       else if d > 1000000000000000 then RestrictedCalculation
                       else n / d
{% endhighlight %}

</p>
</details>



<br/>
## Resolving Bugs

Bugs happen, but there are ways to fix them.
This section will go over a few methods that can be used when trying to resolve a bug.

### :bulb: Check your Understanding
**Before anything else, ask yourself questions.**  
Before you go searching for the solution to your problem, first try to understand how and why it is occuring.
Here are a few questions you can ask yourself when attempting to understand a bug:

Questions for language errors:
- Which terms in the error message am I unfamiliar with?
- Does the logic of the error message make sense?
- Where in the program code is the error message referring to?
- Does the code that comes before the place of error look error-free?

Questions for runtime errors:
- What have I changed/added since I last tested my code?
- How do I expect my program to behave, and in what ways does its current behavior differ?
- If I give my functions specific inputs, do I get the outputs I expect?

Asking yourself questions about your issue can be useful in a multitude of ways.
First, by asking yourself questions you may wind up finding the solution on your own.
Second, by allowing yourself time to understand exactly what you don't know, you will be better able to ask intelligent and focused questions.
You may be able to paraphrase the issue in multiple ways, allowing you to obtain answers that are more relevant.
Going through the excercise of asking yourself questions will also help you learn and retain information about the issue, so that you may be able to better recall and apply it when encountering similiar bugs in the future.

### :crossed_swords: Divide and Conquer
If you have a bug, and you aren't sure which part of your program is causing the issue, try breaking your program apart and testing out individual pieces of it!  

If you have a runtime error, try calling all of your program's functions individually to see if they return expected outputs with the arguments you give them.
You can start with the functions that you think seem the most related to the issue.
Once you have found which function is behaving strangely, you can try running the expressions that are contained in the function seperately in the interpreter.
Similiar to testing the functions, see if the expressions you run in the interpreter evaluate to what you expect them to.
Following this process, you will eventually find something that may not be working in the same way you expected it to.

You can follow a similiar process with language errors.
If you have a language error, try commenting out the parts of your code that prevent your program from running.
You can do this incrementally by repeatedly commenting out the function in which the issue takes place and running the program.
Once the program runs, try running individual expressions in the interpreter that are from the last function you commented out.
Look for expressions that cause issues or evaluate to values you did not expect.

### :books: Strategic Research
If you are attempting something that you haven't before, and encounter an error message or issue that you are not familiar with and don't understand, your best option may be to seek out resources that can help. Before seeking out resources, be sure to first check your understanding and ask yourself questions. This will help you come up with better questions you will be able to ask and use to search for information.

**Humans are generally pretty good at understanding other humans.**  
If you know someone that may be knowlegable about the issue you are having, and that person is willing and able to help out, then asking them questions may be one of the best ways to get information related to your issue.
Presenting your bug to another person will force you to explain your problem and ask questions, which is why people will oftentimes come up with a solution themselves mid-explanation.

**If you know what you don't know, take time to know it.**   
If you encounter a bug while working with a command, tool, or concept that you don't entirely understand, take time to review documentation on how it works.
Learning through trail and error isn't a bad thing, but it oftentimes leaves gaps in understanding that will result in more bugs in the future.
Many documentation and tutorial websites have a handy search feature (including this one), which can allow you to quickly find information about a topic you wish to learn more about.

**Search online with the intent to learn.**  
The unfortunate truth is that you can often resolve bugs in your program without understanding what went wrong, and how you fixed it.
On the internet, there is an unccountable amount of answers to an uncountable amount of questions.
It is incredibly easy to search, find, and implement a solution for a bug without learning why it occured in the first place and how the solution works.
Before trying to search for a solution to your issue online, try to come up with a solution on your own.
Try using strategies mentioned earlier.
When searching online for a solution to a bug, try to understand what is being said about the underlying issue. Why is it occuring? How does the proposed solution fix it?
You will learn less if you do not first try to come up with your own solution for an error.
If you, in addition, implement a solution without trying to understand how it works, you will learn nothing.
