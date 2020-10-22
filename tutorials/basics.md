---
sort: 1 # Order in the sidebar
#permalink: /tutorials/types
---
 
# BoGL Basics
Welcome to BoGL, the Board Game Language! These tutorials will teach you the tools you'll need in order to get started with creating your own programs using this game oriented language.

## Defining your Game
Since BoGL is a game themed language, every BoGL program must begin with a game name. You can choose anything for this as long as it is a valid string (no weird characters), starts with a capital letter, and is preceeded by the keyword `Game`. Below is an example of the simplest program you can make in BoGL.
{% include code_module_template.html 
content = "
game SimplestProgram <br/>
"
%}

## Comments
Sometimes it can be useful to include comments within your code. Anything written after a double dash `--` on a line will be interpreted as comment text, meaning that the interpreter will not interpret that text as BoGL code.
Text can also be marked as comments if it is enclosed by curly bracket-dashes `{- comment text -}`.

{% include code_module_template.html 
content = "
-- Anything after double dashes is comment text<br/>
game SimplestProgram -- even if code is on the same line.<br/>
{-<br/>
    Comments can be<br/>
    on multiple lines<br/>
	if they are enclosed inside<br/>
    of curly bracket-dashes<br/>
-}<br/>
"
%}
