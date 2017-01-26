# nanopass-haskell-compiler
Compiler for Haskell using the idea of many simple passes

We will use a subset of Haskell with no modules, no foreign functions, no comments, and no indentation.  This is to simplify the project.  In the future, a pass which will strip out comments, and a pass which will convert the indented form of code to the non-indented form will be added. Adding in modules and foreign functions may be more difficult.

# Lexical Syntax
* *program* -> { *lexeme* | *whitespace* }
* *whitespace* -> *whitestuff* { *whitestuff* }
* *whitestuff* -> any whitespace character (newline, space, tab, etc.)
* *lexeme* -> *varid* | *conid* | *varsym* | *consym* | *literal* | *special* | *reservedop* | *reservedid*
* *literal* -> *integer* | *float* | *char* | *string*
* *special* -> ( | ) | , | ; | [ | ] | ` | { | }
* *tyvar* -> *varid* (type variables)
* *tycon* -> *conid* (type constructors)
* *tycls* -> *conid* (type classes)
* *varid* -> *small* { *small* | *large* | *digit* | ' } not *reservedid* (variables)
* *conid* -> *large* { *small* | *large* | *digit* | ' } (constructors)
* *reservedid* -> case | class | data | default | deriving | do | else | if | in | infix | infixl | infixr | instance | let | newtype | of | then | type | where | _
* *varsym* -> *symbol*_(:) { *symbol* } not *reservedop*
* *consym* -> : { *symbol* } not *reservedop*
* *reservedop* -> .. | : | :: | = | \ | | | <- | -> | @ | ~ | =>
* *float* -> *decimal* . *decimal* [*exponent*]
* *exponent* -> (e | E) [+ | -] *decimal*
* *integer* -> *decimal*
* *decimal* -> *digit* { *digit* }
* *char* -> '*graphic*_('|\) | *space* | *escape*_(\&)'
* *string* -> "{*graphic*_("|\) | *space* | *escape* |}"
* *escape* -> \*charesc* | *decimal*
* *charesc* -> a | b | f | n | r | t | v | \ | " | ' | &
* *graphic* -> *small* | *large* | *symbol* | *digit* | *special* | " | '
* *small* -> lowercase characters
* *large* -> uppercase characters
* *space* -> a space
* *digit* -> digits

# Basic Idea
The compiler will consist of many small passes over the code. Each pass will make small changes.
1. Lexer, breaks code into lexical units
2. Parser, converts stream of lexical units into tree
3. Other passes
