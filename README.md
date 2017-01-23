# nanopass-haskell-compiler
Compiler for Haskell using the idea of many simple passes

We will use a subset of Haskell with no modules, no foreign functions, no comments, and no indentation.  This is to simplify the project.  In the future, a pass which will strip out comments, and a pass which will convert the indented form of code to the non-indented form will be added. Adding in modules and foreign functions may be more difficult.

# Syntax
*program* -> { *lexeme* | *whitespace* }
*whitespace* -> *whitestuff* { *whitestuff* }
*whitestuff* -> any whitespace character (newline, space, tab, etc.)
*lexeme* ->
