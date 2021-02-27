# Disclaimer

This language is but a **concept**. The compiler and everything else will be released soon (perhaps a few years from now). I just need time to work on it, and get my studies settled.

# Eliph

**Eliph** is how (I think) JavaScript should be like. The golden rule is, if it looks like JavaScript, it should work _with_ and _like_ JavaScript, and compiles to short, sweet and readable JavaScript code. So it should be seen as an attempt to expose and extend the good parts of JavaScript in a simple way, powered by the increasingly rampant JavaScript ecosystem and its many packages and modules.

The language borrows and blends elements and concepts from different programming languages&mdash;reactive, object-oriented and functional programming. Alright, let's begin. It is a completely new programming language by itself, so you can write more sophisticated code with tons of syntactic sugar and powerful features and a large standard library.

Eliph has a syntax similar to Swift, Go, Reason, Dart and Scala, features similar to Haskell, CoffeeScript and LiveScript, and with functions and modules similar to Python and Ruby.

## History of Eliph

Eliph first began as a side gig in early 2020 when I developed algorithms and programs in Python and JavaScript during my free time, but using the former twice as much. However in order to use my Python command line programs in my web development projects I wanted to rewrite my codes in JS, but having to go over to Stack Overflow and manually searching for the exact functions in my code which uses highly specialised Python functions and libraries unavailable and difficult to find in JS.

Also the functions which JavaScript offers are often too difficult to understand and may often require some further explanation to comprehend, after looking at the documentation. As I grew deeply obsessed with programming in JS due to the idea that one can design and develop everything they imagine using only one language, this lead me to pursue a goal of creating a new language that blends the simplicity and ease of Python with the malleability of JavaScript, along with syntaxes and operations inspired by different programming languages.

## Why Eliph?

This all could be summed up in a few different points:

[coffeescript]: https://coffeescript.org/
[wtfjs]: https://github.com/denysdovhan/wtfjs
[stdlib]: https://stdlib.io/
[npm packages]: https://medium.com/@thomasfuchs/what-if-we-had-a-great-standard-library-in-javascript-52692342ee3f

**Eliph is _lagom_**. Preserving JavaScript-like syntax is a clear must, mainly for people who come from languages like C, Java or even JS would be able to learn quickly. However, some of the more unnecessary things that really become a big hassle for developers like me, such as verbosity, word length and excessive use of punctuation, have been removed.

- **Shortened keyword names**: `function -> func`, `instanceof -> instof`, `extends -> from / of`, `implements -> with`
- **Unnecessary punctuation have been removed**, such as semicolons `;`, commas `,`, and parentheses `()` in statements like `if ()` and `for ()` are removed.
- **Everything is an expression**, and can be assigned to variables and returned from functions, which includes control flow statements like `if`, `for` and `try`.
- **Optional declarations** with `var`, `let` or `const` are only allowed when initializing a variable without a value or one in a loop.
- **Implicit returns**: the last statement is automatically returned from a `do`-block (closure) or a function, unless otherwise specified with `return`.

