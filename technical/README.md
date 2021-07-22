---
sort: 4 # Order in the sidebar
permalink: /technical/
---

# Technical Information

This chapter contains technical information about the implementation of BoGL. It focuses on the language, the website, the server, and all the related technologies necessary to connect these parts together.

These technical documents are intended for Haskell and/or Web developers that will be working on BoGL. They take a more in-depth approach to describing the implementation of BoGL and the technologies involved. If you need to know more about the language itself and how to work with it, please refer to standard [tutorials](/tutorials/) instead.

## Overview

The Board Game Language (BoGL) is implemented as a full-stack web application. This means BoGL is served over the internet through a front-end (a website), and uses a back-end (a language server) behind the scenes to actually do the work of evaluating BoGL expressions using a given BoGL program.

![Diagram showing how the back-end (language server) and the front-end (website) work together.](../imgs/h1.jpeg "Diagram showing how the back-end (language server) and the front-end (website) work together.")

This can be demonstrating by showing, at a high-level, how BoGL evaluates the expression `x + y` using the following program.

```haskell
game Example

x : Int
x = 24

y : Int
y = 12
```

Using the diagram from above, we can show how BoGL usies this program and expression to produce a final value.

![Diagram showing how the back-end (language server) and the front-end (website) work together for a specific program & expression.](../imgs/h2.jpeg "Diagram showing how the back-end (language server) and the front-end (website) work together for a specific program & expression.")

In practice, you would be writing this program and the expression into the BoGL website. To do this, the website contains an editor that allows writing in the given program, as well as an area to enter an expression. When this expression is finished evaluating (or runs into an error or prompt), both the program and the expression are sent to the backend to compute the result of evaluating said expression.

Each request sends a new program and expression to the backend. The server does not remember or cache information across requests, making it stateless. This offloads the responsibility for maintaining state onto the front-end, and allows multiple front-ends to talk with the same back-end simultaneously without mixing up their results. This allows us to have various different types of BoGL REPLs, such as the [standalone mini-repl](/tutorials/expressions.html) that exists in the BoGL tutorials. Other applications can be built to leverage the language server to the same effect, so long as the server itself is capable of handling the volume of incoming requests. It goes without saying there are physical limits to the volume of requests that a single server can take, but for our use cases this is sufficient.

It was mentioned briefly above, but not all expressions will produce final values. For example, some expressions produce syntax, type, or runtime errors. In addition, not all programs may be valid either, and may produce syntax or type errors before evaluating an expression. If there is a syntax or type error in a program, it is always displayed before checking the expression. This is due to the fact that expressions are evaluated in the context of a program, and so they remain unevaluated until a program has been successfully parsed and type-checked without errors.
