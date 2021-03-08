# Disclaimer

This language is but a **concept**. The Standard Library and Compiler and everything else will be released soon (perhaps a few years from now). I need time to work on it and get my college and uni settled. I wrote this document a few months ago.

# Eliph

**Eliph** is the language for folks who don't necessarily love JavaScript, but who still acknowledge its importance in the ecosystem.
It embraces the full feature set of JavaScript, and also extends it with new and improved features, so to improve the readability and brevity of traditional JavaScript code.

It compiles to the highest quality of clean, readable and performant JS, directly runnable in browsers and Node. This means you can pick up Eliph and access the vast JS ecosystem and tooling as if you've known it for a long time!

If you have an existing TypeScript or ReScript codebase, Eliph code can be compiled to both of these languages allowing you to slip it in any codebase almost unnoticed. The output preserves the general code structure, as all of the extra features that go along with Eliph is declared at the bottom of the file. Types would be inserted and inferred whenever necessary.

```coffee
query = select user.id from user
  where user.name == 'boom' && user.id == 1
    || user.name == 'bang' && user.id == 2
```

Eliph has:

- a syntax similar to Nim, Ruby, OCaml, LiveScript, CoffeeScript, Bash, Julia and Elixir;
- semantics, features and operators similar to F#, Crystal, Haskell, PureScript and Elm;
- functions and modules based mostly on JavaScript (NPM such as Lodash, Ramda, Math.JS and more), as well as core and community libraries from Python and Ruby.

## Why Eliph?

Eliph aims to be a more concise cousin to the JavaScript language by introducing new concepts, functions and symbols implemented in other programming languages, making it easier to write code with fewer characters and more "syntactic sugar". This would make code typically written in tens or hundreds of lines much more readable and compact and allows you to write expressive code without redundant or verbose boilerplate.

A necessary component of the language and its design has to do with its concise syntax: employing the right balance of words and symbols and minimizing the overuse of brackets and perhaps all the typable keys in the keyboard. So to simplify things, we do remove a number of things, although they really can be seen as optional.

[coffeescript]: https://coffeescript.org/
[wtfjs]: https://github.com/denysdovhan/wtfjs
[stdlib]: https://stdlib.io/
[npm packages]: https://medium.com/@thomasfuchs/what-if-we-had-a-great-standard-library-in-javascript-52692342ee3f

**_Lagom_**. We deem curly braces, semicolons and even commas as unnecessary. Sometimes that applies too for parentheses. The only times you would need them are when you want to cram things into a single line. Some of the more unnecessary things that really become a big hassle for developers like me, such as verbosity, word length and excessive use of punctuation, have been removed.

- **Shortened keyword and function names**: `function -> func`, `instanceof -> instof`, `extends -> from / of`, `implements -> with`
- **Unnecessary punctuation have been removed**, such as semicolons `;`, commas `,`, and parentheses `()` in statements like `if ()` and `for ()`.
- **Everything is an expression**, and can be assigned to variables and returned from functions, which includes control flow statements like `if`, `for` and `try`.
- **Optional declarations** with `var`, `let` or `const` are only allowed when initializing a variable without a value or one in a loop.
- **Implicit returns**: the last statement is automatically returned from a `do`-block (closure) or a function, unless otherwise specified with `return`.

**Static and robust**. JavaScript has a complete lack of types. It's also notorious for its [peculiar runtime behaviour][wtfjs], which can lead to unexpected and sometimes annoying side effects. TypeScript kind of _solves_ this, by adding static and inferred types to the language, but this doesn't change the fact that it inherits all of JavaScript's problems.

- Types in Eliph are **automatically inferred.** You don't need to explicitly assign a type to a variable. Use `any` or `dyn` to disable type-checking.
- You can annotate **anywhere** within your code, such as the types of variables and function parameters, object values, return types, and even within expressions, so you can assure yourself that you really know what you're doing.
- **A type should not change into another.** In JavaScript, your variable's type might change when the code runs, hence causing a wide range of side-effects.
- **A type system that is sometimes incorrect can be dangerous** due to expectation mismatches.
- **Types are erased after compilation** and don't exist at runtime. They are detected at compile time and will get reported in your IDE.

