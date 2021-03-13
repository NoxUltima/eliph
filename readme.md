# Disclaimer

This language is but a **concept**. The Standard Library and Compiler and everything else will be released soon (perhaps a few years from now). I need time to work on it and get my college and uni settled. I wrote this document a few months ago.

# Nyx

**Nyx** is the language for folks who don't necessarily love JavaScript but who still acknowledge its importance in the ecosystem. It fully embraces the evolving JavaScript language, extending it with new and exciting features that enhance the readability and conciseness of traditional JavaScript.

Nyx compiles to clean, readable and performant JS, which you can run both in the browsers and Node. This means you can pick up Nyx and access the vast JS ecosystem and tooling as if you've known it for a long time! If you have an existing JavaScript or TypeScript codebase, Nyx code can be slipped in any codebase almost unnoticed.

```coffee
query = select user.id from user
  where user.name == 'boom' && user.id == 1
    || user.name == 'bang' && user.id == 2
```

Nyx has a syntax similar to Haskell, Swift, Ruby, OCaml, Nim, ReScript, Go, Python, and LiveScript. Some of the other languages which have inspired Nyx are C#, Bash, Julia, Elixir, F#, Crystal, PureScript and Elm.

## Why Nyx?

[coffeescript]: https://coffeescript.org/
[wtfjs]: https://github.com/denysdovhan/wtfjs
[stdlib]: https://stdlib.io/
[npm packages]: https://medium.com/@thomasfuchs/what-if-we-had-a-great-standard-library-in-javascript-52692342ee3f

**_Lagom_**. We deem curly braces, semicolons and even commas as unnecessary. Sometimes that applies too for parentheses. The only times you would need them are when you want to cram things into a single line. Some of the more unnecessary things that become a big hassle for developers like me, such as verbosity, word length and excessive use of punctuation, have been removed.

- Everything is an expression - even variable assignments and control blocks
- Shortened keyword, function and method names to minimise space
- Unnecessary punctuation have been removed, wherever it so fits: semicolons, commas and parentheses.
- An elaborate feature and syntax set, borrowed from many programming languages

**Static and robust**. JavaScript has a complete lack of types. It's also notorious for its [peculiar runtime behaviour][wtfjs], leading to unexpected and sometimes annoying side effects. TypeScript kind of _solves_ this by adding static and inferred types to the language, but this doesn't change the fact that it inherits all of JavaScript's problems.

- Types are inferred. You can even disable type-checking should you wish.
- Annotate as little or as much as you want. They can go anywhere!

- Types are erased after compilation and don't exist at runtime.

**One-to-one mapping**. Unreadable boilerplate JS code generated from other compiled-to-JS languages makes it so that it could be, practically speaking, hard to debug, hard to learn from and hard to integrate with existing JS.

For Nyx, we try to ensure that we preserve much of Nyx's syntax in the output rather than try to cram boilerplate code in the middle of functions. This is especially important while learning, where users might want to understand how the code's compiled and to audit for bugs.

- All JS features are preserved; while some are not so obvious and require some ordering of terms.
- Comments are permanently preserved in the final output, matching your source code as much as possible.
- Type annotations are not "removed" from the output, but rather transformed into comments.
- Standard Library functions and operations generated as prototype methods and functions at the top of the file.
- Variables with "illegal" or invalid names are wrapped with an object.

---

## History of Nyx

The story of Nyx began as a side gig in early 2020 when I was building JavaScript programs and algorithms that I used to collect from school for use in my projects. Some of these algorithms come from Stack Overflow, some from standard and third-party libraries and others I developed in my own. All these functions were written using an intermediary language CoffeeScript. Soon enough, these functions eventually would form the core of the Standard Library.

As I was developing these algorithms in CoffeeScript, I experimented with code themes and regular expressions. I modified the original source code of the CoffeeScript syntax, and created a new theme based on One Dark Pro where I tweaked and modified its colors.

---

Many programming languages and frameworks often have adequate language support in integrated development environments. Language support is a fancy term for code snippets, syntax highlighting, boilerplate, documentation, language references and even an extensive ecosystem of plugins, packages and Stack Overflow developers.

## Roadmap

- Documentation
- Standard library
- Syntax highlighting
- Compiler and Formatter
- Linter and debugger

### Documentation

The roadmap for developing the language has to start with the documentation, as that would give me a head start on the grammatical and syntactic features of the language. The documentation will be written with Markdown, which would explain the features, grammar, functions and modules in the language and its core library, and explain the similarities and differences between it and other programming languages.

### Syntax Highlighting

Syntax highlighting displays text, especially source code, in different colours and text styles according to the category of terms, while visually distinguishing structures and syntax errors.
Code is parsed through a series of regular expressions, and each match is assigned a scope. These scopes are mapped to colors when you install themes in your IDE.

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
