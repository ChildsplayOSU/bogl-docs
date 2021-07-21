---
sort: 4 # Order in the sidebar
permalink: /technical/
---

# Technical Information

This chapter contains technical information about the implementation of BoGL. It focuses on the language, the website, the server, and all the related technologies necessary to connect these parts together.

This is intended for Haskell and/or Web developers that will be working on BoGL. It takes a more technical approach to describing the implementation of BoGL and the technologies involved. If you need to know more about the language itself and how to work with it, please refer to standard [tutorials](/tutorials/) instead.

## Overview

The Board Game Language (BoGL) is implemented as a full-stack web application. This means BoGL is served over the internet through a front-end (a website), but uses a back-end (a language server) behind the scenes to actually do the work of evaluating expressions using a given BoGL program.

![Diagram showing how the back-end (language server) and the front-end (website) work together.](../imgs/h1.jpeg "Diagram showing how the back-end (language server) and the front-end (website) work together.")

An example would be to evaluate the expression `x + y` using the following BoGL program.

```haskell
game Example

x : Int
x = 24

y : Int
y = 12
```

You could describe the same diagram from above using this program and expression like so.

![Diagram showing how the back-end (language server) and the front-end (website) work together for a specific program & expression.](../imgs/h2.jpeg "Diagram showing how the back-end (language server) and the front-end (website) work together for a specific program & expression.")

The website contains an editor that allows writing in the given program, as well as an area to enter an expression. When this expression is finished, both the program and the expression are sent to the backend to compute the result of evaluating said expression. *Every* request sends a new program and expression to the backend because the server does not remember information across requests, it is effectively stateless. This offloads the responsibility for maintaining state to the front-end, and allows multiple front-ends to talk with the same back-end simultaneously without mixing up their results. This allows us to have various different types of BoGL REPLs, such as the [standalone mini-repl](/tutorials/expressions.html) that exists in the BoGL tutorials. Other applications can be built to leverage the language server to the same effect, so long as the server itself is capable of handling the volume of incoming requests.

Not all expressions that are evaluated produce values. Some expressions produce syntax, type, or runtime errors. In addition, not all programs may be valid either, and may produce syntax or type errors before evaluating an expression. If there is a syntax or type error in a program, it was always be displayed first before checking the expression. This is due to the fact that expressions are evaluated in the context of a program, and so they remain unevaluated until a program has been successfully parsed and type-checked without errors.