**Dependency-free**. Eliph aims to provide a suite of built-in classes, methods and functions from its source code on the fly, so there is no need for you to litter your code and ship your product with loads of utility functions and algorithms (unless you're tailoring your own for the job).

That's why we're trying to encode and consolidate these utility functions into a **standard library** (inspired by languages like Python, Ruby and Go). We feel we don't want to drag a lot of our dead code into our final codebase, when we can just take the ones we need.

- Eliph can be used directly on Node.JS and even has its own standalone library with no dependencies, `@eliph/stdlib`. The code is automatically formed or imported from the compiler.
- The standard library also can be used with virtually any language that compiles to javascript, allowing for smooth interop.

**One-to-one mapping**. Unreadable boilerplate JS code generated from other compiled-to-JS languages makes it so that it could be, practically speaking, hard to debug, hard to learn from and hard to integrate with existing JS.

For Eliph, we try to make sure that we preserve much of Eliph's syntax in the output, rather than try to cram boilerplate code in the middle of the output. This is especially important while learning, where users might want to understand how the code's compiled, and to audit for bugs.

- All **JS features** are preserved. Some mappings are less obvious, and may require some reordering of terms. This is all taken care by the compiler.
- **Comments** are always preserved in the final output, even within interpolated strings and block regular expressions.
- **Type annotations** are not "removed" from the output. Mainly, they exist as comments, if the compiled language does not have any types. They are distinguished separately from regular comments.
- **Built-in and standard functions** are generated as prototype methods and functions at the top of the file, along with any import statements.
- **Variables** with illegal identifier names, keyword names or variables that would eventually be deleted with `del`, are declared with an object at the top of its scope (if there are any) and accessed from that object.

---

## History of Eliph

Eliph first began as a side gig in early 2020 when I developed algorithms and programs in Python and JavaScript during my free time. However, as I've gotten used to programming in JavaScript, and previously developed a lot of programs in Python, but having to go over to Stack Overflow and manually searching for the exact functions in my code, which uses highly specialised Python functions and libraries unavailable and difficult to find in JS.

Also, the functions which JavaScript offers are often too difficult to understand and may usually require some further explanation to comprehend after looking at the documentation. As I grew deeply obsessed with programming in JS due to the idea that one can design and develop everything they imagine using only one language, this lead me to pursue a goal of creating a new language that blends the simplicity and ease of Python with the malleability of JavaScript, along with syntaxes and operations inspired by different programming languages.

Many programming languages and frameworks often have adequate language support in integrated development environments. Language support is a fancy term for things like code snippets, syntax highlighting, boilerplate, documentation, language references and even a big ecosystem of plugins, packages and Stack Overflow developers.

## Roadmap

- Documentation
- Standard library
- Syntax highlighting
- Compiler and Formatter
- Linter and debugger

### Documentation

The roadmap for developing the language has to start with the documentation, as that would give me a head start on the grammatical and syntactic features of the language. The documentation will be written with Markdown, which would explain the features, grammar, functions and modules in the language and its core library, and explain the similarities and differences between it and other programming languages.

### Syntax Highlighting

The next pattern is to do the syntax highlighting for the language. Syntax highlighting displays text, especially source code, in different colours and fonts according to the category of terms, while visually distinguishing structures and syntax errors.

Code is parsed through a series of regular expressions, and each match is assigned a scope. These scopes are mapped to colors in stylesheets and themes in code editors and syntax highlighting engines in code editors.

Highlighting can be fine-tuned through the use of custom code, such as highlighting bracket encapsulations or indentation depth, HTML/XML tags and attributes, variable, function or class names, or even allowing for including other languages inside the code.

---

# Table of Contents

[awesomejs]: https://github.com/sorrycc/awesome-javascript/
[awesomenode]: https://github.com/sindresorhus/awesome-nodejs
[awesomepy]: https://github.com/vinta/awesome-python

1. A Formal Introduction
2. The Basics
   1. Your First Program
   2. Code Structure
   3. Comments
   4. Keywords
   5. Embedding Raw Code
3. Variables
   1. `var`, `let`, `const`
   2. Shorthands
4. Constants and literals
   1. Basic data types
   2. `null` and `undef`
   3. Booleans `bool` and their operations
   4. Numbers
      1. Integers `int` and floating points `float`
      2. Arithmetic and bitwise operations
      3. Fractions `frac`
      4. Decimals `deci`
      5. Complex Numbers `comp`
   5. Strings `str` and characters `char`
      1. String Operations
      2. Templates
      3. Basic and Extended Slicing
   6. Regular Expressions
   7. Ranges, Sequences and Comprehensions
      1. Literals `[a<:b:c,d]`
      2. Array and Object Comprehensions
5. Data Structures
   1. Tuples `()` and Arrays `[]`
   2. Objects `{}` and Records `(| |)`
   3. Maps `{| |}` and Sets `[| |]`
   4. Weak Sets `#[]` and Maps `#{}`
   5. Destructuring assignment
6. Control Flow
   1. The `do` block, closures and `pass`
   2. Decision Making
      1. `if`, `elif`, `else`, `unless`, `elun`
      2. `guard-else`
   3. Loops
      1. Range, `for-in`, `for-of` and `for-from`
      2. `break` and `continue`
      3. `while` and `until`; `repeat-while` and `repeat-until`
      4. Infinite `loop`
   4. Switch
      1. Basic (conditional) `switch`
      2. Multiple cases and half-expressions
      3. `break` and `fallthru`
      4. Pattern matching
   5. Error handling
      1. `try-catch-finally`
      2. Multiple `catch` statements
   6. `label` and `goto`
7. Functions
   1. `func` declaration
   2. Recursion
   3. Generators
   4. First-class functions
   5. Composition
   6. Piping
   7. Currying
8. Types
   1. `any`, `void`, `unknown`, `other` and `never`
   2. Type aliases
   3. Literal types
   4. Unions and intersection types
   5. Interfaces
   6. `enum`
      1. Default
      2. Ranged Values
      3. Non-Numeric Values
9. Classes
   1. Constructors and instances
   2. Methods and attributes
   3. Inheritance and mixins
   4. Access modifiers
10. Modules
    1. Import and export
    2. Using NPM modules
    3. Namespaces

---

|## Overview of Features

This is an overview of most language features in Eliph. It does not explain them in detail, but should serve as a quick reference. Please see the guides on the left for additional details about each feature.

### Variables and Types

| Feature                        | Example                                               |
| ------------------------------ | ----------------------------------------------------- |
| Variable value `let`           | `count = 42`                                          |
| Constant value `const`         | `hi := "Hello World!"`                                |
| Non-local variable value `var` | `hi .= "Hello World"`                                 |
| Type annotation on binding     | `count: int = 42`                                     |
| Do-blocks                      | <pre>hi: str = do<br>&#x9;return 'Hello World!'</pre> |

### Primitive Types

| Feature                              | Example                                                                         |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| Integers: `int`                      | `x: int = 10`                                                                   |
| Floating-point number: `float`       | `x: float = 10.`                                                                |
| Fraction: `frac`, `real`\*           | `x: frac = frac(3, 10)`                                                         |
| Arbitrary precision number: `deci`\* | `x: deci = deci(Math.PI)`                                                       |
| Complex number: `comp`\*             | `x: comp = comp(1, 2)`                                                          |
| String: `str`                        | `x: str = "Hello world!"` `x: str = \hello + \world!`                           |
| Characters: `char`                   | `x: char = ?a`                                                                  |
| Units: `void`                        | `x: void = null`                                                                |
| Options:                             | `x: option<int> = 10`                                                           |
| Regular Expression: `regex`          | `x: regex = /\d+/g`                                                             |
| Tuples: `tuple`                      | `x: (int str) = (10 'ten')`                                                     |
| Frozen Set: `frozenset`              | <code>x: int %[\| \|] = %[\| 1 2 3 \|]</code>                                   |
| Frozen Map: `frozenmap`              | <code>x: %{\| [_: int]: int \|} = %{\| 1: 1, 2: 2, 3: 3 \|}</code>              |
| Record: `rec`                        | <code>x: (\| [_: str]: str \|) = (\| one: 1, two: 2, three: 3 \|)</code>        |
| Function: `func`                     | `x: (int int) -> int = (a, b) -> a + b`<br>`x = (a: int, b: int): int -> a + b` |

\* covered in advanced topics (coming soon)

### Data Structures

| Feature       | Example                                                          |
| ------------- | ---------------------------------------------------------------- |
| Array: `arr`  | `x: int[] = 1, 2, 3`                                             |
| Object: `obj` | `x: { [key: str]: str } = { key: 'val' }`                        |
| Set: `set`    | <code>x: int[\| \|] = [\| 1 2 3 \|]</code>                       |
| Map: `map`    | <code>x: {\| [_: int]: int \|} = {\| 1: 1, 2: 2, 3: 3 \|}</code> |

### Strings

| Feature                        | Example                                            |
| ------------------------------ | -------------------------------------------------- |
| String                         | `'hello world'` `"hello world"'` `\hello`          |
| Character                      | `?h` `?&amp;` `?\n` `?\x3f` `?u3004` `?\u{100001}` |
| Character at index             | `'hello'[2]` `'hello'.2`                           |
| String slicing                 | `'hello'[1,2]` `'hello'[1 2]` `'hello'[$>:0]`      |
| String splicing                | `'hello'[:<$='h']`                                 |
| String/character concatenation | `\hello + \world`                                  |
| String replacement             | `\hello - \l` `\hello - (\l \r)`                   |
| String repeating               | `'hello ' * 3`                                     |
| String splitting               | `'hello world' / ' '`                              |
| String formatting              | `'hello %s' % \world`                              |
| String length                  | `len 'Hello World!'`                               |

### Numbers

| Feature                  | pExample                                                             |
| ------------------------ | -------------------------------------------------------------------- |
| Integer                  | `30` `0_040` `-1e4` `1E4` `0x2E` `0xc3p0` `0b1001` `0o0040` `'150'6` |
| Floating-point number    | `0.1` `.1` `1.` `-1.e+4` `0x0.4p0` `'10.4'30`                        |
| Fraction\*               | `(1/3)f` `1f` `1.(3)f` `frac 1 3` `frac(1, 3)` `frac 1/3`            |
| Decimal\*                | `1m` `1.(3)m` `deci sqrt 3`                                          |
| Complex numbers\*        | `1+0j` `1j` `(1 1/3)j` `comp 1 0`                                    |
| Arithmetic               | `+` `-` `*` `/`                                                      |
| Floor (integer) division | `//`                                                                 |
| Exponent                 | `**`                                                                 |
| Bitwise operators        | `&` <code>\|</code> `^` `~` `~&` <code>~\|</code> `~^`               |
| Bitwise shift            | `>>` `<<` `>>>` `<<<`                                                |
| Bitwise rotation         | `>->` `<-<`                                                          |

\* covered in advanced topics (coming soon)

### Booleans and Logical Operators

| Feature                          | Example                                                    |
| -------------------------------- | ---------------------------------------------------------- |
| Alias for `true`                 | `true` `yes` `on`                                          |
| Alias for `false`                | `false` `no` `off`                                         |
| Comparison                       | `<` `>` `<=` `>=`                                          |
| Three-way comparison             | `<->`                                                      |
| Weak equality (JS `==`/`!=`)     | `=~` `!~`                                                  |
| Strong equality (JS `===`/`!==`) | `==` `!=`                                                  |
| Strict equality (JS `Object.is`) | `===` `!==`                                                |
| Logical operators                | `&&` <code>\|\|</code> `^^` `!` `!&` <code>!\|</code> `!^` |

### Ranges

| Operator         | Meaning                                |
| ---------------- | -------------------------------------- |
| `$`              | Length of the iterable                 |
| `a,b`            | `a` and `b` only                       |
| `,b,`            | implicit `0` -> `0,b,0`                |
| `a,b:c`          | `a`, then from `b` to `c` by `±1`      |
| `a::b`           | from `a` to `b`, including `a` and `b` |
| `a:>b` or `a:<b` | ... excluding `b` only                 |
| `a<:b` or `a>:b` | ... excluding `a` only                 |
| `a<>b` or `a><b` | ... excluding both `a` and `b`         |
| `a::b:c`         | ... inclusive, step by `c`             |
| `a::b:c:d`       | ... step by `c`, then `d`\*            |

In the last example mentioned above,

- Range alternates between adding `c` and `d` to `a`, until reaching/hitting `b`.
- Algebraically: `[a, a+c, a+c+d, a+2c+d, a+2c+2d, a+3c+2d, a+3c+3d ... b]`
- If the range counts **out of bounds**, it will coerce that to count in the right direction.
- So, if `c + d > 0 && a > b || c + d < 0 && a < b`, then all numbers following `a` and `b` will be negated: `c` would be `-c` and `d` would be `-d`.

### Decision Making

There is no ternary operator, you just have to use `if-else` as if they are expressions.

| Feature          | Example                                                                          |
| ---------------- | -------------------------------------------------------------------------------- |
| Keywords         | `if`<br>`else`<br>`elif` (else if)<br>`unless` (if not)<br>`eless` (else if not) |
| If blocks        | <pre>if a == true:<br>&#9;a = a + 3<br>else:<br>&#9;a</pre>                      |
| Postfix if       | `x = 3 if a`                                                                     |
| If expressions   | `if cond then a else b`<br>`cond if a else b`                                    |
| Guard statements | `guard cond else...`                                                             |

### Loops

There is no ternary operator, you just have to use `if-else` as if they are expressions.

| Feature                                           | Example                                                                                                                                |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Keywords                                          | `for`<br>`while`<br>`until` (while not)<br>`repeat...while` (do...while)<br>`repeat...until` (do...while not)<br>`repeat` (while true) |
| Numeric or character ranges (covered above)       | `for i in [1::10]`                                                                                                                     |
| Values and indexes in array/string                | `for value, index in array`                                                                                                            |
| Keys and values in object                         | `for key, value of object`                                                                                                             |
| ...with own properties                            | `for own key, value of object`                                                                                                         |
| Values from generator functions                   | `for value from gen_fn`                                                                                                                |
| Optional guard statement                          | `when cond` `lest cond`                                                                                                                |
| Break out of the loop entirely                    | `break if cond`                                                                                                                        |
| Stop current execution and continue with the next | `continue if cond`                                                                                                                     |
| Array comprehensions                              | `for x in 10 when x % 2 == 0`                                                                                                          |

### Pattern Matching

| Feature                                                            | Example                                    |
| ------------------------------------------------------------------ | ------------------------------------------ |
| Switch                                                             | `switch val`                               |
| Empty (conditional switch)                                         | `switch` &rightarrow; `switch true`        |
| Case statement<br>(<code>\|</code> is an alias for `case`)         | `case 3`<br>`case 3 =>`<br>`case 3:`       |
| Catch-all<br>(`_` or <code>\| =></code> is an alias for `default`) | `else`                                     |
| Multiple cases                                                     | `case 1, 2, 3, 4, 5`                       |
| Half/topical expressions                                           | `case typeof == 'str'`<br>`case 1 < $ < 3` |
| Optional bindings (+ destructuring)                                | `case (...x, 3)`                           |
| Optional guard statement                                           | `case (...x, 3) when 0 < x[1] < 100`       |

### Error Handling

| Feature                        | Example                                        |
| ------------------------------ | ---------------------------------------------- |
| Basic structure                | `try ... catch ... finally`                    |
| Multiple error + default types | `try ... catch TypeError ... catch ...finally` |

### Functions

Functions implicitly return the last statement unless explicitly declared with `return` only.

```coffee
twentyThree = () ->
  x = 10
  x += 10 + 3
  x

twentyThree! # 23
```

Just like in LiveScript, use `~>` in place of CoffeeScript's `=>` (bound function).

| Feature                   | Example                                                                                                                     |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Named function            | <pre>func divide a b:<br>&#9;return a / b</pre>                                                                             |
| Anonymous function        | `divide = (a, b) -> a / b`                                                                                                  |
| Half expressions          | `(< 3)` &rightarrow; `(x) -> x < 3`                                                                                         |
| Operators as functions    | `(!)` &rightarrow; `(x) -> !x`                                                                                              |
| Topic functions           | `(len $ < 4)` &rightarrow; `(x) -> len x < 4`                                                                               |
| Property access functions | `(.name)` &rightarrow; `(x) -> x.name` <br> `(.3)` &rightarrow; `(x) -> x[3]`                                               |
| Function calls            | No arguments: `a!` &rightarrow; `a()`<br>Multiple arguments: `a b c` &rightarrow; `a(b, c)`                                 |
| Unary functions           | `unary length = -> len $; length 'yes' # 3`                                                                                 |
| Infix functions           | `` infix sub = -> &0 - &1; 3 `sub` 1 # 2 ``                                                                                 |
| Named arguments           | `divide(:a :b)`<br>`divide a: 3, b: 2`                                                                                      |
| Named argument punning    | `divide a: 3, b: 2`                                                                                                         |
| Recursive functions       | `infin = -> infin!`                                                                                                         |
| Optional arguments        | `divide a? b ...`                                                                                                           |
| Default arguments         | Unnamed: `divide a = 10, b`<br>Named: `divide a: 10, b: 2`                                                                  |
| Arguments object          | `sum = -> &.reduce (-> &0 + &1) &0`                                                                                         |
| Partial application       | `divide = (a, b) => a / b`<hr>In order: `div10 = divide 10 _; div10 5 # 2`<br>Out of order: `half = divide _ 2; half 2 # 1` |
| Function composition      | Forward: `(a >> b)(x)` &rightarrow; `a(b(x))` <br> Backward: `(b << a)(x)` &rightarrow; `a(b(x))`                           |
| Function piping           | Forward: <code>a \|> b</code> &rightarrow; `b(a)` <br> Backward: <code>b <\| a</code> &rightarrow; `b(a)`                   |
| Multi-piping              | Forward: <code>a \|\|\|> b</code> &rightarrow; `b(b(b(a)))`                                                                 |
| Generator functions       | `genfn = (x) *> loop => yield x++`                                                                                          |
| Backcalls                 | `b <- (a << c) x` &rightarrow; `b(c(a(x)))`                                                                                 |

More sections #TODO

### Arrays

### Objects

### Maps

### Sets

### Records and Tuples

### Types

### Classes

### Interfaces

### Enumerations
