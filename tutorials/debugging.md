---
sort: 11 # Order in the sidebar
# permalink: /tutorials/debugging
# published: false
---

# Testing and Debugging

:construction: Under construction :construction:

## Background: What is a Software Bug?
The term *bug*, in the fields of software developement and computer science, is a term that is commonly used to describe an issue or problem with a program. An example of this could be the program not working the way you expected (i.e. a function returning x when it should return y). It could also be that the code just doesn't work at all due to something being undefined or an instruction being written incorrectly. In general we can separate bugs into two separate categories: *Syntactic* errors and *semantic* errors. 

### Syntactic Errors
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

### Semantic Errors
*Semantic errors*, also commonly referred to as *logic errors*, refer to issues with how your code runs and the logic of what your code is doing.
These kinds of bugs will not prevent your program from running, at least not initially, but can cause unexpected behavior and potentially break your program.

## Preventing Bugs
With good programming practices, the amount of bugs you produce can be decreased.

### :telescope: Planning Ahead

> "Weeks of coding can save hours of planning." - Unknown

:construction: Under construction :construction:

### :alembic: Testing as you Code
:construction: Under construction :construction:

## Resolving Bugs
:construction: Under construction :construction:

### :bulb: Check your Understanding
**Before anything else, ask yourself questions.**  
Before you go searching for the solution to your problem, first try to understand how and why it is occuring.
Here are a few questions you can ask yourself when attempting to understand a bug:

Questions for Syntax Errors: 
- Which terms in the error message am I unfamiliar with?
- Does the logic of the error message make sense?
- Where in the program code is the error message referring to?
- Does the code that comes before the place of error look error-free? 

Questions for Semantic Errors:
- What have I changed/added since I last tested my code?
- How do I expect my program to behave, and in what ways does its current behavior differ?
- If I give my functions specific inputs, do I get the outputs I expect?

Asking yourself questions about your issue can be useful in a multitude of ways.
First, by asking yourself questions you may wind up finding the solution on your own.
Second, by allowing yourself time to understand exactly what you don't know, you will be better able to ask intelligent and focused questions. 
You may be able to paraphrase the issue in multiple ways, allowing you to obtain answers that are more relevant.
Going through the excercise of asking yourself questions will also help you learn and retain information about the issue, so that you may be able to better recall and apply it when encountering similiar bugs in the future.

### :crossed_swords: Divide and Conquer
:construction: Under construction :construction:

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