**Static and robust types**. JavaScript, because of its complete lack of types, resulting in its [peculiar runtime behaviour](https://github.com/denysdovhan/wtfjs), which can lead to unexpected and sometimes annoying side effects. TypeScript aimed to provide better tooling for JavaScript, by adding static typing to the JavaScript language, but inherits all of its problems, and has a much slower build process than modern JavaScript since it always has to be "compiled" by type-checking, hence significantly adding a lot more to the build time.

- Types in Eliph are **automatically inferred.** You don't need to explicitly assign a type to a variable. If you want to disable type checking for a variable whenever you're working with a third-party JavaScript library, you can use the `any` type.
- You can annotate **anywhere** within your code, even within expressions, so you can assure yourself and also other people who will be maintaining your code, that you know what you're doing.
- **A type should not change into another.** In JavaScript, your variable's type might change when the code runs, hence causing a wide range of side-effects. This is an anti-feature; it makes the code much harder to understand when reading or debugging.
- **Types are erased after compilation** and don't exist at runtime. You don't need type info during runtime; so any type errors are automatically reported at compile time so you can catch the bugs earlier.
- **A type system that is sometimes incorrect can be dangerous** due to expectation mismatches. Most type systems make a guess at the type of a value and show you a type in your editor that's sometimes incorrect.

**Dependency-free**. Eliph aims to provide a suite of built-in classes, methods and functions that provide more than what JS can, so there is no need for you to compose your own functions on the fly. At the same time, Eliph should include in and of itself a **standard library** (inspired by languages like Python, Ruby and Go) since the JS ecosystem is littered with dependencies. Shipping the final product inevitably drags in a huge amount of code, most of which the project doesn't actually use.

- Eliph can be used directly on Node.JS and even has its own standalone library with no dependencies, `@eliph/stdlib`, similar to other compile-to-JS languages.
- The Eliph standard library can be used directly on any Node.JS application, even alongside other to-JS languages like TypeScript and CoffeeScript.

**One-to-one mapping**. Unreadable boilerplate JS code generated from other compiled-to-JS languages makes it so that it could be, practically speaking, hard to debug, hard to learn from and hard to integrate with existing handwritten JS. Whereas for Eliph, the compiled output is automatically mapped to one source file, while the code structure is preserved. This is especially important while learning, where users might want to understand how the code's compiled, and to audit for bugs. Eliph does a number of things to remove unnecessary boilerplate code from the compiled output.

- Syntactic sugar, `stdlib` modules and built-in functions such as range literals, fractions and s(p)licing, whenever mentioned in Eliph code, are automatically generated as import statements from `@eliph` in the final output, and map cleanly to regular JavaScript functions.
- Variables and constants are temporary. They are declared `let` by default the moment they first appear. Those with **illegal identifier names**, or the values which are passed onto the `del` statement, are put in a "header" object that exists only on the current scope.

---

## the Compilation Process

---

## Eliph's Standard Library

While the Eliph Language Reference describes the syntax and semantics and programming of the Eliph programming language, this library reference manual describes the standard library that is distributed in Eliph's module `@eliph/stdlib`. It also describes some of the optional components that are commonly included in Python distributions.

Eliph's standard library is very extensive, offering a wide range of facilities as indicated by the long table of contents listed below. These modules written in JavaScript that provide standardized solutions for many problems that occur in everyday programming.

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
      4. Regular Expressions
   6. Ranges, Sequences and Comprehensions
      1. Literals `[a<:b:c,d]`
      2. Array and Object Comprehensions
   7. Data Structures
      1. Tuples `()` and Arrays `[]`
      2. Objects `{}` and Records `(| |)`
      3. Maps `{| |}` and Sets `[| |]`
      4. Weak Sets `#[]` and Maps `#{}`
      5. Destructuring assignment
5. Control Flow
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
6. Functions
   1. `func` declaration
   2. Recursion
   3. Generators
   4. First-class functions
   5. Composition
   6. Piping
   7. Currying
7. Types
   1. `any`, `void`, `unknown`, `other` and `never`
   2. Type aliases
   3. Literal types
   4. Unions and intersection types
   5. Interfaces
   6. `enum`
      1. Default
      2. Ranged Values
      3. Non-Numeric Values
8. Classes
   1. Constructors and instances
   2. Methods and attributes
   3. Inheritance and mixins
   4. Access modifiers
9. Modules
   1. Import and export
   2. Using NPM modules
   3. Namespaces

Standard Library

1.  Text Processing `text`
    1. `string` - advanced string manipulation
    2. `regexp` - advanced regular expressions and operations
    3. `unicode` - Unicode character data
2.  Mathematical and Numeric Modules (inspired by MathJS)
    1. `math` (alias `quickmafs` - mathematical functions
    2. `decimal` - decimal fixed point and floating point arithmetic
    3. `fraction` - rational numbers
    4. `complex` - complex numbers
    5. `algebra` - algebra and polynomials
    6. `random`, `seed`, `chance` - PRNG and advanced (seeded) random generation
    7. `radix` - formatting and converting numbers between locales and bases
    8. `units` - unit conversion
    9. `stats` - statistics functions
    10. `money` - currency conversion and manipulation
3.  Data Types (inspired by Moment and DateJS)
    1. `datetime` — date parsing, conversion and manipulation
    2. `datetime.timezone` — IANA time zone support
    3. `calendar` — calendar-related functions
    4. `mutable` - mutable data structures
    5. `immutable` - immutable data structures
4.  Data Analysis and Manipulation (insipred by SciPy)
    1. `transform` - data manipulation and transformation algorithms
    2. `sym` - scientific computing and data analysis tools
    3. `plot` - data visualization tools
5.  Reactive Programming (inspired by RXJS)
    1. `react` - tools for reactive programming
    2. `reactfunc` - reactive functional programming
6.  Functional Programming (inspired by Ramda and LazyJS)
    1. `iterator` - functions creating iterators for efficient looping
    2. `function` - higher-order functions and operations on callable objects
    3. `operator` - operators as functions
7.  File System and I/O
    1. `glob` - Unix style pathname pattern expansion
    2. `pathlib` — Object-oriented filesystem paths
    3. `os` and `path` — Common pathname manipulations
    4. `schedule` - Task scheduler
8.  Data Serialization, Web Templating and Design
    1. `json`, `yaml`, `toml` - data serialization for JSON, YAML and TOML config files
    2. `url` - URL utilities and manipulation
    3. `html` - templating utilities
    4. `color` - color manipulation
    5. `csv` - CSV file reading and writing
    6. `css` - CSS functions and conversions
    7. `html` - HTML manipulation, templating and functions
    8. `convert` - templating language conversion
9.  Data Generation
    1.  `datagen` - data generation library
10. Security and Cryptography
    1. `crypto` - cryptography and security algorithm and tools
    2. `passhash` - password hashing algorithms
11. Internationalization and Localization
    1. `i18n` - tools for i18n, with built-in plurals
12. APIs and web services (inspired by Axios)
    1.  `api` - tools for interacting with web APIs
    2.  `rest` - building web APIs
13. Machine Learning (inspired by scikit-learn)
    1. `mine` - a web scraping module for JS
    2. `ml.classify` - classification
    3. `ml.regress` - regression
    4. `ml.cluster` - clustering
    5. `ml.reduce` - dimensionality reduction
    6. `ml.select` - validating/comparing parameters
    7. `ml.process` - extraction and normalization
14. Natural Language Processing
    1.  `lang` - textual processing and analysis
    2.  `lang.data` - datasets and corpora for NLP
    3.  `lang.model` - NLP framework and pipeline
    4.  `lang.gen` - natural language generation modules
    5.  `lang.topic` - Gensim-inspired topic modeling
15. Code Analysis (inspired by Flow and TypeScript)
    1.  `typecheck` - static runtime type checking
    2.  `assert` - testing and debugging tools
    3.  `format` - code formatter and prettifier
16. the Eliph Programming Language
    1.  `parser` — Access Eliph parse trees
    2.  `ast` — Abstract Syntax Trees
    3.  `symtable` — Access to the compiler's symbol tables
    4.  `symbol` — Constants used with Eliph parse trees
    5.  `token` — Constants used with Eliph parse trees
    6.  `keyword` — Testing for Eliph keywords
    7.  `tokenize` — Tokenizer for Eliph source code
