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
Semantic errors, also commonly referred to as logic errors, refer to issues with how your code runs and the logic of what your code is doing.
These kinds of bugs will not prevent your program from running, at least not initially, but can cause unexpected behavior and potentially break your program.

## Preventing Bugs
With good programming practices, the amount of bugs you produce can be decreased.

### :telescope: Planning Ahead

> "Weeks of coding can save hours of planning." - Unknown

### :alembic: Testing as you Code

## Resolving Bugs

### :crossed_swords: Divide and Conquer

### :books: Strategic Research

<details>
 <summary>Click to see solutions :eyes:</summary>

content goes here

</details>

:dart: **Excercise:**  
